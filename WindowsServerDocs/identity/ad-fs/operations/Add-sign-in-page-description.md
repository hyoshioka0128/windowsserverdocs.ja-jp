---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: サインイン ページへの説明の追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 918fdce52972edc0b7b4ccba76f8b65b6d91786f
ms.sourcegitcommit: 67d9c51e396c8f937f8704a25e66fea8c5fae81a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87441538"
---
# <a name="add-sign-in-page-description"></a>サインイン \- ページの説明の追加


## <a name="to-add-sign-in-page-description"></a>サインインページの説明を追加するには \-  
サインインページにサインインページの説明を追加するには、 \- \- 次の Windows PowerShell コマンドレットと構文を使用します。  

![サインインの説明の追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 したがって、p タグを使用せずに次のコマンドレットを実行することもでき &lt; &gt; ます。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

サインインページをカスタマイズすると、 \- カスタマイズが優先されるため、サポートするすべての言語に合わせてカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" など、 \- 国と地域に固有のロケールを構成する前に、最初に "en" などの国のロケールで構成する必要があり \- \- ます。  

## <a name="additional-references"></a>その他のリファレンス 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
