---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: "AD FS サインイン ページのカスタマイズの詳細"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/13/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ea01d0ff2a38c4fef2f68091608d777d8412e91b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS サインイン ページのカスタマイズの詳細

>適用対象: Windows Server 2016、Windows Server 2012 R2
  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>AD FS サインイン ページの高度なカスタマイズ  
Windows Server 2012 R2 の AD FS は、サインイン エクスペリエンスをカスタマイズするための組み込みのサポートを提供します。 これらのシナリオの大部分を組み込みの Windows PowerShell コマンドレットとは、必要なのです。  AD FS サインイン エクスペリエンスを得る可能な限り、標準的な要素をカスタマイズする、組み込みの Windows PowerShell コマンドを使用することをお勧めします。  参照してください[AD FS ユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)詳細についてはします。  
  
場合によっては、AD FS 管理者は、AD FS と詳細なボックスに組み込まれている既存の PowerShell コマンドを使ってれていないその他のサインイン エクスペリエンスを提供する必要可能性があります。 一部のインスタンスで、ことが可能な \ (示されているガイドライン below\) 内エクスペリエンスのカスタマイズ サインインさらに追加のロジックを追加することで、管理者用**onload.js** AD FS によって提供され、すべての AD FS ページ上で実行します。  
  
## <a name="things-to-know-before-you-start"></a>開始する前に知っておく  
  
-   リダイレクト フローに影響するかで AD FS が動作するプロトコルのパラメーターを変更を変更することはできません。
  
-   既定の web テーマに付属している元の onload.js には、さまざまなフォーム ファクターのページのレンダリングを処理するコードが含まれています。 元の onload.js コンテンツの変更が、カスタム ロジックを処理する既存 onload.js にのみ、コードを追加しないことをお勧めします。  
  
-   AD FS は、既定と呼ばれる組み込みの web テーマが付属します。 既定の web テーマの onload.js を変更することはできません。 Onload.js を更新するには、作成し、AD FS サインイン ページのカスタム web テーマを使用する必要があります。  参照してください[AD FS ユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)カスタム web テーマを作成する方法についてです。  
  
-   すべての ad FS ページ \(ex. で同じ onload.js が実行されます。 フォーム ベースのログオン ページ、ホーム領域検出ページなど、。 \)。 スクリプト内でコードのみを取得実行されるように設計されており、予期せずが実行されないことを確認する必要があります。  
  
-   HTML の任意の要素を参照するときに、常にチェックする要素に作用する前に、要素が存在することを確認します。 これは、堅牢性を提供し、カスタムのロジックがこの要素が含まれていないページで実行されていないは確認します。 単に既存の要素を表示する AD FS サインイン ページの HTML のソースを表示できます。  
  
-   別の環境で、カスタマイズの内容を検証し、それらを運用環境に AD FS サーバーのロール アウトする前にテストを強くお勧めします。 これにより、エンドユーザーが検証する前にこれらのカスタマイズに公開される可能性が減少します。  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Onload.js を使用して、AD FS サインイン エクスペリエンスをカスタマイズします。  
AD FS サービスの onload.js をカスタマイズする場合は、次の手順を使用します。  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>AD FS サービスの onload.js をカスタマイズします。  
  
1.  Onload.js に、カスタム ロジックを追加するには、まずカスタム web テーマを作成する必要があります。 テーマは出荷 out\ of\-the\ のボックスには、既定は呼び出されます。 既定のテーマをエクスポートし、すばやく開始できるように使用できます。 次のコマンドレットでは、既定の web テーマを複製して、カスタム web テーマを作成します。  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  ユーザー設定をエクスポートし、または既定の web テーマ onload.js ファイルを取得できます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    Onload.js スクリプト フォルダーの下で見つかりますディレクトリ上、export コマンドレットで指定し、スクリプトに、カスタム ロジックを追加する \ (「」を参照例セクション below\ のユース ケース).  
  
3.  必要に応じて onload.js をカスタマイズするために必要な変更を行います。  
  
4.  変更した onload.js でテーマを更新します。 カスタム web テーマに更新 onload.js を適用するには、次のコマンドレットを使用します。  
  
    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
  
5.  AD FS にカスタム web テーマを適用するには、次のコマンドレットを使用します。  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>その他のカスタマイズの例  
Onload.js 異なる fine\ 調整のために追加されるカスタム コードの例を次に示します。 カスタム コードを追加する場合は、onload.js の一番下の独自のコードを追加してください常にします。  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>例 1:「の組織のアカウントでサインイン」文字列を変更します。  
ユーザーの入力ボックスの上「組織のアカウントでサインイン」というタイトルを、既定の AD FS フォーム ベースのサインイン ページには。  
  
この文字列に独自の文字列を置き換える場合は、onload.js に次のコードを追加できます。  
  
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
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>例 2: AD FS フォーム ベース サインインのページでログイン形式として SAM\ アカウント名をそのまま使用します。  
既定のユーザー プリンシパル名 \(UPNs\) \(for example, ** johndoe@contoso.com **\) またはドメインの AD FS サインイン ページのフォーム ベースをサポートしていますログイン形式 sam\ アカウント名を修飾 \ (**contoso\\johndoe**または**contoso.com\\johndoe**\)。 場合に、同じドメインに由来するすべてのユーザーと、sam\ アカウント名は知っているのみ、それら sam\ アカウント名のみを使用する、ユーザーがサインインできるシナリオをサポートする可能性があります。 このシナリオをサポートする、ドメイン"contoso.com"の例では以下を使用するドメインと置き換えます onload.js には、次のコードを追加できます。  
  
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
  
## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  

