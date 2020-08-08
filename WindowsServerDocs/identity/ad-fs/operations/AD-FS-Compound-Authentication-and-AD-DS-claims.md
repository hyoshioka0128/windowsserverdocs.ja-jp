---
title: Active Directory フェデレーションサービス (AD FS) における複合認証と Active Directory Domain Services 要求
description: 次のドキュメントでは、AD FS での複合認証と AD DS 要求について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.openlocfilehash: c0e2681498fdc86782bf418bfc90446bab0e0170
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940387"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>AD FS での複合認証と AD DS クレーム
Windows Server 2012 では、複合認証の導入によって Kerberos 認証が強化されています。  複合認証を使用すると、Kerberos チケット保証サービス (TGS) の要求に2つの id を含めることができます。

- ユーザーの id
- ユーザーのデバイスの id。

Windows[は、kerberos の柔軟な認証 (高速) または kerberos 防御](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11))を拡張することによって、複合認証を行います。

AD FS 2012 以降のバージョンでは、Kerberos 認証チケットに存在する AD DS 発行されたユーザーまたはデバイスの信頼性情報を使用できます。 以前のバージョンの AD FS では、要求エンジンは Kerberos からユーザーとグループのセキュリティ Id (Sid) のみを読み取ることができましたが、Kerberos チケット内に含まれる要求情報を読み取ることができませんでした。

Active Directory フェデレーションサービス (AD FS) (AD FS) を使用して、Active Directory Domain Services (AD DS) によって発行されたユーザーとデバイスの信頼性情報を使用することにより、フェデレーションアプリケーションの高度なアクセス制御を有効にすることができます。

## <a name="requirements"></a>要件
1.  フェデレーションアプリケーションにアクセスするコンピューターは、 **Windows 統合認証**を使用して AD FS に対して認証を行う必要があります。
    - Windows 統合認証は、バックエンド AD FS サーバーに接続する場合にのみ使用できます。
    - コンピューターがフェデレーションサービス名のバックエンド AD FS サーバーに接続できる必要がある
    - AD FS サーバーは、イントラネット設定で Windows 統合認証をプライマリ認証方法として提供する必要があります。

2.  複合認証によって保護されているフェデレーションアプリケーションにアクセスするすべてのコンピューターに、**信頼性情報の複合認証および kerberos 防御に対するポリシー Kerberos クライアントのサポート**が適用されている必要があります。 これは、フォレスト間またはフォレスト間のシナリオの場合に適用されます。

3.  AD FS サーバーをハウジングするドメインには、ドメインコントローラーに適用される [**要求の複合認証および Kerberos 防御をサポートするための KDC** ] ポリシー設定が必要です。

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS を構成する手順
複合認証と要求を構成するには、次の手順を使用します。

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1: 既定のドメインコントローラーポリシーで KDC による信頼性情報、複合認証、および Kerberos 防御のサポートを有効にする
1.  サーバーマネージャーで、[ツール]、[**グループポリシーの管理**] を選択します。
2.  **既定のドメインコントローラーポリシー**に移動し、右クリックして、[**編集**] を選択します。
![グループ ポリシー管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  **グループポリシー管理エディター**で、[**コンピューターの構成**] の [**ポリシー**] を展開し、[**管理用テンプレート**]、[**システム**] の順に展開して、[ **KDC**] を選択します。
4.  右側のウィンドウで、[KDC で**信頼性情報、複合認証、および Kerberos 防御をサポートする**] をダブルクリックします。
![グループ ポリシー管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  新しいダイアログウィンドウで、[KDC サポート] を [**有効**] に設定します。
6.  [オプション] で、ドロップダウンメニューから [**サポート**] を選択し、[**適用**] をクリックして、[ **OK]** をクリックします。
![グループ ポリシー管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2: フェデレーションアプリケーションにアクセスするコンピューターで Kerberos クライアントによる信頼性情報、複合認証、および Kerberos 防御のサポートを有効にする

1.  フェデレーションアプリケーションにアクセスするコンピューターに適用されているグループポリシーで、**グループポリシー管理エディター**の [**コンピューターの構成**] の下にある [**ポリシー**] を展開し、[**管理用テンプレート**]、[**システム**] の順に展開して、[ **Kerberos**] を選択します。
2.  [グループポリシー管理エディター] ウィンドウの右側のウィンドウで、[ **kerberos クライアントで信頼性情報、複合認証、および kerberos 防御をサポートする**] をダブルクリックします。
3.  新しいダイアログウィンドウで、[Kerberos クライアントサポート] を [**有効**] に設定し、[**適用**] と [ **OK]** をクリックします。
![グループ ポリシー管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>手順 3: AD FS サーバーが更新されていることを確認します。
AD FS サーバーに次の更新プログラムがインストールされていることを確認する必要があります。

|更新|説明|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|累積的なセキュリティ更新プログラム (KB2919355、KB2932046、KB2934018、KB2937592、KB2938439 を含む)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|サーバー 2012 R2 の更新|
|[修正プログラム3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|この更新プログラムは、Active Directory フェデレーションサービス (AD FS) で複合 ID 要求のサポートを追加します。|

### <a name="step-4-configure-the-primary-authentication-provider"></a>手順 4: プライマリ認証プロバイダーを構成する

1. イントラネット設定を AD FS には、プライマリ認証プロバイダーを [ **Windows 認証**] に設定します。
2. AD FS 管理] の [**認証ポリシー**] で、[**プライマリ認証**] を選択し、[**グローバル設定**] で [**編集**] をクリックします。
3. [**イントラネット**] の [**グローバル認証ポリシーの編集**] で、[ **Windows 認証**] を選択します。
4. [**適用**] をクリックし、[ **Ok]** をクリックします。

![グループ ポリシー管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. PowerShell を使用する場合は、 **AdfsGlobalAuthenticationPolicy**コマンドレットを使用できます。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID ベースのファームでは、プライマリ AD FS サーバーで PowerShell コマンドを実行する必要があります。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバーで PowerShell コマンドを実行できます。

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>手順 5: 要求の説明を AD FS に追加する
1. 次の要求の説明をファームに追加します。 この要求の説明は、既定では ADFS 2012 R2 に存在しないため、手動で追加する必要があります。
2. AD FS 管理] の [**サービス**] で、[**要求の説明**] を右クリックし、[**要求の説明の追加**] を選択します。
3. 要求の説明に次の情報を入力します。
   - 表示名: ' Windows デバイスグループ '
   - 要求の説明: ' <https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup> ' '
4. 両方のチェックボックスをオンにします。
5. **[OK]** をクリックします。

![要求の説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. PowerShell を使用する場合は、 **AdfsClaimDescription**コマンドレットを使用できます。
   ``` powershell
   Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
   -ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device'
   ```


>[!NOTE]
>WID ベースのファームでは、プライマリ AD FS サーバーで PowerShell コマンドを実行する必要があります。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバーで PowerShell コマンドを実行できます。

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 6: 型の SupportedEncryptionTypes 属性で複合認証ビットを有効にする

1.  **Set ADServiceAccount** PowerShell コマンドレットを使用して、AD FS サービスを実行するように指定したアカウントの [複合認証ビット] 属性の [複合認証ビット] を有効にします。

>[!NOTE]
>サービスアカウントを変更する場合は、 **compoundIdentitySupported: $true** Windows PowerShell コマンドレットを実行して、複合認証を手動で有効にする必要があります。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true
```
2. ADFS サービスを再起動します。

>[!NOTE]
>' CompoundIdentitySupported ' が true に設定されている場合、新しいサーバー (2012R2/2016) に同じ gMSA をインストールすると、次のエラーが発生します- **install-ADServiceAccount: service アカウントをインストールできません。エラーメッセージ: ' 指定されたコンテキストがターゲットと一致しませんでした。 '**。
>
>**解決方法**: 一時的に CompoundIdentitySupported を $false に設定します。 この手順により、ADFS は WindowsDeviceGroup 要求の発行を停止します。
Set ADServiceAccount-Identity ' ADFS Service Account '-CompoundIdentitySupported: $false 新しいサーバーに gMSA をインストールしてから、CompoundIdentitySupported を $True に戻します。
CompoundIdentitySupported を無効にしてから再度有効化する場合、ADFS サービスを再起動する必要はありません。

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>手順 7: Active Directory の AD FS 要求プロバイダー信頼を更新する

1. Active Directory の AD FS 要求プロバイダー信頼を更新して、' WindowsDeviceGroup ' 要求に対して次の ' パススルー ' 要求規則を含めます。
2.  **AD FS 管理**] で、 **[要求プロバイダー信頼**] をクリックし、右側のウィンドウで [ **Active Directory** ] をクリックして、[**要求規則の編集**] を選択します。
3.  [**アクティブなディレクターの要求規則の編集**] で [**規則の追加**] をクリックします。
4.  **変換要求規則の追加ウィザード**で、[**入力方向の要求をパススルーまたはフィルター処理する**] を選択し、[**次へ**] をクリックします。
5.  表示名を追加し、[入力**方向の要求の種類**] ドロップダウンから [ **Windows デバイスグループ**] を選択します。
6.  **[完了]** をクリックします。  [**適用**] をクリックし、[ **Ok]** をクリックします。
![要求の説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 8: "WindowsDeviceGroup" 要求がある証明書利用者には、同様の "パススルー" または "変換" 要求規則を追加します。
2. **AD FS 管理**] で、[**証明書利用者信頼**] をクリックし、右側のウィンドウで RP を右クリックして、[**要求規則の編集**] を選択します。
3. [**発行変換規則**] で、[**規則の追加**] をクリックします。
4. **変換要求規則の追加ウィザード**で、[**入力方向の要求をパススルーまたはフィルター処理する**] を選択し、[**次へ**] をクリックします。
5. 表示名を追加し、[入力**方向の要求の種類**] ドロップダウンから [ **Windows デバイスグループ**] を選択します。
6. **[完了]** をクリックします。  [**適用**] をクリックし、[ **Ok]** をクリックします。
   ![要求の説明](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


## <a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016 で AD FS を構成する手順
以下では、Windows Server 2016 の AD FS で複合認証を構成する手順について詳しく説明します。

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1: 既定のドメインコントローラーポリシーで KDC による信頼性情報、複合認証、および Kerberos 防御のサポートを有効にする
1.  サーバーマネージャーで、[ツール]、[**グループポリシーの管理**] を選択します。
2.  **既定のドメインコントローラーポリシー**に移動し、右クリックして、[**編集**] を選択します。
3.  **グループポリシー管理エディター**で、[**コンピューターの構成**] の [**ポリシー**] を展開し、[**管理用テンプレート**]、[**システム**] の順に展開して、[ **KDC**] を選択します。
4.  右側のウィンドウで、[KDC で**信頼性情報、複合認証、および Kerberos 防御をサポートする**] をダブルクリックします。
5.  新しいダイアログウィンドウで、[KDC サポート] を [**有効**] に設定します。
6.  [オプション] で、ドロップダウンメニューから [**サポート**] を選択し、[**適用**] をクリックして、[ **OK]** をクリックします。


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2: フェデレーションアプリケーションにアクセスするコンピューターで Kerberos クライアントによる信頼性情報、複合認証、および Kerberos 防御のサポートを有効にする

1.  フェデレーションアプリケーションにアクセスするコンピューターに適用されているグループポリシーで、**グループポリシー管理エディター**の [**コンピューターの構成**] の下にある [**ポリシー**] を展開し、[**管理用テンプレート**]、[**システム**] の順に展開して、[ **Kerberos**] を選択します。
2.  [グループポリシー管理エディター] ウィンドウの右側のウィンドウで、[ **kerberos クライアントで信頼性情報、複合認証、および kerberos 防御をサポートする**] をダブルクリックします。
3.  新しいダイアログウィンドウで、[Kerberos クライアントサポート] を [**有効**] に設定し、[**適用**] と [ **OK]** をクリックします。
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-configure-the-primary-authentication-provider"></a>手順 3: プライマリ認証プロバイダーを構成する

1. イントラネット設定を AD FS には、プライマリ認証プロバイダーを [ **Windows 認証**] に設定します。
2. AD FS 管理] の [**認証ポリシー**] で、[**プライマリ認証**] を選択し、[**グローバル設定**] で [**編集**] をクリックします。
3. [**イントラネット**] の [**グローバル認証ポリシーの編集**] で、[ **Windows 認証**] を選択します。
4. [**適用**] をクリックし、[ **Ok]** をクリックします。
5. PowerShell を使用する場合は、 **AdfsGlobalAuthenticationPolicy**コマンドレットを使用できます。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID ベースのファームでは、プライマリ AD FS サーバーで PowerShell コマンドを実行する必要があります。
>SQL ベースのファームでは、ファームのメンバーである任意の AD FS サーバーで PowerShell コマンドを実行できます。

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 4: 型の SupportedEncryptionTypes 属性で複合認証ビットを有効にする

1.  **Set ADServiceAccount** PowerShell コマンドレットを使用して、AD FS サービスを実行するように指定したアカウントの [複合認証ビット] 属性の [複合認証ビット] を有効にします。

>[!NOTE]
>サービスアカウントを変更する場合は、 **compoundIdentitySupported: $true** Windows PowerShell コマンドレットを実行して、複合認証を手動で有効にする必要があります。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true
```
2. ADFS サービスを再起動します。

>[!NOTE]
>' CompoundIdentitySupported ' が true に設定されている場合、新しいサーバー (2012R2/2016) に同じ gMSA をインストールすると、次のエラーが発生します- **install-ADServiceAccount: service アカウントをインストールできません。エラーメッセージ: ' 指定されたコンテキストがターゲットと一致しませんでした。 '**。
>
>**解決方法**: 一時的に CompoundIdentitySupported を $false に設定します。 この手順により、ADFS は WindowsDeviceGroup 要求の発行を停止します。
Set ADServiceAccount-Identity ' ADFS Service Account '-CompoundIdentitySupported: $false 新しいサーバーに gMSA をインストールしてから、CompoundIdentitySupported を $True に戻します。
CompoundIdentitySupported を無効にしてから再度有効化する場合、ADFS サービスを再起動する必要はありません。

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>手順 5: Active Directory の AD FS 要求プロバイダー信頼を更新する

1. Active Directory の AD FS 要求プロバイダー信頼を更新して、' WindowsDeviceGroup ' 要求に対して次の ' パススルー ' 要求規則を含めます。
2.  **AD FS 管理**] で、 **[要求プロバイダー信頼**] をクリックし、右側のウィンドウで [ **Active Directory** ] をクリックして、[**要求規則の編集**] を選択します。
3.  [**アクティブなディレクターの要求規則の編集**] で [**規則の追加**] をクリックします。
4.  **変換要求規則の追加ウィザード**で、[**入力方向の要求をパススルーまたはフィルター処理する**] を選択し、[**次へ**] をクリックします。
5.  表示名を追加し、[入力**方向の要求の種類**] ドロップダウンから [ **Windows デバイスグループ**] を選択します。
6.  **[完了]** をクリックします。  [**適用**] をクリックし、[ **Ok]** をクリックします。


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 6: ' WindowsDeviceGroup ' 要求がある証明書利用者には、同様の "パススルー" または "変換" 要求規則を追加します。
2. **AD FS 管理**] で、[**証明書利用者信頼**] をクリックし、右側のウィンドウで RP を右クリックして、[**要求規則の編集**] を選択します。
3. [**発行変換規則**] で、[**規則の追加**] をクリックします。
4. **変換要求規則の追加ウィザード**で、[**入力方向の要求をパススルーまたはフィルター処理する**] を選択し、[**次へ**] をクリックします。
5. 表示名を追加し、[入力**方向の要求の種類**] ドロップダウンから [ **Windows デバイスグループ**] を選択します。
6. **[完了]** をクリックします。  [**適用**] をクリックし、[ **Ok]** をクリックします。

## <a name="validation"></a>検証
"WindowsDeviceGroup" 要求のリリースを検証するには、.Net 4.6 を使用してテスト要求対応アプリケーションを作成します。 WIF SDK 4.0 を使用します。
ADFS で証明書利用者としてアプリケーションを構成し、前述の手順で指定したとおりに要求規則で更新します。
Windows 統合認証プロバイダーの ADFS を使用してアプリケーションを認証する場合、次の要求がキャストされます。
![検証](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

コンピューターまたはデバイスの信頼性情報を使用して、より豊富なアクセス制御を行うことができるようになりました。

たとえば、次の**Additionalauthenticationrules**は、認証を行うユーザーがセキュリティグループ "-1-5-21-2134745077-1211275016-3050530490-1117" のメンバーではなく、コンピューター (ユーザーが認証を行っている場所) がセキュリティグループ "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)" のメンバーではない場合に、MFA を呼び出すように AD FS に指示します。

ただし、上記の条件のいずれかが満たされている場合は、MFA を呼び出さないでください。

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
