---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: サインイン ページへの説明の追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 033663720750ee2990cbc6eb4dd0c6d9abe1a002
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962636"
---
# <a name="add-sign-in-page-description"></a>サインイン \- ページの説明の追加

## <a name="to-add-sign-in-page-description"></a>サインインページの説明を追加するには \-
サインインページにサインインページの説明を追加するには、 \- \- 次の Windows PowerShell コマンドレットと構文を使用します。

![サインインの説明の追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

```powershell
Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"
```

> [!IMPORTANT]
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 したがって、p タグを使用せずに次のコマンドレットを実行することもでき &lt; &gt; ます。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." `

サインインページをカスタマイズすると、 \- カスタマイズが優先されるため、サポートするすべての言語に合わせてカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" など、 \- 国と地域に固有のロケールを構成する前に、最初に "en" などの国のロケールで構成する必要があり \- \- ます。

## <a name="additional-references"></a>その他の参照情報

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
