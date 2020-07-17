---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: ページの説明に符号\-を追加する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8d3cc69bde1c9126f97926802b53d049ed1ef501
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859995"
---
# <a name="add-sign-in-page-description"></a>ページの説明に符号\-を追加する


## <a name="to-add-sign-in-page-description"></a>ページの説明に符号\-を追加するには  
ページの説明に署名\-を\-ページに追加するには、次の Windows PowerShell コマンドレットと構文を使用します。  

![サインインの説明の追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 そのため、&lt;p&gt; タグを使用せずに、次のコマンドレットを実行することもできます。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

ページの [\-の署名] がカスタマイズされると、カスタマイズが優先されます。そのため、サポートするすべての言語でをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" のように、国と地域を構成する前に、"en\-us" のような特定のロケール\-国と地域を構成する前に、"en" などの\-国のロケールで構成する必要があります。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
