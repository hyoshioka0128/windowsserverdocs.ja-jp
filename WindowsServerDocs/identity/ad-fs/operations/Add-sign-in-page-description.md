---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: 記号を追加\-でページの説明
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 94ad9889ce78ba77f016210ee478a301babdf307
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190049"
---
# <a name="add-sign-in-page-description"></a>記号を追加\-でページの説明


## <a name="to-add-sign-in-page-description"></a>追加の署名を\-でページの説明  
記号を追加する\-、サインオン ページの説明で\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![説明のサインインを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 そのため、実行することも、次のコマンドレットを使用せず、 &lt;p&gt;タグ。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

記号の後\- ページでは、カスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語の情報をカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成するときに、国を構成する必要があります\-少ないロケール最初に、たとえば、"en"、country と region を構成する前に\-などの特定のロケール"en\-私たち"です。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
