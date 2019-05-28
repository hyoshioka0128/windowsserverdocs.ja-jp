---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: AD FS サインイン ページのカスタマイズの詳細
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73ff3fc6df872edd29735ee96c0918144250d5f1
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190045"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS サインイン ページのカスタマイズの詳細

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS のサインインのカスタマイズを高度な\-ページ  
Windows Server 2012 R2 で AD FS は、ビルドを提供します。\-符号をカスタマイズするためのサポートの\-エクスペリエンス。 これらのシナリオは、組み込みの大半\-コマンドレットでは Windows PowerShell では必要なのです。  組み込みを使用することをお勧め\-AD FS の標準的な要素をカスタマイズする Windows PowerShell コマンドでは、サインイン\-エクスペリエンスが可能な場合。  参照してください[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)詳細についてはします。  
  
追加のサインインを提供する必要は場合によっては、AD FS 管理者\-れないエクスペリエンスで、既存の PowerShell コマンドに出荷する\-と AD FS のボックスです。 特定のインスタンスが可能な\(以下のガイドライン内\)符号をカスタマイズする管理者用\-エクスペリエンスで追加のロジックを追加することによってさらに**onload.js**ですAD FS によって提供され、AD FS のすべてのページで実行されます。  
  
## <a name="things-to-know-before-you-start"></a>開始する前に知っておくべきこと  
  
-   リダイレクトのフローに影響を与えますまたは AD FS の連携プロトコル パラメーターを変更する変更はサポートされていません。
  
-   既定の web テーマが付属している元の onload.js には、フォーム ファクター別のページのレンダリングを処理するコードが含まれています。 Onload.js の元のコンテンツの変更が、カスタム ロジックを処理する既存の onload.js にのみ、コードを追加していないことをお勧めします。  
  
-   AD FS が組み込まれているが付属しています\-と呼ばれる既定の web テーマです。 既定の web テーマの onload.js を変更することはできません。 Onload.js を更新するには、作成して AD FS のサインインのカスタム web テーマを使用する必要がある\-ページ。  参照してください[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)については、カスタム web テーマを作成する方法。  
  
-   ADFS のすべてのページの実行は同じ onload.js \(ex。 フォーム\-ベースのログオン ページ、ホーム領域検出ページなど\)します。 コードをスクリプトにのみ実行は設計されていて、予期しない実行されないことを確認する必要があります。  
  
-   任意の HTML 要素を参照するときに、要素で動作する前に、要素の存在をチェックを常に確認します。 これにより、堅牢性を提供し、カスタム ロジックをこの要素が含まれていないページで実行されませんが。 AD FS のサインインで単に HTML ソースを表示できます\-で既存の要素を表示するページ。  
  
-   別の環境に、カスタマイズ設定を検証し、それらを運用環境に AD FS サーバーのロール アウトする前にテストを強くお勧めします。 これにより、エンド ユーザーを検証する前にこれらのカスタマイズに公開される可能性が減少します。  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>AD FS のサインインのカスタマイズ\-onload.js を使用してエクスペリエンス  
AD FS サービスの onload.js をカスタマイズする際に、次の手順を使用します。  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>AD FS サービスの onload.js をカスタマイズします。  
  
1.  Onload.js には、カスタム ロジックを追加するには、まず、カスタム web テーマを作成する必要があります。 同梱されているテーマ\-の\-、\-ボックスは既定値と呼ばれます。 既定のテーマをエクスポートして使用すると、カスタマイズを簡単に開始できます。 次のコマンドレットでは、既定の web テーマを複製するカスタム web テーマを作成します。  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  ユーザー設定をエクスポートしたり、既定の web テーマ onload.js ファイルを取得できます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    Onload.js スクリプト フォルダーの下で見つかりますディレクトリ エクスポート コマンドレットは、上記で指定し、スクリプトに、カスタム ロジックを追加する\(を参照してください以下のセクションの例のユース ケース\)します。  
  
3.  必要に応じて onload.js をカスタマイズするために必要な変更を行います。  
  
4.  変更された onload.js でテーマを更新します。 Update onload.js をカスタム web テーマを適用するには、次のコマンドレットを使用します。  

     Windows Server 2012 R2 で AD FS:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
    Windows server 2016 の AD FS:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\ADFStheme\script\onload.js"   
  
    ```  
  
5.  AD FS には、カスタム web テーマを適用するには、次のコマンドレットを使用します。  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>その他のカスタマイズ例  
さまざまな細かい onload.js に追加されたカスタム コードの例を次に\-目的を調整します。 カスタム コードを追加する場合は、onload.js の下部に、カスタム コードを追加してください常にします。  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>例 1:「組織アカウントでサインイン」の文字列を変更します。  
既定の AD FS のフォーム\-ベースのサインオン\- ページでユーザーの入力ボックスの上の「組織アカウントでサインイン」のタイトルが付いています。  
  
この文字列を独自の文字列に置き換える場合は、onload.js に次のコードを追加できます。  
  
```  
// Sample code to change “Sign in with organizational account” string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>例 2: SAM を受け入れる\-アカウント名には、AD FS のフォームをログイン形式\-ベースのサインオン\- ページ  
既定の AD FS フォーム\-ベースのサインオン\- ページでユーザー プリンシパル名のログインの形式をサポートしています\(Upn\) \(など**johndoe@contoso.com** \) 。ドメイン修飾 sam または\-アカウント名\( **contoso\\johndoe**または**contoso.com\\johndoe**\)します。 場合は、同じドメインから取得すべてのユーザーと sam について知らないのみ\-アカウント名、sam それらを使用して、ユーザーがサインインできる場所のシナリオをサポートするためにすることがあります\-アカウント名のみです。 このシナリオをサポートするには、ドメイン"contoso.com"の例では、以下を使用するドメインに置き換えます onload.js に次のコードを追加できます。  
  
```  
if (typeof Login != 'undefined'){  
    Login.submitLoginRequest = function () {   
    var u = new InputUtil();  
    var e = new LoginErrors();  
    var userName = document.getElementById(Login.userNameInput);  
    var password = document.getElementById(Login.passwordInput);  
    if (userName.value && !userName.value.match('[@\\\\]'))   
    {  
        var userNameValue = 'contoso.com\\' + userName.value;  
        document.forms['loginForm'].UserName.value = userNameValue;  
    }  
  
    if (!userName.value) {  
       u.setError(userName, e.userNameFormatError);  
       return false;  
    }  
  
    if (!password.value)   
    {  
        u.setError(password, e.passwordEmpty);  
        return false;  
    }  
    document.forms['loginForm'].submit();  
    return false;  
};  
}  
  
```  
  
## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  

