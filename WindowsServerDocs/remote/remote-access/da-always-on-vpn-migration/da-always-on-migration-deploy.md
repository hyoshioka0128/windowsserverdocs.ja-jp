---
title: Always On VPN を DirectAccess からの移行
description: DirectAccess から Always On VPN への移行には、特定のプロセスに役立ちますが順不同の移行手順の実行に起因する競合状態を最小限に抑えるクライアントを移行する必要があります。
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 06/07/2018
ms.openlocfilehash: 94852b33936ece0b329614f428e845f2c7a2ac6a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854583"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Always On VPN への移行と DirectAccess の使用停止

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#171;[**前。** DirectAccess Always On VPN への移行からを計画します。](da-always-on-migration-planning.md)<br>

DirectAccess から Always On VPN への移行には、特定のプロセスに役立ちますが順不同の移行手順の実行に起因する競合状態を最小限に抑えるクライアントを移行する必要があります。 大まかに言えば、移行プロセスは 4 つの主な手順で構成されます。

1.  **サイド バイ サイドでの VPN インフラストラクチャをデプロイします。** 移行フェーズと展開に追加する機能を確認した後は、既存の DirectAccess のインフラストラクチャと並行 VPN インフラストラクチャを配置します。  

2.  **証明書と構成をクライアントに展開します。**  VPN インフラストラクチャ準備ができたら、作成し、クライアントに必要な証明書を発行します。 クライアントが証明書を受信したときに、VPN_Profile.ps1 構成スクリプトを配置します。 または、Intune を使用して、VPN クライアントを構成することができます。 正常な VPN 構成の展開を監視するには、Microsoft System Center Configuration Manager または Microsoft Intune を使用します。

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

Always On VPN を DirectAccess からの移行プロセスを開始する前に、移行を予定していることを確認します。  移行が計画されていない場合は、次を参照してください。 [、DirectAccess から Always On VPN への移行を計画](da-always-on-migration-planning.md)します。

>[!TIP] 
>このセクションでは、Always On VPN の展開のステップ バイ ステップ ガイドではありませんが、補完するものではなく[Always On VPN 展開の Windows Server および Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)し移行に固有の展開のガイダンスを提供します。

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>サイド バイ サイドでの VPN インフラストラクチャをデプロイします。

既存の DirectAccess のインフラストラクチャと並行 VPN インフラストラクチャを展開するとします。  ステップ バイ ステップの詳細については「 [Always On VPN 展開の Windows Server および Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)をインストールして、Always On VPN インフラストラクチャを構成します。 

サイド バイ サイド展開は、次の大まかなタスクで構成されます。

1.  VPN ユーザー、VPN サーバー、および NPS サーバーのグループを作成します。

2.  作成し、必要な証明書テンプレートを発行します。

3.  サーバー証明書を登録します。

4.  インストールし、Always On VPN のリモート アクセス サービスを構成します。

5.  インストールし、NPS を構成します。

6.  Always On VPN の DNS およびファイアウォール規則を構成します。

次の図は、VPN 移行 DirectAccess-に – Always 全体でインフラストラクチャの変更を視覚的な参照を提供します。

![](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>証明書と VPN 構成スクリプトをクライアントに展開します。

VPN クライアント構成の一括、[デプロイ Always On VPN](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md)セクション、2 つの追加 DirectAccess から Always On VPN への移行を正常に完了する手順が必要です。 

いることを確認する必要があります、 **VPN_Profile.ps1**は_後_なしで接続する VPN クライアントが試行しないように、証明書が発行されています。 そのためには、証明書を使用して、Always On VPN 構成を展開する VPN 展開の準備がグループに登録したユーザーのみを追加するスクリプトを実行します。

>[!NOTE] 
>そのユーザー移行の呼び出し回数のいずれかで実行する前に、このプロセスをテストすることをお勧めします。

1.  **作成し VPN 証明書を発行し、自動登録のグループ ポリシー オブジェクト (GPO) を有効にします。** 従来、証明書ベースの Windows 10 の VPN 展開は、接続を認証できるようにデバイスまたはユーザーのいずれかに証明書が発行されます。 新しい認証証明書を作成して自動登録用にパブリッシュするは作成する必要があり、VPN ユーザー グループを構成した自動登録設定を使用した GPO をデプロイします。 証明書と自動登録を構成する手順については、次を参照してください。[サーバー インフラストラクチャを構成する](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)します。

2.  **VPN ユーザー グループにユーザーを追加します。** VPN ユーザー グループに移行するどのユーザーを追加します。 それらのユーザーは、今後のすべての証明書の更新プログラムを受信できるように移行した後、そのセキュリティ グループに残ります。 続行すると、Always On VPN DirectAccess からのすべてのユーザーに移動するまで、このグループにユーザーを追加します。 

3.  **VPN 認証証明書を受信したユーザーを特定します。** DirectAccess から移行するため、クライアントが必要な証明書を受信したし、の VPN の構成情報を受信する準備ができてを識別するためのメソッドを追加する必要があります。 実行、 **GetUsersWithCert.ps1** nonrevoked 証明書が指定した AD DS セキュリティ グループに指定したテンプレートの名前を元の発行元は現在のユーザーを追加するスクリプト。 たとえば、実行した後、 **GetUsersWithCert.ps1**スクリプト、すべてのユーザーで、VPN 認証証明書テンプレートは、VPN 展開の準備がグループに追加から有効な証明書が発行されました。

    >[!NOTE] 
    >クライアントが必要な証明書を受信したときに識別するためにメソッドがない、前に、VPN 接続に失敗する原因と、ユーザーが発行された証明書、VPN の構成をデプロイできます。 このような状況を回避するには、実行、 **GetUsersWithCert.ps1**証明機関で、または VPN 展開の準備がグループに証明書を受信したユーザーを同期するスケジュールに従ってスクリプトします。 そのセキュリティ グループは、System Center Configuration Manager または Intune を見ると、証明書を受信した前に、マネージ クライアントによって、VPN の構成が表示されませんが、VPN 構成の展開の対象に使用されます。
    
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

4. Always On VPN 構成をデプロイします。 実行して、vpn 認証証明書を発行は、 **GetUsersWithCert.ps1**スクリプトをユーザーが VPN 展開の準備完了のセキュリティ グループに追加されます。


| 使用する場合.  | 結果 |
| ---- | ---- |
| System Center Configuration Manager | そのセキュリティ グループのメンバーシップに基づいてユーザーのコレクションを作成します。<br><br>![](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)演算子|
| Intune | 同期されていると、セキュリティ グループを直接ターゲットだけです。 |
|
    
実行するたびに、 **GetUsersWithCert.ps1**構成スクリプトでは、System Center Configuration Manager でセキュリティ グループのメンバーシップを更新する AD DS の検出規則も実行する必要があります。 また、メンバーシップの更新プログラムの展開コレクションを頻繁に発生するのに十分なことを確認 (配置スクリプトと検出ルールを使用)。

System Center Configuration Manager または Intune を使用して、Windows クライアントに Always On VPN を展開する方法の詳細については、次を参照してください。 [Always On VPN 展開の Windows Server および Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)します。 必ず、ただし、これらの移行に固有のタスクを組み込む。

>[!NOTE] 
>単純な Always On VPN 展開および DirectAccess から Always On VPN への移行の重要な違いは、これらの移行に固有のタスクを組み込むことです。 正しく展開ガイドでメソッドを使用するのではなく、セキュリティ グループを対象とするコレクションを定義することを確認します。


## <a name="remove-devices-from-the-directaccess-security-group"></a>DirectAccess のセキュリティ グループからデバイスを削除します。

ユーザー認証証明書を受信すると、 **VPN_Profile.ps1**対応する System Center Configuration Manager または Intune での VPN 構成スクリプト展開が成功を確認する構成スクリプト。 それぞれの展開後に、DirectAccess を後で削除できるように DirectAccess のセキュリティ グループからそのユーザーのデバイスを削除します。 Intune と System Center Configuration Manager の両方には、各ユーザーのデバイスを判断するのに役立つユーザーとデバイスの割り当て情報が含まれています。

>[!NOTE] 
>コンピューター グループではなく、組織単位 (Ou) から DirectAccess の Gpo を適用する場合は、OU からユーザーのコンピューター オブジェクトを移動します。

## <a name="decommission-the-directaccess-infrastructure"></a>DirectAccess インフラストラクチャを使用停止します。

Always On VPN へのすべての DirectAccess クライアントの移行が完了したら、DirectAccess インフラストラクチャの使用を停止し、グループ ポリシーからの DirectAccess の設定を削除できます。 環境から DirectAccess を正常に削除するには、次の手順を実行するをお勧めします。

1.  [!INCLUDE [remove-config-settings-shortdesc-include](../includes/remove-config-settings-shortdesc-include.md)]

    ![](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

3.  **DNS をクリーンアップします。** 内部 DNS サーバーからすべてのレコードを削除してくださいし、パブリック DNS サーバーに関連する DirectAccess は、たとえば、DA.contoso.com、DAGateway.contoso.com します。

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

5.  **Active Directory 証明書サービスからの DirectAccess のすべての証明書を削除します。** DirectAccess は、実装をコンピューターの証明書を使用した場合は、証明機関 コンソールで証明書テンプレートのフォルダーから発行されたテンプレートを削除します。

## <a name="next-step"></a>次の手順
完了したら DirectAccess から Always On VPN への移行します。 

---