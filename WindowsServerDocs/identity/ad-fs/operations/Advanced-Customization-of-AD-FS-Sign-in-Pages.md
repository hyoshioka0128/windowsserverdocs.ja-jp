---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: AD FS サインインページの高度なカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e49b18bf5e10de6150603b690095f61a13e59ef2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865991"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS サインインページの高度なカスタマイズ

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS サインイン\-ページの高度なカスタマイズ  
Windows Server 2012 R2 の AD FS には\-、サインイン\-エクスペリエンスをカスタマイズするためのサポートが組み込まれています。 これらのシナリオの大部分では、\-組み込みの Windows PowerShell コマンドレットが必要です。  組み込み\-の Windows PowerShell コマンドを使用して、可能な限り AD FS サインイン\-エクスペリエンスの標準要素をカスタマイズすることをお勧めします。  詳細については[、「AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)」を参照してください。  
  
場合によっては、AD FS 管理者が、AD FS\-box で\-出荷される既存の PowerShell コマンドを使用して実行できない追加のサインインエクスペリエンスを提供することがあります。 特定のインスタンスでは、管理\(者がサインイン\-エクスペリエンスを\)さらにカスタマイズするために、次に示すガイドラインに従うことをお勧めし**ます。** これは、AD FS によって提供される追加のロジックを追加することにより、すべての AD FS ページで実行されます。  
  
## <a name="things-to-know-before-you-start"></a>開始する前に理解しておくべきこと  
  
-   リダイレクトフローに影響を与える変更や、で動作する AD FS プロトコルパラメーターを変更することはサポートされていません。
  
-   既定の web テーマに付属する元の onload には、さまざまなフォームファクターのページレンダリングを処理するコードが含まれています。 元の onload コンテンツを変更しないことをお勧めしますが、カスタムロジックを処理する既存の onload にコードを追加するだけです。  
  
-   AD FS には、既定\-と呼ばれる組み込みの web テーマが付属しています。 既定の web テーマの onload を変更することはできません。 Onload を更新するには、AD FS サインイン\-ページのカスタム web テーマを作成して使用する必要があります。  カスタム web テーマを作成する方法については[、「AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)」を参照してください。  
  
-   同じ onload がすべての ADFS ページ\(ex で実行されます。 フォーム\-ベースのログオンページ、ホーム領域検出ページ\)など。 スクリプト内のコードがデザイン時にのみ実行されるようにし、予期せずに実行されないようにする必要があります。  
  
-   HTML 要素を参照する場合は、要素に対して動作する前に、必ず要素の存在を確認してください。 これにより、堅牢性が提供され、この要素が含まれていないページでカスタムロジックが実行されないようにします。 AD FS サインイン\-ページで HTML ソースを表示するだけで、既存の要素を表示できます。  
  
-   カスタマイズを代替環境で検証し、運用 AD FS サーバーにロールアウトする前にテストすることを強くお勧めします。 これにより、エンドユーザーが検証の前にこれらのカスタマイズに公開される可能性が低くなります。  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Onload を使用し\-た AD FS サインインエクスペリエンスのカスタマイズ  
AD FS サービスに対して onload をカスタマイズする場合は、次の手順に従います。  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>AD FS サービス用に onload をカスタマイズする  
  
1.  カスタムロジックを onload に追加するには、最初にカスタム web テーマを作成する必要があります。 既定と呼ばれるのは\-、\-その\-まま出荷されるテーマです。 既定のテーマをエクスポートして使用すると、カスタマイズを簡単に開始できます。 次のコマンドレットは、既定の web テーマを複製するカスタム web テーマを作成します。  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  その後、カスタムまたは既定の web テーマをエクスポートして、ファイルを取り込むことができます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    上記の export コマンドレットで指定したディレクトリのスクリプトフォルダーの下に、onload があることを確認し、カスタムロジックをスクリプト\(に追加します。次\)の「例」の「ユースケース」を参照してください。  
  
3.  必要に応じて、onload をカスタマイズするために必要な変更を行います。  
  
4.  変更した onload でテーマを更新します。 次のコマンドレットを使用して、更新プログラムの onload をカスタム web テーマに適用します。  

     Windows Server 2012 R2 の AD FS:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}  
  
    ```  
    Windows Server 2016 の AD FS:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\ADFStheme\script\onload.js"   
  
    ```  
  
5.  AD FS にカスタム web テーマを適用するには、次のコマンドレットを使用します。  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>その他のカスタマイズの例  
次に、さまざまな\-微調整を目的として、onload に追加されたカスタムコードの例を示します。 カスタムコードを追加するときは、必ずカスタムコードを onload の末尾に追加してください。  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>例 1: "組織のアカウントでサインインする" 文字列を変更する  
既定の AD FS フォーム\-ベースの\-サインインページには、ユーザー入力ボックスの上に "組織のアカウントでサインイン" というタイトルが付いています。  
  
この文字列を独自の文字列に置き換える場合は、次のコードを追加することができます。  
  
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
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>例 2: AD FS フォーム\-\-ベースのサインイン\-ページで SAM アカウント名をログイン形式として受け入れる  
既定の AD FS フォーム\-ベースの\-サインインページでは、ユーザープリンシパル名\) \( \(upn のログイン形式 ( <strong>johndoe@contoso.com</strong>たとえば、ドメイン修飾 sam \) \-)がサポートされています。アカウント名\( **contosojohndoe\\** また**はcontoso.com\\johndoe。** \) すべてのユーザーが同じドメインからのものであり、sam\-アカウント名のみを認識している場合は、ユーザーが sam\-アカウント名のみを使用してサインインできるシナリオをサポートすることをお勧めします。 次のコードを、このシナリオをサポートするために、次の例のドメイン "contoso.com" を使用するドメインに置き換えるだけで、このシナリオをサポートすることができます。  
  
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
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
  

