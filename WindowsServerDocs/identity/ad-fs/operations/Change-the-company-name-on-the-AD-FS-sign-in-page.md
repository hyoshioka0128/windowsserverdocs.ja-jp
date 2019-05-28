---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: AD FS サインイン ページに会社名を変更します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2b5c7228094305759344d5094cffa7f24a0da7a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190023"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページに会社名を変更します。
 
記号が表示される会社の名前を変更する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。 この値には、セットアップ時に入力したフェデレーション サービスの表示名が既定で設定されています。  

![名前を変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Windows PowerShell Integrated Scripting Environment を使用することもできます。 \(ISE\)会社名を変更します。 Windows PowerShell ISE を使用すると、Unicode でコンテンツを表示することができます\-準拠の環境。 詳細については、「 [Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)」を参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  
