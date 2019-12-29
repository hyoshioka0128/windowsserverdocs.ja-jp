---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: AD FS サインインページの図を変更する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3da7726ca625c32728fb0ae64d291ae599b6cd8d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358291"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS サインインページの図を変更する

## <a name="change-the-illustration"></a>図を変更する  


左側のグラフィックを変更するには、[\-のサインイン] ページに表示される次の Windows PowerShell コマンドレットと構文を使用します。  

![図の変更](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> イラストの寸法は 1420x1080 ピクセル (96 DPI) に設定して、ファイル サイズは 200 KB 以下にすることをお勧めします。  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
  
  
