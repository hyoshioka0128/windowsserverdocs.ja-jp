---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: "ローカライズのカスタマイズ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac206d5aa8af970b65a014955ac66a8cf2835eb6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="customization-for-localization"></a>ローカライズのカスタマイズ 

>適用対象: Windows Server 2016、Windows Server 2012 R2

Web コンテンツを英語以外の言語にローカライズすることができます。 ローカライズするときにする次の考慮事項に注意してください。  
  
コンテンツをカスタマイズすると、カスタマイズ設定が優先されます。そのため、すべての言語をサポートするでカスタマイズする必要があります。 すべてのカスタマイズ コンテンツは、ロケール パラメーターを受け取ります。 ローカライズされたコンテンツを構成するときに構成 country\ を含まないロケールで最初に、たとえば、"en"国および region\ に固有のロケールをよう構成する前に"en\-ご"です。  
  
追加のコード例を次に示します。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
追加のコード例を次に示します。  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Web コンテンツを Unicode の入力が必要な英語以外の言語をカスタマイズする場合は、Windows PowerShell ISE を使用することをお勧めします。 詳細についてを参照してください。[Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)します。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
