---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: AD FS サインイン ページに会社のロゴを変更します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6e0271ae3d7ac120e510a2fb81fb55c8d10b3c87
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813583"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページに会社のロゴを変更します。

>適用先:Windows Server 2016、Windows Server 2012 R2

#### <a name="change-company-logo"></a>会社ロゴの変更  
記号が表示される会社のロゴを変更する\- ページで、次の PowerShell の Windows PowerShell コマンドレットと構文を使用します。  

![ロゴを変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> ロゴの寸法は 260x35 ピクセル (96 DPI) に設定して、ファイル サイズは 10 KB 以下にすることをお勧めします。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> `TargetName` パラメーターは必須です。 AD FS と共にリリースされている既定のテーマの名前は*既定*します。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
