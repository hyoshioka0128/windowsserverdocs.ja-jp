---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: "AD FS サインイン ページで会社のロゴを変更します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ca54abe7fe852b22f2f4d9a717e38d219fa50694
ms.sourcegitcommit: a00fc4426dc4ad0098257f01f0124d6c733d1aef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2018
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページで会社のロゴを変更します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

#### <a name="change-company-logo"></a>会社ロゴの変更  
サインイン ページに表示される会社のロゴを変更するには、次の PowerShell の Windows PowerShell コマンドレットと構文を使用します。  

![ロゴを変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 10 KB よりものファイル サイズが 96 dpi @ 260 x 350 であるロゴの寸法ことをお勧めします。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> `TargetName`パラメーターは必須です。 AD FS に含まれている既定のテーマの名前は*既定*します。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
