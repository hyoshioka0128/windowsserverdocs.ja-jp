---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: AD FS サインインページで会社名を変更する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 378979825c0e8e505c3996cf8cbcdb471a0c7d79
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859965"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>AD FS サインインページで会社名を変更する
 
[\-のサインイン] ページに表示される会社の名前を変更するには、次の Windows PowerShell コマンドレットと構文を使用します。 この値には、セットアップ時に入力したフェデレーション サービスの表示名が既定で設定されています。  

![名前の変更](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Windows PowerShell Integrated Scripting Environment \(ISE\) を使用して会社名を変更することもできます。 Windows PowerShell ISE を使用すると、Unicode\-準拠環境でコンテンツを表示できます。 詳細については、「 [Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)」を参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
  
