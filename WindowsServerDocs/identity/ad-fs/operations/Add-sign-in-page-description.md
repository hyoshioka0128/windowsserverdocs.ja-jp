---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: "サインイン ページの説明を追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 128a4ffd8d4b9dfcfe5f0e8e2df8a0e1505cbb24
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-sign-in-page-description"></a>サインイン ページの説明を追加します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

## <a name="to-add-sign-in-page-description"></a>サインイン ページの説明を追加するには  
サインイン ページには、サインイン ページの説明を追加するには、次の Windows PowerShell の PowerShell コマンドレットと構文を使用します。  

![説明にログを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> 文字列を`SignInPageDescriptionText`パラメーターには、タグとはなしのピュア HTML がサポートしています。 そのため、実行することも、次のコマンドレットを使用せず、&lt;p&gt;タグ。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

サインイン ページをカスタマイズすると、カスタマイズ設定が優先されます。そのため、すべての言語をサポートするでカスタマイズする必要があります。 すべてのカスタマイズ コンテンツは、ロケール パラメーターを受け取ります。 ローカライズされたコンテンツを構成するときに、向けに構成される country\ を含まないロケールで最初に、例では、"en"国および region\ に固有のロケールをよう構成する前に"en\-ご"です。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
