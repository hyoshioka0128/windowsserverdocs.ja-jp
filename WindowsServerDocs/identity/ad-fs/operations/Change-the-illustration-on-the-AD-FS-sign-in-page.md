---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: AD FS サインイン ページのイラストを変更します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4f1cba9862766092c2beadb894cbac092d146887
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858243"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページのイラストを変更します。

>適用先:Windows Server 2016、Windows Server 2012 R2

## <a name="change-the-illustration"></a>変更の図は、  


図では、記号を表示される、左側の画像を変更する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![イラストを変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> イラストの寸法は 1420x1080 ピクセル (96 DPI) に設定して、ファイル サイズは 200 KB 以下にすることをお勧めします。  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  
  
