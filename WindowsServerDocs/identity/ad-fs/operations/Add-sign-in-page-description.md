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
ms.openlocfilehash: 553cdcf2ac98b23d06cc43a64220cf8433117fc8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814013"
---
# <a name="add-sign-in-page-description"></a>記号を追加\-でページの説明

>適用先:Windows Server 2016、Windows Server 2012 R2

## <a name="to-add-sign-in-page-description"></a>追加の署名を\-でページの説明  
記号を追加する\-、サインオン ページの説明で\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![説明のサインインを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 そのため、実行することも、次のコマンドレットを使用せず、 &lt;p&gt;タグ。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

記号の後\- ページでは、カスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語の情報をカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成するときに、国を構成する必要があります\-少ないロケール最初に、たとえば、"en"、country と region を構成する前に\-などの特定のロケール"en\-私たち"です。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
