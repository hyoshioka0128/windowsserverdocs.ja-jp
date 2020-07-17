---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: AD FS サインインページで会社のロゴを変更する
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d12429b22265495cb8168ce3e5993a5cf3e74a0c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859975"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>AD FS サインインページで会社のロゴを変更する

#### <a name="change-company-logo"></a>会社ロゴの変更  
[\-のサインイン] ページに表示される会社のロゴを変更するには、次の PowerShell Windows PowerShell コマンドレットと構文を使用します。  

![ロゴの変更](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> ロゴの寸法は 260x35 ピクセル (96 DPI) に設定して、ファイル サイズは 10 KB 以下にすることをお勧めします。  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> `TargetName` パラメーターは必須です。 AD FS と共にリリースされる既定のテーマには、 *default*という名前が付けられます。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
