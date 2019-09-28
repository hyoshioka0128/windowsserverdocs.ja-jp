---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: ローカライズのカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ba3441d362960e054791ca3d6872dba6c7bd9a12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357980"
---
# <a name="customization-for-localization"></a>ローカライズのカスタマイズ 


Web コンテンツを英語以外の言語にローカライズできます。 ローカライズを行う場合は、次の考慮事項に注意してください。  
  
コンテンツをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でコンテンツをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" のように、国と地域を構成する前に、最初に "en" などの国の @ no__t-0less ロケールで構成します。  
  
追加のコード例を次に示します。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
追加のコード例を次に示します。  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Unicode の入力が必要な英語以外の言語に web コンテンツをカスタマイズする場合は、Windows PowerShell ISE を使用することをお勧めします。 詳細については、「 [Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)」を参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md) 
