---
title: AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開 - 手順 2、AD FS の構成後の作業
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 06/06/2019
ms.assetid: 0a48852e-48cc-4047-ae58-99f11c273942
ms.openlocfilehash: 84ff335514b4b9251ffa1518b613120f3b3e2869
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946195"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-2-ad-fs-post-configuration-work"></a>AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 2、AD FS の構成後の作業

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシを使用して、ワーク フォルダーを展開する 2 番目の手順について説明します。 このプロセスの他の手順は、次のトピックで確認できます。

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 概要](deploy-work-folders-adfs-overview.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 1: AD FS のセットアップ](deploy-work-folders-adfs-step1.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 3: ワーク フォルダーのセットアップ](deploy-work-folders-adfs-step3.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 4: Web アプリケーション プロキシのセットアップ](deploy-work-folders-adfs-step4.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 5: クライアントのセットアップ](deploy-work-folders-adfs-step5.md)

> [!NOTE]
> このセクションで説明する手順は、Windows Server 2019 または Windows Server 2016 環境向けです。 Windows Server 2012 R2 を使用している場合には、[Windows Server 2012 R2 の手順](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)) に従います。

手順 1 では、AD FS のインストールと構成を行いました。 次に、AD FS の構成に続いて、次の手順を実行する必要があります。

## <a name="configure-dns-entries"></a>DNS エントリの構成

AD FS のために DNS エントリを 2 つ作成する必要があります。 これらは、インストール前の手順で、サブジェクト代替名 (SAN) の証明書を作成するときに使用されていたものと同じ 2 つのエントリです。

DNS エントリの形式は次のとおりです。

-   AD FS サービス名.ドメイン

-   enterpriseregistration.ドメイン

-   AD FS サーバー名.ドメイン   (DNS エントリが既に存在しているはずです。 たとえば 2016-ADFS.contoso.com)

テストの例では、値は以下のようになります。

-   **blueadfs.contoso.com**

-   **enterpriseregistration.contoso.com**

## <a name="create-the-a-and-cname-records-for-ad-fs"></a>AD FS の A レコードと CNAME レコードの作成

AD FS の A レコードと CNAME レコードを作成するには、次の手順を実行します。

1.  ドメイン コントローラーで、[DNS マネージャー] を開きます。

2.  [前方参照ゾーン] フォルダーを展開し、ドメインで右クリックして、**[新しいホスト (A)]** を選択します。

3.  **[新しいホスト]** ウィンドウが開きます。 **[名前]** フィールドに、AD FS サービス名のエイリアスを入力します。 このテストの例では、「**blueadfs**」とします。

    エイリアスは、AD FS で使用した証明書のサブジェクトと同じである必要があります。 たとえば、サブジェクトが adfs.contoso.com であった場合、ここで入力するエイリアスは「**adfs**」となります。

    > [!IMPORTANT]
    > Windows PowerShell ではなく、Windows Server のユーザー インターフェイス (UI) を使用して、AD FS をセットアップする場合には、AD FS の CNAME レコードではなく A レコードを作成する必要があります。 これは、UI を使って作成されたサービス プリンシパル名 (SPN) には、ホストとしての AD FS サービスをセットアップするために使用されたエイリアスのみが含まれているためです。

4.  **[IP アドレス]** で、AD FS サーバーの IP アドレスを入力します。 このテストの例では、「**192.168.0.160**」とします。 **[ホストの追加]** をクリックします。

5.  [前方参照ゾーン] フォルダーで、再度ドメインで右クリックし、**[新しいエイリアス (CNAME)]** を選択します。

6.  **[新しいリソース レコード]** ウィンドウで、エイリアス名「**enterpriseregistration**」を追加し、AD FS サーバーの FQDN を入力します。 このエイリアスはデバイスの参加に使用され、**enterpriseregistration** が呼び出される必要があります。

7.  **[OK]** をクリックします。

Windows PowerShell で同等の手順を実行するには、次のコマンドを使用します。 コマンドは、ドメイン コントローラーで実行する必要があります。

```Powershell
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name blueadfs -A -IPv4Address 192.168.0.160
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name enterpriseregistration -CName  -HostNameAlias 2016-ADFS.contoso.com
```

## <a name="set-up-the-ad-fs-relying-party-trust-for-work-folders"></a>ワーク フォルダーのための AD FS の証明書利用者信頼のセットアップ

ワーク フォルダーをセットアップする前でも、ワーク フォルダーの証明書利用者信頼をセットアップして構成できます。 AD FS を使ってワーク フォルダーを有効にするには、証明書利用者信頼を設定する必要があります。 ここでは AD FS をセットアップしているので、このタイミングで証明書利用者信頼をセットアップすると、作業をスムーズに行うことができます。

証明書利用者信頼をセットアップするには:

1.  **[サーバー マネージャー]** を開き、**[ツール]** メニューで **[AD FS管理]** を選択します。

2.  右側のウィンドウで、**[アクション]** の **[証明書利用者信頼の追加]** をクリックします。

3.  **[ようこそ]** ページで、**[要求に対応する]** を選択し、**[開始]** をクリックします。

4.  [**データ ソースの選択**] ページで、[**証明書利用者についてのデータを手動で入力する**] を選択し、[**次へ**] をクリックします。

5.  **[表示名]** フィールドで、「**WorkFolders**」と入力して、**[次へ]** をクリックします。

6.  **[証明書の構成]** ページで、**[次へ]** をクリックします。 トークン暗号化証明書はオプションです。テスト構成には必要ありません。

7.  **[URL の構成]** ページで、**[次へ]** をクリックします。

8. [**識別子の構成**] ページで、次の識別子を追加します `https://windows-server-work-folders/V1` 。 この識別子はワーク フォルダーで使われるハードコード値であり、AD FS を使って通信するときに、ワーク フォルダー サービスによって送信されます。 **[次へ]** をクリックします。

9. [アクセス制御ポリシーの選択] ページで、**[すべてのユーザーを許可]** を選択し、**[次へ]** をクリックします。

10. **[信頼の追加の準備完了]** ページで、**[次へ]** をクリックします。

11. 構成が完了すると、ウィザードの最後のページで構成が成功したことが表示されます。 要求規則の編集のチェックボックスを選択し、**[閉じる]** をクリックします。

12. AD FS スナップインで、**WorkFolders** の証明書利用者信頼を選択し、[アクション] の **[要求発行ポリシーの編集]** をクリックします。

13. **[WorkFolders の要求発行ポリシーの編集]** ウィンドウが開きます。 [**ルールの追加**] をクリックします。

14. **[要求規則テンプレート]** ドロップダウン リストで、**[LDAP 属性を要求として送信]** を選択して、**[次へ]** をクリックします。

15. **[要求規則の構成]** ページで、**[要求規則名]** フィールドに「**WorkFolders**」と入力します。

16. **[属性ストア]** ドロップダウン リストで、「**Active Directory**」を選択します。

17. マッピング テーブルに、次の値を入力します。

    -   ユーザー プリンシパル名: UPN

    -   表示名: 名前

    -   姓: 姓

    -   名: 名

18. **[完了]** をクリックします。 [発行変換規則] タブに WorkFolders 規則が表示されます。**[OK]** をクリックします。

### <a name="set-relying-part-trust-options"></a>証明書利用者信頼のオプションの設定

AD FS の証明書利用者信頼をセットアップした後で、Windows PowerShell で 5 つのコマンドを実行して構成を完了する必要があります。 これらのコマンドは、ワーク フォルダーが AD FS と正常に通信を行うために必要なオプションで、UI から設定できないオプションを設定します。 オプションは次のとおりです。

-   JSON Web トークン (JWT) の使用を有効にする

-   暗号化された要求を無効にする

-   自動更新を有効にする \-

-   OAuth 更新トークンの発行をすべてのデバイスに設定する

-   証明書利用者信頼へのクライアント アクセスを許可する

これらのオプションを設定するには、次のコマンドを使用します。

```powershell
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -EnableJWT $true
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -Encryptclaims $false
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -AutoupdateEnabled $true
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -IssueOAuthRefreshTokensTo AllDevices
Grant-AdfsApplicationPermission -ServerRoleIdentifier "https://windows-server-work-folders/V1" -AllowAllRegisteredClients -ScopeNames openid,profile
```

## <a name="enable-workplace-join"></a>Workplace Join を有効にする

Workplace Join の有効化はオプションですが、ユーザーが個人のデバイスを使用して職場のリソースにアクセスできるようにするために役立ちます。

デバイスの Workplace Join への登録を有効化するには、次の Windows PowerShell コマンドを実行して、デバイスの登録を構成し、グローバル認証ポリシーを設定する必要があります。

```powershell
Initialize-ADDeviceRegistration -ServiceAccountName <your AD FS service account>
    Example: Initialize-ADDeviceRegistration -ServiceAccountName contoso\adfsservice$
Set-ADFSGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true
```

## <a name="export-the-ad-fs-certificate"></a>AD FS 証明書のエクスポート

次に、自己署名 AD FS 証明書をエクスポートして、 \- テスト環境の次のコンピューターにインストールできるようにします。

-   ワーク フォルダー用に使われるサーバー

-   Web アプリケーション プロキシに使用するサーバー

-   ドメインに参加している Windows クライアント

-   ドメインに参加していない Windows クライアント

証明書をエクスポートするには、以下の手順を実行します。

1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

2.  「**MMC**」と入力します。

3.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。

4.  [**利用できるスナップイン**] の一覧で、[**証明書**]、[**追加**] の順に選択します。 証明書スナップイン ウィザードが開始されます。

5.  **[コンピューター アカウント]** を選択し、**[次へ]** をクリックします。

6.  **[ローカル コンピュータ (このコンソールを実行しているコンピュータ)]** を選択し、次に **[完了]** をクリックします。

7.  **[OK]** をクリックします。

8.  フォルダー**コンソール Root\Certificates \( Local Computer) \Personal\Certificates**を展開します。

9.  **[AD FS 証明書]** を右クリックし、**[すべてのタスク]**、**[エクスポート]** の順にクリックします。

10. 証明書のエクスポート ウィザードが開きます。 **[はい、秘密キーをエクスポートします]** を選択します。

11. **[エクスポートファイルの形式]** ページでは、既定のオプションを選択して、**[次へ]** をクリックします。

12. 証明書のパスワードを作成します。 これは、後で他のデバイスに証明書をインポートするときに使用するパスワードです。 **[次へ]** をクリックします。

13. 場所と証明書の名前を入力して、**[完了]** をクリックします。

証明書のインストールについては、展開の手順の後半で説明します。

## <a name="manage-the-private-key-setting"></a>秘密キーの設定の管理

AD FS サービス アカウントに、新しい証明書の秘密キーにアクセスするためのアクセス許可を与える必要があります。 通信証明書の期限が切れた後に通信証明書を交換するときには、再度このアクセス許可を付与する必要があります。 アクセス許可を付与するには、次の手順に従います。

1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

2.  「**MMC**」と入力します。

3.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。

4.  [**利用できるスナップイン**] の一覧で、[**証明書**]、[**追加**] の順に選択します。 証明書スナップイン ウィザードが開始されます。

5.  **[コンピューター アカウント]** を選択し、**[次へ]** をクリックします。

6.  **[ローカル コンピュータ (このコンソールを実行しているコンピュータ)]** を選択し、次に **[完了]** をクリックします。

7.  **[OK]** をクリックします。

8.  フォルダー**コンソール Root\Certificates \( Local Computer) \Personal\Certificates**を展開します。

9.  **[AD FS 証明書]** を右クリックし、**[すべてのタスク]** をクリックして、**[秘密キーの管理]** をクリックします。

10. **[アクセス許可]** ウィンドウで、**[追加]** をクリックします。

11. **[オブジェクトの種類]** ウィンドウで、**[サービス アカウント]** を選択し、**[OK]** をクリックします。

12. AD FS を実行しているアカウント名を入力します。 このテストの例では、「ADFSService」です。 **[OK]** をクリックします。

13. **[アクセス許可]** ウィンドウで、少なくとも読み取りアクセス許可をアカウントに付与して、**[OK]** をクリックします。

秘密キーを管理するオプションがない場合は、次のコマンドの実行が必要になることがあります。`certutil -repairstore my *`

## <a name="verify-that-ad-fs-is-operational"></a>AD FS が動作していることを確認する

AD FS が動作していることを確認するには、ブラウザーウィンドウを開き、にアクセスして `https://blueadfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` 、使用している環境に合わせて URL を変更します。

ブラウザー ウィンドウには、フェデレーション サーバーのメタデータが書式設定なしで表示されます。 SSL のエラーや警告なしでデータが表示された場合、フェデレーション サーバーは動作しています。

次の手順: [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 3: ワーク フォルダーのセットアップ](deploy-work-folders-adfs-step3.md)

## <a name="see-also"></a>参照
[ワーク フォルダーの概要](Work-Folders-Overview.md)
