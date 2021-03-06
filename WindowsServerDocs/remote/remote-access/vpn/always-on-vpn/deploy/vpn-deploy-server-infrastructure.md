---
title: サーバー インフラストラクチャを構成します。
description: この手順では、インストールし、VPN をサポートするために必要なサーバー側コンポーネントを構成します。 サーバー側コンポーネントには、ユーザー、VPN サーバー、および NPS サーバーで使用される証明書を配布するための PKI の構成が含まれます。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 8a07d84427b770da465b8712d71eb846a7c9cf8d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749605"
---
# <a name="step-2-configure-the-server-infrastructure"></a>手順 2. サーバー インフラストラクチャを構成します。

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** 手順 1.Always On VPN 展開を計画する](always-on-vpn-deploy-planning.md)
- [**次に：** 手順 3.Always On VPN 用にリモート アクセス サーバーを構成する](vpn-deploy-ras.md)

この手順でインストールし、VPN をサポートするために必要なサーバー側コンポーネントを構成します。 サーバー側コンポーネントには、ユーザー、VPN サーバー、および NPS サーバーで使用される証明書を配布するための PKI の構成が含まれます。  またの IKEv2 接続と VPN 接続の承認を実行する NPS サーバーをサポートするように RRAS を構成します。

## <a name="configure-certificate-autoenrollment-in-group-policy"></a>グループ ポリシーで証明書の自動登録を構成します。
この手順でポリシーを構成するグループ、ドメイン コント ローラーのドメインのメンバーが自動的にユーザーとコンピューターの証明書を要求できるようにします。 これにより、VPN ユーザーを要求し、自動的に VPN 接続を認証するユーザー証明書を取得します。 同様に、このポリシーにより、サーバー要求を NPS サーバー認証証明書を自動的にします。 

VPN サーバーに証明書を手動で登録します。

>[!TIP]
>非 domained 参加しているコンピューターでは、次を参照してください。[ドメイン以外の CA の構成には、コンピューターが参加している](#ca-configuration-for-non-domain-joined-computers)します。 RRAS サーバーがドメイン参加済みでないため、VPN ゲートウェイの証明書を登録する自動登録を使用できません。  そのため、オフラインの証明書の要求手順を使用します。

1. ドメイン コント ローラーで、グループ ポリシーの管理を開きます。

2. ナビゲーション ウィンドウで、ドメイン (corp.contoso.com など) を右クリックし、選択**このドメインに GPO を作成し、リンクする**します。

3. [新しい GPO] ダイアログ ボックスで、次のように入力します。**の自動登録ポリシー**を選択し、 **OK**します。

4. ナビゲーション ウィンドウで右**の自動登録ポリシー**を選択し、**編集**します。

5. グループ ポリシー管理エディターでは、コンピューター証明書の自動登録を構成する次の手順を完了します。

    1. ナビゲーション ウィンドウに移動**コンピューターの構成** > **ポリシー** > **Windows 設定** >  **セキュリティ設定** > **公開キー ポリシー**します。

    2. 詳細ペインで右クリックして**証明書サービス クライアント – 自動登録**を選択し、**プロパティ**します。

    3. 証明書サービス クライアント – 自動登録のプロパティ ダイアログ ボックスで**構成モデル**、**有効**します。

    4. **[有効期限が切れた証明書を更新、保留中の証明書を更新、および破棄された証明書を削除する]** と **[証明書テンプレートを使用する証明書を更新する]** を選択します。

    5. **[OK]** を選択します。

6. グループ ポリシー管理エディターでは、ユーザー証明書の自動登録を構成する次の手順を完了します。

    1. ナビゲーション ウィンドウに移動**ユーザー構成** > **ポリシー** > **Windows 設定** >  **セキュリティ設定** > **公開キー ポリシー**します。

    2. 詳細ウィンドウで **[証明書サービス クライアント - 自動登録]** を右クリックして **[プロパティ]** を選択します。

    3. 証明書サービス クライアント – 自動登録のプロパティ ダイアログ ボックスで**構成モデル**、**有効**します。

    4. **[有効期限が切れた証明書を更新、保留中の証明書を更新、および破棄された証明書を削除する]** と **[証明書テンプレートを使用する証明書を更新する]** を選択します。

    5. **[OK]** を選択します。

    6. グループ ポリシー管理エディターを閉じます。

7. [グループ ポリシーの管理] を閉じます。

### <a name="ca-configuration-for-non-domain-joined-computers"></a>非ドメイン参加済みコンピューターの CA の構成

RRAS サーバーがドメイン参加済みでないため、VPN ゲートウェイの証明書を登録する自動登録を使用できません。  そのため、オフラインの証明書の要求手順を使用します。

1. という名前のファイルを生成、RRAS サーバーで**VPNGateway.inf** (セクション 0) の付録で提供される証明書ポリシー要求の例に基づくし、次のエントリをカスタマイズします。

   - [リクエスト] セクションで置き換える vpn.contoso.com 選択した証明書のサブジェクト名の使用 [_顧客_] VPN エンドポイントの FQDN。

   - [拡張機能] セクションで置換 vpn.contoso.com 選択した証明書のサブジェクト代替名の使用 [_顧客_] VPN エンドポイントの FQDN。

2. 保存またはコピー、 **VPNGateway.inf**ファイルを選択した場所にします。

3. 含むフォルダーに移動しますから管理者特権のコマンド プロンプトで、 **VPNGateway.inf**ファイルと型。

   ```
   certreq -new VPNGateway.inf VPNGateway.req
   ```

4. 新しく作成されたコピー **VPNGateway.req**証明機関サーバー、または Privileged Access Workstation (PAW) を出力ファイル。

5. 保存またはコピー、 **VPNGateway.req**証明機関サーバー、または Privileged Access Workstation (PAW) で、選択した場所にファイル。

6. 管理者特権でコマンド プロンプトで、種類と前の手順で作成した VPNGateway.req ファイルが含まれているフォルダーに移動します。

   ```
   certreq -attrib “CertificateTemplate:[Customer]VPNGateway” -submit VPNgateway.req VPNgateway.cer
   ```

7. 証明機関の一覧 ウィンドウでは、メッセージが表示されたら、証明書要求の処理を適切なエンタープライズ CA を選択します。

8. 新しく作成されたコピー **VPNGateway.cer** RRAS サーバーへの出力ファイル。 

9. 保存またはコピー、 **VPNGateway.cer** RRAS サーバーで、選択した場所にファイル。

10. 管理者特権でコマンド プロンプトで、種類と前の手順で作成した VPNGateway.cer ファイルが含まれているフォルダーに移動します。

    ```
    certreq -accept VPNGateway.cer
    ```

11. 説明したように、証明書の MMC スナップインで実行[ここ](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in)を選択すると、**コンピューター アカウント**オプション。

12. 次のプロパティを持つ RRAS サーバーの有効な証明書が存在することを確認します。

    - **目的:** サーバー認証、IP セキュリティ IKE 中間 

    - **証明書テンプレート:** [_顧客_] VPN サーバー

#### <a name="example-vpngatewayinf-script"></a>以下に例を示します。VPNGateway.inf script

ここで、帯域外のプロセスを使用して VPN ゲートウェイの証明書を要求するために使用する証明書要求ポリシーのスクリプトの例を確認できます。

>[!TIP]
>証明書の要求ポリシー フォルダーの下 VPN サービス IP キット VPNGateway.inf スクリプトのコピーが見つかります。 'Subject' にのみ更新と '\_続行\_' 顧客固有の値を使用します。

```
[Version] 

Signature="$Windows NT$"

[NewRequest]
Subject = "CN=vpn.contoso.com"
Exportable = FALSE   
KeyLength = 2048     
KeySpec = 1          
KeyUsage = 0xA0      
MachineKeySet = True
ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
RequestType = PKCS10 

[Extensions]
2.5.29.17 = "{text}"
_continue_ = "dns=vpn.contoso.com&"
```

## <a name="create-the-vpn-users-vpn-servers-and-nps-servers-groups"></a>VPN ユーザー、VPN サーバー、および NPS サーバーのグループを作成します。

この手順では、VPN を使用して、組織のネットワークに接続を許可するユーザーを含む、新しい Active Directory (AD) グループを追加できます。

このグループには、2 つの目的があります。

- VPN が必要です。 ユーザーの証明書に登録できるユーザーを定義します。

- NPS は、VPN アクセスを承認するユーザーを定義します。

カスタム グループを使用して、ユーザーの VPN アクセスを失効する場合をから削除できますそのユーザー グループ。

また、NPS サーバーを含む別のグループと VPN サーバーを含むグループを追加します。 証明書の要求をそのメンバーに制限するのにには、これらのグループを使用します。

>[!NOTE]
>VPN をお勧め DMA/境界内に存在するサーバーがドメインに参加していることできません。 ただし、管理の容易さのドメインに参加している VPN サーバーがある場合 (グループ ポリシー、バックアップの監視エージェントでは、ローカル ユーザーを管理する)、AD グループを追加、VPN サーバーの証明書テンプレート。

### <a name="configure-the-vpn-users-group"></a>VPN ユーザー グループを構成します。

1. ドメイン コント ローラーで、Active Directory ユーザーとコンピューターを開きます。

2. コンテナーまたは組織単位を右クリックして**新規**を選択し、**グループ**します。

3. **グループ名**、入力**VPN ユーザー**を選択し、 **OK**します。

4. 右クリック**VPN ユーザー**選択**プロパティ**します。

5. **メンバー**選択 [VPN ユーザーのプロパティ] ダイアログ ボックスのタブ**追加**します。

6. [ユーザーの選択] ダイアログ ボックスで、VPN アクセスおよび選択が必要なすべてのユーザーを追加**OK**します。

7. [Active Directory ユーザーとコンピューター] を閉じます。

### <a name="configure-the-vpn-servers-and-nps-servers-groups"></a>VPN サーバーと NPS サーバーのグループを構成します。

1. ドメイン コント ローラーで、Active Directory ユーザーとコンピューターを開きます。

2. コンテナーまたは組織単位を右クリックして**新規**を選択し、**グループ**します。

3. **グループ名**、入力**VPN サーバー**を選択し、 **OK**します。

4. 右クリック**VPN サーバー**選択**プロパティ**します。

5. **メンバー**選択 [VPN サーバーのプロパティ] ダイアログ ボックスのタブ**追加**します。

6. 選択**オブジェクトの種類**を選択します、**コンピューター**チェック ボックスをオンし、選択**OK**します。

7. **選択するオブジェクト名を入力します**、VPN サーバーの名前を入力し、選択、 **OK**。

8. 選択**OK** VPN サーバーのプロパティ ダイアログ ボックスを閉じます。

9. NPS サーバー グループの前の手順を繰り返します。

10. [Active Directory ユーザーとコンピューター] を閉じます。

## <a name="create-the-user-authentication-template"></a>ユーザー認証テンプレートを作成します。

この手順では、カスタムのクライアントとサーバーの認証テンプレートを構成します。 このテンプレートは、アップグレードの互換性レベルを選択して、証明書の全体的なセキュリティを強化するために必要な Microsoft のプラットフォーム暗号化プロバイダーを選択します。 この最後の変更では、証明書をセキュリティで保護するクライアント コンピューターで TPM を使用できます。 TPM の概要については、次を参照してください。[トラステッド プラットフォーム モジュール テクノロジの概要](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview)します。

**手順:**

1. CA で、証明機関を開きます。

2. ナビゲーション ウィンドウで右**証明書テンプレート**選択と**管理**します。

3. 証明書テンプレート コンソールで、右クリックして**ユーザー**選択**テンプレートの複製**します。

   >[!WARNING]
   >選択しない**適用**または**OK**手順 10 の前に、いつでもです。  すべてのパラメーターを入力する前にこれらのボタンを選択した場合、多くの選択肢は固定し、不要になった編集可能になります。 などの**暗号化**タブの場合は_レガシ暗号ストレージ プロバイダー_プロバイダーのカテゴリ フィールドに、無効になります、以降のすべての変更を防止を示します。 唯一の代替手段は、テンプレートを削除して再作成します。  

4. 新しいテンプレートのプロパティ ダイアログ ボックスで、**全般** タブで、次の手順します。

   1. **テンプレート表示名**、型**VPN ユーザーの認証**します。

   2. クリア、 **Active Directory で証明書を発行**チェック ボックスをオンします。

5. **セキュリティ** タブで、次の手順を完了します。

   1. **[追加]** をクリックします。

   2. ユーザーの選択、コンピューター、サービス アカウント、またはグループ ダイアログ ボックスで次のように入力します。 **VPN ユーザー**を選択し、 **OK**します。

   3. **グループまたはユーザー名**、 **VPN ユーザー**します。

   4. **VPN ユーザーのアクセス許可**を選択、**登録**と**自動登録**のチェック ボックス、**許可**列。

      >[!TIP]
      >ように、読み取りのチェック ボックスをオンのままにしてください。 つまり、登録の読み取り権限が必要です。 

   5. **グループまたはユーザー名**を選択します**Domain Users**を選択し、**削除**します。

6. **互換性** タブで、次の手順を完了します。

   1. **証明機関**、 **Windows Server 2012 R2**します。

   2. **結果的な変更**ダイアログ ボックスで、 **OK**します。

   3. **証明書の受信者**、 **Windows 8.1/Windows Server 2012 R2**します。

   4. **結果的な変更**ダイアログ ボックスで、 **OK**します。

7. **要求処理**タブで、、**をエクスポートする秘密キーを許可する**チェック ボックスをオンします。

8. **暗号化** タブで、次の手順を完了します。

   1. **プロバイダーのカテゴリ**、 **Key Storage Provider**します。

   2. 選択**要求は、次のプロバイダーのいずれかを使用する必要があります**します。

   3. 選択、 **Microsoft プラットフォーム暗号化プロバイダー**チェック ボックスをオンします。

9. **サブジェクト名**タブのチェック ボックスをオフのすべてのユーザー アカウントに記載されている電子メール アドレスを持ち、**サブジェクト名に電子メール名を含める**と**電子メール名**チェック ボックス。

10. 選択**OK** VPN ユーザーの認証の証明書テンプレートを保存します。

11. 証明書テンプレート コンソールを閉じます。

12. 証明機関スナップインのナビゲーション ウィンドウで右**証明書テンプレート**を選択します**新規**選び**発行する証明書テンプレート**します。

13. 選択**VPN ユーザーの認証**を選択し、 **OK**します。

14. 証明機関スナップインを閉じます。

## <a name="create-the-vpn-server-authentication-template"></a>VPN サーバーの認証テンプレートを作成します。

この手順では、VPN サーバーの新しいサーバーの認証テンプレートを構成できます。 拡張キー使用法を 1 つ以上の証明書がサーバー認証で使用可能な場合、IP セキュリティ (IPsec) の IKE 中間アプリケーションのポリシーにより、サーバー証明書のフィルターを追加します。

>[!IMPORTANT]
>VPN クライアントは、このサーバーをパブリック インターネットからアクセスするため、サブジェクトと代替名は内部サーバー名と異なるです。 その結果、VPN サーバーでこの証明書自動登録をできません。

**前提条件:**

VPN サーバーのドメインに参加しています。

**手順:**

1. CA で、証明機関を開きます。

2. ナビゲーション ウィンドウで右**証明書テンプレート**選択と**管理**します。

3. 証明書テンプレート コンソールで、右クリックして**RAS および IAS サーバー**選択**テンプレートの複製**します。

4. [新しいテンプレートのプロパティ] ダイアログ ボックスで、**全般**] タブの [**テンプレート表示名**など、VPN サーバーのわかりやすい名前を入力します**VPN サーバー認証**または**RADIUS サーバー**します。

5. **拡張機能** タブで、次の手順を完了します。

    1. 選択**アプリケーション ポリシー**を選択し、**編集**します。

    2. **アプリケーション ポリシー拡張の編集**ダイアログ ボックスで、**追加**します。

    3. **アプリケーション ポリシーの追加**ダイアログ ボックスで、 **IP セキュリティ IKE 中間**を選択し、 **OK**します。
   
        セキュリティ IKE 中間、EKU には、IP を追加するため、VPN サーバーでは、複数のサーバー認証証明書が存在するシナリオで役立ちます。 IP セキュリティ IKE 中間が存在する場合は、IPSec により、証明書が両方の EKU オプションのみ使用されます。 これを行わない IKEv2 認証でした 13801 エラーで失敗します。IKE 認証資格情報は、許容されません。

    4. 選択**OK**に戻る、**新しいテンプレートのプロパティ** ダイアログ ボックス。

6. **セキュリティ** タブで、次の手順を完了します。

    1. **[追加]** をクリックします。

    2. **[ユーザー、コンピューター、サービス アカウント、またはグループ**] ダイアログ ボックスに、入力**VPN サーバー**を選択し、 **OK**します。

    3. **グループまたはユーザー名**、 **VPN サーバー**します。

    4. **VPN サーバーのアクセス許可**を選択、**登録** チェック ボックス、**許可**列。

    5. **グループまたはユーザー名**、 **RAS and IAS Servers**を選択し、**削除**します。

7. **サブジェクト名** タブで、次の手順を完了します。

    1. 選択**要求に含まれる**します。

    2. **証明書テンプレート**警告ダイアログ ボックスで**OK**します。

8. (省略可能)VPN 接続用の条件付きアクセスを構成する場合は、選択、**要求処理**タブを選び**をエクスポートする秘密キーを許可する**します。

9. 選択**OK** VPN サーバーの証明書テンプレートを保存します。

10. 証明書テンプレート コンソールを閉じます。

11. 証明機関スナップインのナビゲーション ウィンドウで右**証明書テンプレート**を選択します**新規**選び**発行する証明書テンプレート**します。

12. 前述の手順 4 で選択した名前を選択し、クリックして **OK**します。

13. 証明機関スナップインを閉じます。

## <a name="create-the-nps-server-authentication-template"></a>NPS サーバーの認証テンプレートを作成します。

3 番目および最後の証明書テンプレートを作成するには、NPS サーバーの認証のテンプレートです。 NPS サーバーの認証のテンプレートは、このセクションでは、先ほど作成した NPS サーバーのグループにセキュリティで保護する RAS および IAS サーバー テンプレートの単純なコピーです。

この証明書の自動登録を構成します。

**手順:**

1. CA で、証明機関を開きます。

2. ナビゲーション ウィンドウで右**証明書テンプレート**選択と**管理**します。

3. 証明書テンプレート コンソールで、右クリックして**RAS および IAS サーバー**、選択と**テンプレートの複製**します。

4. [新しいテンプレートのプロパティ] ダイアログ ボックスで、**全般**] タブの [**テンプレート表示名**、型**NPS サーバーの認証**。

5. **セキュリティ** タブで、次の手順を完了します。

    1. **[追加]** をクリックします。

    2. **[ユーザー、コンピューター、サービス アカウント、またはグループ**] ダイアログ ボックスに、入力**NPS サーバー**を選択し、 **OK**します。

    3. **グループまたはユーザー名**、 **NPS サーバー**します。

    4. **NPS サーバーのアクセス許可**を選択、**登録**と**自動登録**のチェック ボックス、**許可**列。

    5. **グループまたはユーザー名**、 **RAS and IAS Servers**を選択し、**削除**します。

6. 選択**OK** NPS サーバー証明書テンプレートを保存します。

7. 証明書テンプレート コンソールを閉じます。

8. 証明機関スナップインのナビゲーション ウィンドウで右**証明書テンプレート**を選択します**新規**選び**発行する証明書テンプレート**します。

9. 選択**NPS サーバーの認証**を選択し、 **OK**します。

10. 証明機関スナップインを閉じます。

## <a name="enroll-and-validate-the-user-certificate"></a>登録し、ユーザー証明書の検証

ユーザー証明書を自動登録するグループ ポリシーを使用しているため、ポリシーを更新する必要がありますのみと Windows 10 は、正しい証明書のユーザー アカウントを自動的に登録します。 証明書コンソールの証明書を検証できます。

**手順:**

1. メンバーとして、ドメインに参加しているクライアント コンピューターにサインイン、 **VPN ユーザー**グループ。

2. Windows キー + R、型を押して**gpupdate/force**、Enter キーを押します。

3. [スタート] メニューで、次のように入力します。 **certmgr.msc**、Enter キーを押します。

4. 証明書スナップインで、**個人**を選択します**証明書**します。 詳細ウィンドウで、証明書が表示されます。

5. 現在のドメイン ユーザー名を持つ証明書を右クリックし、**オープン**します。

6. **全般** タブで、日付が下に表示されることを確認します。**有効期間の開始**今日の日付。 いない場合は、誤った証明書を選択した可能性があります。

7. 選択**OK**、し、証明書スナップインを閉じます。

## <a name="enroll-and-validate-the-server-certificates"></a>登録して、サーバー証明書の検証

ユーザー証明書とは異なり、VPN サーバーの証明書を手動で登録する必要があります。 登録した後は、ユーザー証明書を使用して同じ処理を使用して検証します。 ユーザー証明書のように NPS サーバーでは、検証は行う必要があるすべての認証証明書が自動的に登録します。

>[!NOTE]
>次の手順を完了する前に、それらのグループ メンバーシップを更新できるように VPN と NPS サーバーを再起動する必要があります。

### <a name="enroll-and-validate-the-vpn-server-certificate"></a>登録して、VPN サーバーの証明書の検証

1. VPN サーバーの [スタート] メニューの次のように入力します。 **certlm.msc**、Enter キーを押します。

2. 右クリック**個人**を選択します**すべてのタスク**し、**新しい証明書の要求**証明書の登録ウィザードを起動します。

3. 開始する前に ページで、次のように選択します。**次**します。

4. 証明書登録ポリシーの選択 ページで、次のように選択します。**次**します。

5. 証明書の要求 ページで、それを選択する VPN サーバーの横にあるチェック ボックスを選択します。

6. VPN サーバー チェック ボックスの **詳細については、必要な**を証明書のプロパティ ダイアログ ボックスを開き、次の手順します。

    1. 選択、**サブジェクト** タブで **共通名** **サブジェクト名**で、**型**します。

    2. **サブジェクト名**の**値**、VPN、vpn.contoso.com に接続し、選択するために使用する外部ドメインのクライアントの名前を入力**追加**します。

    3. **別名**の**型**を選択します**DNS**します。

    4. **別名**で、**値**、すべてのクライアントなどの VPN に接続を使用してサーバー名、vpn.contoso.com、vpn、132.64.86.2 を入力します。

    5. 選択**追加**それぞれの名前を入力した後にします。

    6. 選択**OK**が完了します。

7. 選択**登録**します。

8. **[完了]** を選択します。

9. 証明書スナップインで、**個人**を選択します**証明書**します。
    
    詳細ウィンドウに表示されている証明書が表示されます。

10. VPN サーバーの名前、し、を含む証明書を右クリックして**オープン**します。

11. **全般** タブで、日付が下に表示されることを確認します。**有効期間の開始**今日の日付。 いない場合は、正しくない証明書を選択した可能性があります。

12. **詳細**] タブで [**拡張キー使用法**、ことを確認します**IP セキュリティ IKE 中間**と**サーバー認証**一覧に表示します。

13. 選択**OK**証明書を閉じます。

14. 証明書スナップインを閉じます。

### <a name="validate-the-nps-server-certificate"></a>NPS サーバー証明書を検証します。

1. NPS サーバーを再起動します。

2. NPS サーバーの [スタート] メニューの次のように入力します。 **certlm.msc**、Enter キーを押します。

3. 証明書スナップインで、**個人**を選択します**証明書**します。

    詳細ウィンドウに表示されている証明書が表示されます。

4. NPS サーバーの名前、し、を含む証明書を右クリックして**オープン**します。

5. **全般** タブで、日付が下に表示されることを確認します。**有効期間の開始**今日の日付。 いない場合は、正しくない証明書を選択した可能性があります。

6. 選択**OK**証明書を閉じます。

7. 証明書スナップインを閉じます。

## <a name="next-steps"></a>次のステップ

[手順 3.VPN でのリモート アクセス サーバーを常に構成](vpn-deploy-ras.md):この手順では、IKEv2 VPN 接続を許可する、その他の VPN プロトコルからの接続を拒否しの IP アドレスを発行するための静的 IP アドレス プールを割り当てる承認済みの VPN クライアントの接続のリモート アクセス VPN を構成します。
