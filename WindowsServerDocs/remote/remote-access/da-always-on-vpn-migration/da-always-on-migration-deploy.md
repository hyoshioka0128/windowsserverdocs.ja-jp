---
title: DirectAccess から Always On VPN への移行
description: DirectAccess から Always On VPN に移行するには、クライアントを移行するための特定のプロセスが必要です。これにより、移行手順を順番に実行することによって発生する競合状態を最小限に抑えることができます。
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 06/07/2018
ms.openlocfilehash: a452c9ab1a24304a9acfec8357bc98a3d058e03c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971749"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Always On VPN への移行と DirectAccess の使用停止

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#171; [**前の手順:** VPN 移行を Always On するように DirectAccess を計画する](da-always-on-migration-planning.md)<br>

DirectAccess から Always On VPN に移行するには、クライアントを移行するための特定のプロセスが必要です。これにより、移行手順を順番に実行することによって発生する競合状態を最小限に抑えることができます。 大まかに言えば、移行プロセスは次の4つの主要な手順で構成されます。

1.  **サイドバイサイド VPN インフラストラクチャを展開します。** 移行フェーズと、展開に含める機能を決定したら、既存の DirectAccess インフラストラクチャと共に VPN インフラストラクチャをサイドバイサイドで展開します。

2.  **証明書と構成をクライアントに展開します。**  VPN インフラストラクチャの準備ができたら、必要な証明書を作成してクライアントに発行します。 クライアントが証明書を受信したら、VPN_Profile.ps1 構成スクリプトを展開します。 または、Intune を使用して VPN クライアントを構成することもできます。 Microsoft Endpoint Configuration Manager または Microsoft Intune を使用して、VPN 構成の展開が成功したかを監視します。

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

DirectAccess から Always On VPN への移行プロセスを開始する前に、移行の計画があることを確認してください。  移行を計画していない場合は、「 [VPN 移行を Always On に DirectAccess を計画する](da-always-on-migration-planning.md)」を参照してください。

>[!TIP]
>このセクションでは、Always On VPN の手順については説明していませんが、 [Windows Server と windows 10 向けの Vpn 展開の Always On](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)を補完し、移行に固有の展開のガイダンスを提供することを目的としています。

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>サイドバイサイド VPN インフラストラクチャを展開する

VPN インフラストラクチャは、既存の DirectAccess インフラストラクチャとサイドバイサイドで展開します。  詳細な手順については、「 [ALWAYS ON Vpn Deployment For Windows Server」および「windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) 」を参照して、Always On vpn インフラストラクチャをインストールして構成してください。

サイドバイサイド展開は、次の大まかなタスクで構成されています。

1.  VPN ユーザー、VPN サーバー、および NPS サーバーグループを作成します。

2.  必要な証明書テンプレートを作成して発行します。

3.  サーバー証明書を登録します。

4.  Always On VPN 用のリモートアクセスサービスをインストールして構成します。

5.  NPS をインストールして構成します。

6.  Always On VPN の DNS とファイアウォール規則を構成します。

次の図は、DirectAccess から Always On VPN への移行におけるインフラストラクチャの変更を視覚的に示しています。

![DirectAccess から Always On VPN への移行におけるインフラストラクチャの変更の図](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>証明書と VPN 構成スクリプトをクライアントに展開する

Vpn クライアント構成の大部分は[ALWAYS ON vpn の展開](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md)セクションにありますが、DirectAccess から Always On VPN への移行を正常に完了するには、2つの追加の手順が必要です。

VPN クライアントが接続を試行しないように、証明書が発行され_た後_に**VPN_Profile.ps1**が発生していることを確認する必要があります。 これを行うには、証明書に登録されているユーザーのみを VPN 展開の準備ができているグループに追加するスクリプトを実行します。このグループは、Always On VPN 構成を展開するために使用します。

>[!NOTE]
>このプロセスは、ユーザーの移行リングで実行する前にテストすることをお勧めします。

1.  **VPN 証明書を作成して発行し、自動登録グループポリシーオブジェクト (GPO) を有効にします。** 従来の証明書ベースの Windows 10 VPN 展開では、接続を認証できるように、デバイスまたはユーザーに対して証明書が発行されます。 新しい認証証明書が作成され、自動登録のために公開された場合、自動登録設定を構成した GPO を作成して、VPN Users グループに展開する必要があります。 証明書と自動登録を構成する手順については、「[サーバーインフラストラクチャの構成](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)」を参照してください。

2.  **VPN ユーザーグループにユーザーを追加します。** VPN ユーザーグループに移行するユーザーを追加します。 これらのユーザーは、後で証明書の更新を受け取ることができるように、移行後にそのセキュリティグループにとどまります。 すべてのユーザーを DirectAccess から Always On VPN に移動するまで、このグループへのユーザーの追加を続けます。

3.  **VPN 認証証明書を受け取ったユーザーを識別します。** DirectAccess から移行する場合は、クライアントが必要な証明書を受信し、VPN 構成情報を受信する準備ができたことを識別するメソッドを追加する必要があります。 **GetUsersWithCert.ps1**スクリプトを実行して、指定したテンプレート名から発行された非失効証明書を現在発行しているユーザーを、指定した AD DS セキュリティグループに追加します。 たとえば、 **GetUsersWithCert.ps1**スクリプトを実行すると、Vpn 認証証明書テンプレートから有効な証明書を発行したすべてのユーザーが、vpn 展開の準備ができたグループに追加されます。

    >[!NOTE]
    >クライアントが必要な証明書を受け取ったことを特定する方法がない場合は、ユーザーに証明書が発行される前に VPN 構成を展開して、VPN 接続が失敗するようにすることができます。 この状況を回避するには、証明機関またはスケジュールに基づいて**GetUsersWithCert.ps1**スクリプトを実行して、証明書を受信したユーザーを VPN 展開の準備ができたグループに同期します。 その後、そのセキュリティグループを使用して、Microsoft Endpoint Configuration Manager または Intune での VPN 構成の展開をターゲットにします。これにより、管理されたクライアントは、証明書を受信する前に VPN 構成を受信しなくなります。

    ### <a name="getuserswithcertps1"></a>GetUsersWithCert.ps1

    ```powershell
    Import-module ActiveDirectory
    Import-Module AdcsAdministration

    $TemplateName = 'VPNUserAuthentication'##Certificate Template Name (not the friendly name)
    $GroupName = 'VPN Deployment Ready' ##Group you will add the users to
    $CSServerName = 'localhost\corp-dc-ca' ##CA Server Information

    $users= @()
    $TemplateID = (get-CATemplate | Where-Object {$_.Name -like $TemplateName} | Select-Object oid).oid
    $View = New-Object -ComObject CertificateAuthority.View
    $NULL = $View.OpenConnection($CSServerName)
    $View.SetResultColumnCount(3)
    $i1 = $View.GetColumnIndex($false, "User Principal Name")
    $i2 = $View.GetColumnIndex($false, "Certificate Template")
    $i3 = $View.GetColumnIndex($false, "Revocation Date")
    $i1, $i2, $i3 | %{$View.SetResultColumn($_) }
    $Row= $View.OpenView()

    while ($Row.Next() -ne -1){
    $Cert = New-Object PsObject
    $Col = $Row.EnumCertViewColumn()
    [void]$Col.Next()
    do {
    $Cert | Add-Member -MemberType NoteProperty $($Col.GetDisplayName()) -Value $($Col.GetValue(1)) -Force
          }
    until ($Col.Next() -eq -1)
    $col = ''

    if($cert."Certificate Template" -eq $TemplateID -and $cert."Revocation Date" -eq $NULL){
       $users= $users+= $cert."User Principal Name"
    $temp = $cert."User Principal Name"
    $user = get-aduser -Filter {UserPrincipalName -eq $temp} –Property UserPrincipalName
    Add-ADGroupMember $GroupName $user
       }
      }
    ```

4. Always On VPN 構成を展開します。 VPN 認証証明書が発行され、 **GetUsersWithCert.ps1**スクリプトを実行すると、ユーザーが Vpn 展開準備完了セキュリティグループに追加されます。


| ...  | 結果 |
| ---- | ---- |
| Configuration Manager | そのセキュリティグループのメンバーシップに基づいてユーザーコレクションを作成します。<br><br>![[条件のプロパティ] ダイアログボックス](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)|
| Intune | 同期するときに、セキュリティグループを直接ターゲットにするだけです。 |

**GetUsersWithCert.ps1**構成スクリプトを実行するたびに、AD DS 検出ルールを実行して Configuration Manager のセキュリティグループメンバーシップを更新する必要もあります。 また、展開コレクションのメンバーシップの更新が頻繁に発生することを確認してください (スクリプトと検出ルールに合わせます)。

Configuration Manager または Intune を使用して Windows クライアントに Always On VPN を展開する方法の詳細については、「 [Windows Server および windows 10 用の Vpn 展開の Always On](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)」を参照してください。 ただし、これらの移行に固有のタスクを組み込むには、必ず注意してください。

>[!NOTE]
>これらの移行固有のタスクを組み込むことは、単純な Always On VPN の展開と、DirectAccess から Always On VPN への移行の間の重要な違いです。 展開ガイドのメソッドを使用するのではなく、セキュリティグループを対象とするようにコレクションを適切に定義するようにしてください。


## <a name="remove-devices-from-the-directaccess-security-group"></a>DirectAccess セキュリティグループからデバイスを削除する

ユーザーが認証証明書と**VPN_Profile.ps1**構成スクリプトを受信すると、Configuration Manager または Intune に、対応する VPN 構成スクリプトの展開が表示されます。 各展開後に、directaccess セキュリティグループからそのユーザーのデバイスを削除して、後で DirectAccess を削除できるようにします。 Intune と Configuration Manager には、各ユーザーのデバイスを特定するのに役立つユーザーデバイスの割り当て情報が含まれています。

>[!NOTE]
>コンピューターグループではなく組織単位 (Ou) を使用して DirectAccess Gpo を適用している場合は、ユーザーのコンピューターオブジェクトを OU の外に移動します。

## <a name="decommission-the-directaccess-infrastructure"></a>DirectAccess インフラストラクチャの使用停止

すべての DirectAccess クライアントの Always On VPN への移行が完了したら、DirectAccess インフラストラクチャを使用停止し、グループポリシーから DirectAccess 設定を削除することができます。 Microsoft では、環境から DirectAccess を適切に削除するために、次の手順を実行することをお勧めします。

1. **構成設定を削除します。** 次の図に示すように、リモートアクセス管理コンソールを開き、[構成設定の削除] を選択して、作成された Gpo とリモートアクセスグループポリシー設定のリモートアクセスを削除します。 構成を削除する前にグループを削除すると、エラーが発生する可能性があります。

    ![環境から DirectAccess を削除するプロセス](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2. **DirectAccess セキュリティグループからデバイスを削除します。** ユーザーが正常に移行すると、そのデバイスを DirectAccess セキュリティグループから削除します。 環境から DirectAccess を削除する前に、DirectAccess セキュリティグループが空かどうかを確認してください。 まだメンバーが含まれている場合は、セキュリティグループを削除しないでください。 メンバーが含まれているセキュリティグループを削除すると、そのデバイスからリモートアクセス権を持たない従業員を離れるリスクがあります。 Microsoft エンドポイント Configuration Manager または Microsoft Intune を使用して、デバイス割り当て情報を特定し、各ユーザーに属するデバイスを検出します。

3. **DNS をクリーンアップします。** 内部 DNS サーバーと、DirectAccess に関連するパブリック DNS サーバー (たとえば、DA.contoso.com、DAGateway.contoso.com) からすべてのレコードを削除してください。

4. **DirectAccess サーバーの使用を停止します。** 構成設定と DNS レコードが正常に削除されたら、DirectAccess サーバーを破棄することができます。 これを行うには、サーバーマネージャーでロールを削除するか、サーバーを使用停止にして AD DS から削除します。

5. **Active Directory 証明書サービスからのすべての DirectAccess 証明書を削除します。** DirectAccess の実装にコンピューター証明書を使用していた場合は、証明機関コンソールの [証明書テンプレート] フォルダーから、発行されたテンプレートを削除します。

## <a name="next-step"></a>次のステップ

DirectAccess から Always On VPN への移行が完了しました。
