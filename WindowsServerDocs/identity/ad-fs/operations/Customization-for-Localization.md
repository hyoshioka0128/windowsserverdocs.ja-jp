---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: ローカリゼーション用のカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac206d5aa8af970b65a014955ac66a8cf2835eb6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882033"
---
# <a name="customization-for-localization"></a>ローカリゼーション用のカスタマイズ 

>適用先:Windows Server 2016、Windows Server 2012 R2

Web コンテンツを英語以外の言語にローカライズできます。 ローカライズを行う場合は、次の考慮事項に注意してください。  
  
コンテンツをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でコンテンツをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成するときに、国で構成\-少ないロケール最初に、たとえば、"en"、country と region を構成する前に\-などの特定のロケール"en\-私たち"です。  
  
追加のコード例を次に示します。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
追加のコード例を次に示します。  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Web コンテンツを Unicode の入力が必要な英語以外の言語をカスタマイズする場合は、Windows PowerShell ISE を使用することをお勧めします。 詳細については、「 [Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)」を参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
