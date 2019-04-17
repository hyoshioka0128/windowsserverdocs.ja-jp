---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: "AD FS サインイン ページにイラストを変更します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac5e60aaad864248b58a3908e7aa9622165fbc14
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページにイラストを変更します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

## <a name="change-the-illustration"></a>変更の図  


イラストを変更するには、左側のサインイン ページに表示される画像は、次の Windows PowerShell の PowerShell コマンドレットと構文を使用します。  

![イラストを変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> ファイル サイズは 200 KB よりも 96 DPI @ 1420 x 1080 ピクセルの図の大きさことをお勧めします。  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  
  
