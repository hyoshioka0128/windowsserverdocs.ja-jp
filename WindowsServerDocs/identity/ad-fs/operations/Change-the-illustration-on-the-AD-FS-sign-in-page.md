---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: AD FS サインインページの図を変更する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: de0fc7af4c4eecad59b7af6b08426ef207da5db1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859955"
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
  
  
