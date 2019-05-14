---
title: 複合 Active Directory フェデレーション サービスで認証と Active Directory Domain Services の要求
description: 次のドキュメントでは、複合認証、および AD FS での AD DS 信頼性情報について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 270fb6efd63e6355c410ee45d09e6fd16b14222b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867993"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>AD FS での複合認証と AD DS クレーム
Windows Server 2012 では、複合認証を導入することで Kerberos 認証を強化します。  複合認証を使用すると、Kerberos チケット保証サービス (TGS) 要求を 2 つの id が含まれます。 

- ユーザーの id
- ユーザーのデバイスの id。  

Windows で複合認証を行う拡張を[Kerberos フレキシブル認証セキュア トンネリング (FAST)、または Kerberos 防御](https://technet.microsoft.com/library/hh831747.aspx)します。 

AD FS 2012 およびそれ以降のバージョンは、AD DS を Kerberos 認証チケット内に存在するユーザーまたはデバイスの要求を発行の消費量を使用できます。 AD FS の以前のバージョンでは、要求エンジンは、Kerberos からユーザーとグループのセキュリティ Id (Sid) を読み取る可能性がありますのみが、いずれかを読み取ることができませんでしたは Kerberos チケット内に含まれる情報を要求します。

Active Directory Domain Services (AD DS) を使用してフェデレーション アプリケーションの高度なアクセス制御を有効にすることができます-Active Directory フェデレーション サービス (AD FS) を同時に、ユーザーとデバイスの要求を発行します。

## <a name="requirements"></a>必要条件
1.  AD FS を使用するフェデレーション アプリケーションへのアクセス、コンピューターを認証する必要があります**Windows 統合認証**します。 
    - Windows 統合認証は、バックエンドの AD FS サーバーに接続するときにのみ使用できます。
    - コンピューターは、フェデレーション サービス名、バックエンドの AD FS サーバーに到達できる必要があります。
    - AD FS サーバーは、そのイントラネット設定でプライマリ認証方法として Windows 統合認証を提供する必要があります。

2.  ポリシー**クレーム複合認証および Kerberos 防御の Kerberos クライアント サポート**複合認証によって保護されているフェデレーション アプリケーションにアクセスするすべてのコンピューターに適用する必要があります。 これは、1 つのフォレストが発生した場合、またはクロス フォレストのシナリオに適用します。

3.  ドメインの AD FS サーバーを格納している必要があります、**要求は複合認証、および Kerberos 防御 KDC のサポート**ポリシー設定がドメイン コント ローラーに適用します。

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS を構成する手順
次の手順を使用して、複合認証、およびクレームを構成します。 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1:KDC 信頼性情報、複合認証、および既定のドメイン コント ローラー ポリシーでの Kerberos 防御をサポートを有効にします。
1.  サーバー マネージャーで、選択ツール、 **Group Policy Management**します。
2.  下に移動し、**既定のドメイン コント ローラー ポリシー**を右クリックし、**編集**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  **グループ ポリシー管理エディター** **コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、選び**KDC**します。
4.  右側のウィンドウでダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  新しいダイアログ ウィンドウにセットの要求を KDC サポート**有効**します。
6.  [オプション] の選択**サポートされている**クリックしてドロップダウン メニューから**適用**と**OK**。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2:信頼性情報、複合認証、およびフェデレーション アプリケーションにアクセスするコンピューターでの Kerberos 防御の Kerberos クライアント サポートを有効にします。

1.  フェデレーションのアプリケーションにアクセスするコンピューターに適用されるグループ ポリシーで、**グループ ポリシー管理エディター****コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、選び**Kerberos**します。
2.  グループ ポリシー管理エディター ウィンドウの右側のウィンドウでダブルクリック**信頼性情報、複合認証、および Kerberos 防御の Kerberos クライアント サポートします。**
3.  新しいダイアログ ウィンドウに Kerberos クライアント サポートを設定**有効** をクリック**適用**と**OK**。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>手順 3:AD FS サーバーが更新されたことを確認します。
次の更新プログラムが、AD FS サーバーにインストールされていることを確認する必要があります。

|更新|説明|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|(、KB2919355、KB2932046、KB2934018、KB2937592 KB2938439 を含む) の累積的なセキュリティ更新プログラム|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Server 2012 R2 の更新|
|[修正プログラム 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|この更新プログラムは、Active Directory フェデレーション サービスで、複合 ID のクレームのサポートを追加します。|

### <a name="step-4-configure-the-primary-authentication-provider"></a>手順 4:プライマリ認証プロバイダーを構成します。

1. プライマリ認証プロバイダーを設定**Windows 認証**for AD FS のイントラネット設定します。
2. AD FS の管理 [**認証ポリシー**を選択します**プライマリ認証** **グローバル設定**] をクリックして**編集**します。
3. **グローバル認証ポリシーの編集** **イントラネット**選択**Windows 認証**します。
4. クリックして**適用**と**Ok**します。

![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. PowerShell を使用することができますを使用して、**セット AdfsGlobalAuthenticationPolicy**コマンドレット。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID でファーム、プライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell に基づいています。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバー上の PowerShell コマンドを実行できます。

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>手順 5:AD fs のクレームの説明を追加します。
1.  ファームには、次のクレームの説明を追加します。 このクレームの説明が ADFS 2012 R2 では、既定で存在しないと、手動で追加する必要があります。
2.  AD FS の管理 **サービス**を右クリックして**請求の説明**選択と**追加請求の説明**
3.  クレームの説明で、次の情報を入力します。
    - 表示名:' Windows デバイスのグループ ' 
    - クレームの説明: 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' '
4. 両方のボックスに、チェックを配置します。
5. **[OK]** をクリックします。

![クレームの説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. PowerShell を使用することができますを使用して、**追加 AdfsClaimDescription**コマンドレット。
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>WID でファーム、プライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell に基づいています。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバー上の PowerShell コマンドを実行できます。

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 6:Msds-supportedencryptiontypes 属性に複合認証のビットを有効にします。

1.  ビットを使用する AD FS サービスを実行するように指定するアカウントの Msds-supportedencryptiontypes 属性に複合認証を有効にする、 **Set-adserviceaccount** PowerShell コマンドレット。  

>[!NOTE]
>サービス アカウントを変更するかどうかは、実行して複合認証を有効にする必要があります手動で、 **Set-aduser compoundIdentitySupported: $true** Windows PowerShell コマンドレット。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS サービスを再起動します。

>[!NOTE]
>新しいサーバー (2012R2/2016) 障害が発生した次のエラー – 同じ gMSA の true の場合、インストールに設定すると、'CompoundIdentitySupported' **Install-adserviceaccount:サービス アカウントをインストールすることはできません。エラー メッセージ :' 指定されたコンテキストが一致しません、ターゲット。 '**.
>
>**解決方法**:一時的に CompoundIdentitySupported を $false に設定します。 この手順では ADFS WindowsDeviceGroup 要求の発行を停止します。 Set-adserviceaccount-Identity 'ADFS サービス アカウント' - CompoundIdentitySupported: $false が、新しいサーバーで、gMSA をインストールし、CompoundIdentitySupported を $True に有効にします。
CompoundIdentitySupported を無効にして、再有効化は、ADFS サービスの再起動は必要ありません。

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>手順 7:Active Directory の更新、AD FS の要求プロバイダー信頼

1. AD FS の要求プロバイダー信頼の 'WindowsDeviceGroup' 要求の次の 'パススルー' の要求規則を含めるように Active Directory を更新します。
2.  **AD FS 管理**、 をクリックして**要求プロバイダー信頼**と右側のウィンドウで右クリックして**Active Directory**選択**要求規則の編集**.
3.  **Active Director の要求規則の編集**クリックして**規則の追加**します。
4.  **変換要求規則追加ウィザード**選択**パススルーまたはフィルター処理の入力方向の要求** をクリック**次**。
5.  表示名を追加し、選択**Windows デバイスのグループ**から、**着信要求の種類**ドロップダウンします。
6.  **[Finish]**(完了) をクリックします。  クリックして**適用**と**Ok**します。 
![クレームの説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 8:'WindowsDeviceGroup' 要求が予想される証明書利用者のパーティでは、'パススルー' または '変換' のような要求規則を追加します。
2.  **AD FS 管理**、 をクリックして**証明書利用者信頼**と右側のウィンドウで右クリックして、RP と選択**要求規則の編集**します。
3.  **発行変換規則**クリックして**規則の追加**します。
4.  **変換要求規則追加ウィザード**選択 **パススルーまたはフィルター処理の入力方向の要求** をクリック**次**。
5.  表示名を追加し、選択**Windows デバイスのグループ**から、**着信要求の種類**ドロップダウンします。
6.  **[Finish]**(完了) をクリックします。  クリックして**適用**と**Ok**します。
![クレームの説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016 で AD FS を構成する手順
次は、Windows Server 2016 の AD FS で複合認証を構成する手順について説明します。

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1:KDC 信頼性情報、複合認証、および既定のドメイン コント ローラー ポリシーでの Kerberos 防御をサポートを有効にします。
1.  サーバー マネージャーで、選択ツール、 **Group Policy Management**します。
2.  下に移動し、**既定のドメイン コント ローラー ポリシー**を右クリックし、**編集**します。
3.  **グループ ポリシー管理エディター** **コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、選び**KDC**します。
4.  右側のウィンドウでダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**します。
5.  新しいダイアログ ウィンドウにセットの要求を KDC サポート**有効**します。
6.  [オプション] の選択**サポートされている**クリックしてドロップダウン メニューから**適用**と**OK**。


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2:信頼性情報、複合認証、およびフェデレーション アプリケーションにアクセスするコンピューターでの Kerberos 防御の Kerberos クライアント サポートを有効にします。

1.  フェデレーションのアプリケーションにアクセスするコンピューターに適用されるグループ ポリシーで、**グループ ポリシー管理エディター** **コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、選び**Kerberos**します。
2.  グループ ポリシー管理エディター ウィンドウの右側のウィンドウでダブルクリック**信頼性情報、複合認証、および Kerberos 防御の Kerberos クライアント サポートします。**
3.  新しいダイアログ ウィンドウに Kerberos クライアント サポートを設定**有効** をクリック**適用**と**OK**。
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-configure-the-primary-authentication-provider"></a>手順 3:プライマリ認証プロバイダーを構成します。

1. プライマリ認証プロバイダーを設定**Windows 認証**for AD FS のイントラネット設定します。
2. AD FS の管理 [**認証ポリシー**を選択します**プライマリ認証** **グローバル設定**] をクリックして**編集**します。
3. **グローバル認証ポリシーの編集** **イントラネット**選択**Windows 認証**します。
4. クリックして**適用**と**Ok**します。
5. PowerShell を使用することができますを使用して、**セット AdfsGlobalAuthenticationPolicy**コマンドレット。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID でファーム、プライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell に基づいています。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバー上の PowerShell コマンドを実行できます。

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 4:Msds-supportedencryptiontypes 属性に複合認証のビットを有効にします。

1.  ビットを使用する AD FS サービスを実行するように指定するアカウントの Msds-supportedencryptiontypes 属性に複合認証を有効にする、 **Set-adserviceaccount** PowerShell コマンドレット。  

>[!NOTE]
>サービス アカウントを変更するかどうかは、実行して複合認証を有効にする必要があります手動で、 **Set-aduser compoundIdentitySupported: $true** Windows PowerShell コマンドレット。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS サービスを再起動します。

>[!NOTE]
>新しいサーバー (2012R2/2016) 障害が発生した次のエラー – 同じ gMSA の true の場合、インストールに設定すると、'CompoundIdentitySupported' **Install-adserviceaccount:サービス アカウントをインストールすることはできません。エラー メッセージ :' 指定されたコンテキストが一致しません、ターゲット。 '**.
>
>**解決方法**:一時的に CompoundIdentitySupported を $false に設定します。 この手順では ADFS WindowsDeviceGroup 要求の発行を停止します。 Set-adserviceaccount-Identity 'ADFS サービス アカウント' - CompoundIdentitySupported: $false が、新しいサーバーで、gMSA をインストールし、CompoundIdentitySupported を $True に有効にします。
CompoundIdentitySupported を無効にして、再有効化は、ADFS サービスの再起動は必要ありません。

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>手順 5:Active Directory の更新、AD FS の要求プロバイダー信頼

1. AD FS の要求プロバイダー信頼の 'WindowsDeviceGroup' 要求の次の 'パススルー' の要求規則を含めるように Active Directory を更新します。
2.  **AD FS 管理**、 をクリックして**要求プロバイダー信頼**と右側のウィンドウで右クリックして**Active Directory**選択**要求規則の編集**.
3.  **Active Director の要求規則の編集**クリックして**規則の追加**します。
4.  **変換要求規則追加ウィザード**選択 **パススルーまたはフィルター処理の入力方向の要求** をクリック**次**。
5.  表示名を追加し、選択**Windows デバイスのグループ**から、**着信要求の種類**ドロップダウンします。
6.  **[Finish]**(完了) をクリックします。  クリックして**適用**と**Ok**します。 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 6:'WindowsDeviceGroup' 要求が予想される証明書利用者のパーティでは、'パススルー' または '変換' のような要求規則を追加します。
2.  **AD FS 管理**、 をクリックして**証明書利用者信頼**と右側のウィンドウで右クリックして、RP と選択**要求規則の編集**します。
3.  **発行変換規則**クリックして**規則の追加**します。
4.  **変換要求規則追加ウィザード**選択 **パススルーまたはフィルター処理の入力方向の要求** をクリック**次**。
5.  表示名を追加し、選択**Windows デバイスのグループ**から、**着信要求の種類**ドロップダウンします。
6.  **[Finish]**(完了) をクリックします。  クリックして**適用**と**Ok**します。

## <a name="validation"></a>［確認］
'WindowsDeviceGroup' 要求のリリースを検証、テストを作成するには、.Net 4.6 を使用して対応するアプリケーションを要求します。 WIF sdk 4.0。
ADFS で証明書利用者としてアプリケーションを構成し、上記の手順で指定されている要求規則を使って更新します。
ADFS の Windows 統合認証プロバイダーを使用してアプリケーションに、認証時に次の要求はキャストします。
![検証](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

コンピューター/デバイスの信頼性情報は、多数のアクセス制御のようになりました使用可能性があります。

たとえば – 次**AdditionalAuthenticationRules** – 認証ユーザーは、セキュリティ グループのメンバーではない場合、MFA を呼び出すための AD FS の通知"-1-5-21-2134745077-1211275016-3050530490-1117"とコンピューター (場所は、認証をユーザーには)"S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)"のセキュリティ グループのメンバーではありません

ただし、上記の条件のいずれかが満たされた場合は MFA 呼び出されません。

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
