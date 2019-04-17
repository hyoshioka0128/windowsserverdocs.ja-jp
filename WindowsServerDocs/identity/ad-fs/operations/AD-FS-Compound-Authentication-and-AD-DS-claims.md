---
title: "Active Directory フェデレーション サービスの認証および Active Directory ドメイン サービスの要求に応じて複合します。"
description: "次のドキュメントでは、複合認証、および AD FS での AD DS 信頼性情報について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5f80cbcbdb2deca9b098014627365b8ea819b5f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>複合認証、および AD FS での AD DS 信頼性情報
Windows Server 2012 では、複合認証を導入することで Kerberos 認証を強化します。  複合認証は、2 つの ID を含める Kerberos チケット保証サービス (TGS) 要求を有効にします。 

- ユーザーの id
- ユーザーのデバイスの id。  

Windows での拡張を複合認証を行う[Kerberos フレキシブル認証セキュア トンネリング (FAST)、または Kerberos 防御](https://technet.microsoft.com/library/hh831747.aspx)します。 

AD FS 2012 およびそれ以降のバージョンは、AD DS を Kerberos 認証チケット内に存在するユーザーまたはデバイスの信頼性情報の発行の消費量をできます。 AD FS の以前のバージョンでは、要求エンジンは、Kerberos からユーザーとグループのセキュリティ ID (Sid) を読み取る可能性がありますのみが、すべてを読み取ることができませんでしたは、Kerberos チケットに含まれる情報を要求します。

Active Directory ドメイン サービス (AD DS) を使用してフェデレーション アプリケーションの高度なアクセス制御を有効にすることができます、Active Directory フェデレーション サービス (AD FS) と同時に、ユーザーとデバイスの信頼性情報を発行します。

## <a name="requirements"></a>要件
1.  AD FS を使用する、フェデレーション アプリケーションにアクセスするコンピューターを認証する必要があります**Windows 統合認証**します。 
    - Windows 統合認証を利用可能なは、バックエンドの AD FS サーバーに接続している場合だけです。
    - コンピューターがフェデレーション サービス名のバックエンド AD FS サーバーに到達できる必要があります。
    - AD FS サーバーのイントラネット設定でプライマリ認証方法として Windows 統合認証を提供する必要があります。

2.  ポリシー**クレーム複合認証、および Kerberos 防御の Kerberos クライアント サポート**複合認証によって保護されているフェデレーション アプリケーションにアクセスするすべてのコンピューターに適用する必要があります。 これは、単一のフォレストが発生した場合、またはクロス フォレスト シナリオに適用します。

3.  ドメインの AD FS サーバーを格納している必要があります、**KDC で信頼性情報は複合認証、および Kerberos 防御のサポート**ポリシー設定がドメイン コントローラーに適用します。

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS を構成する手順
複合認証、および信頼性情報を構成するために、次の手順を使用してください。 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1: KDC で信頼性情報、複合認証、および既定のドメイン コントローラー ポリシーでの Kerberos 防御のサポートを有効にします。
1.  サーバー マネージャーで、選択ツール、**グループ ポリシーの管理**します。
2.  下に移動し、**既定のドメイン コントローラー ポリシー**を右クリックし、選択**編集**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  **グループ ポリシー管理エディター**[**コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、**KDC**します。
4.  右側のウィンドウでダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  新しいダイアログ ウィンドウで、設定の KDC で信頼性情報をサポート**有効**します。
6.  [オプション] を選択**サポートされている**クリックしてドロップダウン メニューから**適用**と**OK**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2: 信頼性情報、複合認証、およびフェデレーション アプリケーションにアクセスするコンピューターでの Kerberos 防御の Kerberos クライアント サポートを有効にします。

1.  フェデレーション アプリケーションにアクセスするコンピューターに適用されるグループ ポリシーで、**グループ ポリシー管理エディター**[**コンピューターの構成**、展開**ポリシー**、展開**管理テンプレート**、展開**システム**、] を選択して**Kerberos**します。
2.  グループ ポリシー管理エディター] ウィンドウの右側のウィンドウでダブルクリック**信頼性情報、複合認証、および Kerberos 防御の Kerberos クライアント サポートします。**
3.  新しいダイアログ ウィンドウで、Kerberos クライアント サポートを設定**有効**] をクリック**適用**と**OK**します。
![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>手順 3: は、AD FS サーバーが更新されたことを確認します。
次の更新プログラムが、AD FS サーバーにインストールされていることを確認する必要があります。

|更新プログラム|説明|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|累積的なセキュリティ更新プログラム (、kb2919355 という、KB2932046、KB2934018、KB2937592 KB2938439 が含まれています)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Server 2012 R2 用の更新プログラム|
|[修正プログラム 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|この更新プログラムは、Active Directory フェデレーション サービスに複合 ID のクレームのサポートを追加します。|

### <a name="step-4-configure-the-primary-authentication-provider"></a>手順 4: プライマリ認証プロバイダーを構成します。

1. プライマリ認証プロバイダーを設定**Windows 認証**の AD FS のイントラネット設定します。
2. AD FS 管理] の下にある**認証ポリシー**を選択**プライマリ認証**し、[**グローバル設定**] をクリックして**編集**します。
3. **グローバル認証ポリシーの編集**下にある**イントラネット**選択**Windows 認証**します。
4. をクリックして**適用**と**OK**します。

![グループ ポリシーの管理](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. PowerShell を使用することができますを使用して、**セット AdfsGlobalAuthenticationPolicy**コマンドレット。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID では、ファームでプライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell を基づいています。
>SQL ベースのファームで、ファームのメンバーある任意の AD FS サーバー上の PowerShell コマンドを実行する可能性があります。

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>手順 5: AD fs の要求記述を追加します。
1.  次の要求記述をファームに追加します。 この要求記述が ad FS 2012 R2 では、既定で存在しないと、手動で追加する必要があります。
2.  AD FS の管理下にある**サービス**を右クリックして**要求の説明**選択**要求記述の追加**
3.  要求記述で、次の情報を入力してください。
    - 表示名: ' Windows デバイス グループ ' 
    - 要求記述: 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' '
4. 両方のボックスで、チェックを配置します。
5. をクリックして**OK**します。

![要求記述](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. PowerShell を使用することができますを使用して、**追加 AdfsClaimDescription**コマンドレット。
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>WID では、ファームでプライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell を基づいています。
>SQL ベースのファームで、ファームのメンバーある任意の AD FS サーバー上の PowerShell コマンドを実行する可能性があります。

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 6: Msds-supportedencryptiontypes 属性のビット複合認証を有効にします。

1.  AD FS サービスを使用して、実行するときに指定したアカウントの Msds-supportedencryptiontypes 属性のビット複合認証を有効にする、**Set-adserviceaccount** PowerShell コマンドレット。  

>[!NOTE]
>サービス アカウントを変更するかどうかを実行して、複合認証を有効にする必要があります手動で、**Set-aduser compoundIdentitySupported: $true** Windows PowerShell コマンドレット。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Ad FS サービスを再起動します。

>[!NOTE]
>新しいサーバー (2012R2/2016) が失敗した場合、次のエラー – で同じ gMSA の true の場合、インストールに 'CompoundIdentitySupported' が設定されたら**インストール ADServiceAccount: サービス アカウントをインストールすることはできません。エラー メッセージ:"指定されたコンテキストが一致しませんターゲット。'**.
>
>**解決策**: 一時的に CompoundIdentitySupported を $false に設定します。 この手順により、ADFS WindowsDeviceGroup 信頼性情報の発行を停止します。 Set-ADServiceAccount-Identity の ' ad FS サービス アカウント CompoundIdentitySupported: $false gMSA を新しいサーバーにインストールし、$True に戻る CompoundIdentitySupported を有効に、します。
CompoundIdentitySupported を無効にし、有効にするは、ad FS サービスを再起動するのには必要ありません。

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>AD FS の要求プロバイダー信頼の Active Directory の手順 7: 更新プログラム

1. AD FS 要求プロバイダー信頼の 'WindowsDeviceGroup' 要求の次の 'パススルー' 要求規則を含めるように Active directory を更新します。
2.  **AD FS 管理**、] をクリックして**要求プロバイダー信頼**し、右側のウィンドウで右クリックして**Active Directory**選択**要求規則の編集**します。
3.  **アクティブ ディレクターの要求規則の編集**クリックして**規則の追加**します。
4.  **追加変換要求規則のウィザード**選択**パススルーまたはフィルター処理入力方向の要求**] をクリック**次**します。
5.  表示名を追加し、選択**Windows デバイス グループ**から、**入力方向の要求の種類**ドロップ ダウンします。
6.  をクリックして**完了**します。  をクリックして**適用**と**OK**します。 
![要求記述](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 8: 'WindowsDeviceGroup' 信頼性情報が必要な場所、証明書利用者のパーティ、同様の 'パススルー' または 'を ' 変換要求規則を追加します。
2.  **AD FS 管理**、] をクリックして**証明書利用者信頼**し、右側のウィンドウで右クリックして、RP と選択**要求規則の編集**します。
3.  **発行変換規則**クリックして**規則の追加**します。
4.  **追加変換要求規則のウィザード**選択**パススルーまたはフィルター処理入力方向の要求**] をクリック**次**します。
5.  表示名を追加し、選択**Windows デバイス グループ**から、**入力方向の要求の種類**ドロップ ダウンします。
6.  をクリックして**完了**します。  をクリックして**適用**と**OK**します。
![要求記述](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016 での AD FS を構成する手順
次では、Windows Server 2016 の AD FS で複合認証を構成する手順について説明します。

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>手順 1: KDC で信頼性情報、複合認証、および既定のドメイン コントローラー ポリシーでの Kerberos 防御のサポートを有効にします。
1.  サーバー マネージャーで、選択ツール、**グループ ポリシーの管理**します。
2.  下に移動し、**既定のドメイン コントローラー ポリシー**を右クリックし、選択**編集**します。
3.  **グループ ポリシー管理エディター**[**コンピューターの構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**、**KDC**します。
4.  右側のウィンドウでダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**します。
5.  新しいダイアログ ウィンドウで、設定の KDC で信頼性情報をサポート**有効**します。
6.  [オプション] を選択**サポートされている**クリックしてドロップダウン メニューから**適用**と**OK**します。


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>手順 2: 信頼性情報、複合認証、およびフェデレーション アプリケーションにアクセスするコンピューターでの Kerberos 防御の Kerberos クライアント サポートを有効にします。

1.  フェデレーション アプリケーションにアクセスするコンピューターに適用されるグループ ポリシーで、**グループ ポリシー管理エディター**[**コンピューターの構成**、展開**ポリシー**、展開**管理テンプレート**、展開**システム**、] を選択して**Kerberos**します。
2.  グループ ポリシー管理エディター] ウィンドウの右側のウィンドウでダブルクリック**信頼性情報、複合認証、および Kerberos 防御の Kerberos クライアント サポートします。**
3.  新しいダイアログ ウィンドウで、Kerberos クライアント サポートを設定**有効**] をクリック**適用**と**OK**します。
4.  グループ ポリシー管理エディターを閉じます。

### <a name="step-3-configure-the-primary-authentication-provider"></a>手順 3: プライマリ認証プロバイダーを構成します。

1. プライマリ認証プロバイダーを設定**Windows 認証**の AD FS のイントラネット設定します。
2. AD FS 管理] の下にある**認証ポリシー**を選択**プライマリ認証**し、[**グローバル設定**] をクリックして**編集**します。
3. **グローバル認証ポリシーの編集**下にある**イントラネット**選択**Windows 認証**します。
4. をクリックして**適用**と**OK**します。
5. PowerShell を使用することができますを使用して、**セット AdfsGlobalAuthenticationPolicy**コマンドレット。

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID では、ファームでプライマリ AD FS サーバーでコマンドを実行する必要があります、PowerShell を基づいています。
>SQL ベースのファームで、ファームのメンバーある任意の AD FS サーバー上の PowerShell コマンドを実行する可能性があります。

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>手順 4: Msds-supportedencryptiontypes 属性のビット複合認証を有効にします。

1.  AD FS サービスを使用して、実行するときに指定したアカウントの Msds-supportedencryptiontypes 属性のビット複合認証を有効にする、**Set-adserviceaccount** PowerShell コマンドレット。  

>[!NOTE]
>サービス アカウントを変更するかどうかを実行して、複合認証を有効にする必要があります手動で、**Set-aduser compoundIdentitySupported: $true** Windows PowerShell コマンドレット。

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Ad FS サービスを再起動します。

>[!NOTE]
>新しいサーバー (2012R2/2016) が失敗した場合、次のエラー – で同じ gMSA の true の場合、インストールに 'CompoundIdentitySupported' が設定されたら**インストール ADServiceAccount: サービス アカウントをインストールすることはできません。エラー メッセージ:"指定されたコンテキストが一致しませんターゲット。'**.
>
>**解決策**: 一時的に CompoundIdentitySupported を $false に設定します。 この手順により、ADFS WindowsDeviceGroup 信頼性情報の発行を停止します。 Set-ADServiceAccount-Identity の ' ad FS サービス アカウント CompoundIdentitySupported: $false gMSA を新しいサーバーにインストールし、$True に戻る CompoundIdentitySupported を有効に、します。
CompoundIdentitySupported を無効にし、有効にするは、ad FS サービスを再起動するのには必要ありません。

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>AD FS の要求プロバイダー信頼の Active Directory の手順 5: 更新プログラム

1. AD FS 要求プロバイダー信頼の 'WindowsDeviceGroup' 要求の次の 'パススルー' 要求規則を含めるように Active directory を更新します。
2.  **AD FS 管理**、] をクリックして**要求プロバイダー信頼**し、右側のウィンドウで右クリックして**Active Directory**選択**要求規則の編集**します。
3.  **アクティブ ディレクターの要求規則の編集**クリックして**規則の追加**します。
4.  **追加変換要求規則のウィザード**選択**パススルーまたはフィルター処理入力方向の要求**] をクリック**次**します。
5.  表示名を追加し、選択**Windows デバイス グループ**から、**入力方向の要求の種類**ドロップ ダウンします。
6.  をクリックして**完了**します。  をクリックして**適用**と**OK**します。 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>手順 6: 'WindowsDeviceGroup' 信頼性情報が必要な場所、証明書利用者のパーティ、上のような 'パススルー' または 'を ' 変換要求規則を追加します。
2.  **AD FS 管理**、] をクリックして**証明書利用者信頼**し、右側のウィンドウで右クリックして、RP と選択**要求規則の編集**します。
3.  **発行変換規則**クリックして**規則の追加**します。
4.  **追加変換要求規則のウィザード**選択**パススルーまたはフィルター処理入力方向の要求**] をクリック**次**します。
5.  表示名を追加し、選択**Windows デバイス グループ**から、**入力方向の要求の種類**ドロップ ダウンします。
6.  をクリックして**完了**します。  をクリックして**適用**と**OK**します。

## <a name="validation"></a>検証
'WindowsDeviceGroup' の信頼性情報のリリースの検証、テストを作成するには、.Net 4.6 を使用して対応するアプリケーションを要求します。 WIF sdk 4.0 します。
Ad FS の証明書利用者のパーティとしてアプリケーションを構成し、上記の手順で指定されている要求規則で更新します。
ADFS の統合 Windows 認証プロバイダーを使用してアプリケーションを認証するときは、次の要求はキャストされます。
![検証](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

高度なアクセス制御のコンピューター/デバイスの信頼性情報を消費することができるようになりました。

次の例: **AdditionalAuthenticationRules** – 認証ユーザーがセキュリティ グループのメンバーではない場合に MFA を呼び出すための AD FS に指示"-1-5-21-2134745077-1211275016-3050530490-1117"と、コンピューター (ここでは、ユーザーは認証) が"S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)"のセキュリティ グループのメンバーではないです。

ただし、上記の条件のいずれかが満たされた場合は MFA 呼び出されません。

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```