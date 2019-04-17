---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: "Microsoft 著作権情報を削除します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c2e6f9445e53a5b5867a763d58ad4a6ca3600cbe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2
 
既定では、AD FS のページには Microsoft 著作権情報が含まれています。 カスタマイズ済みページからこの著作権情報を削除するには、次の手順を使用することができます。 

![著作権情報を削除します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除するには  
  
1.  既定値に基づいたカスタム テーマを作成します。  
  

    `New-AdfsWebTheme –Name custom –SourceName default ` 
 
  
2.  出力フォルダーを指定してテーマをエクスポートします。  

    `Export-AdfsWebTheme -Name custom -DirectoryPath C:\customWebTheme ` 

  
3.  出力フォルダーに配置されている Style.css ファイルを見つけます。 前の例を使用してパスを C:\\CustomWebTheme\\Css\\Style.css となります。  
  
4.  メモ帳などのエディターで Style.css ファイルを開きます。  
  
5.  検索、`#copyright`部分、および、次に変更します。  
  `#copyright {color:#696969; display:none;} ` 
 
6.  新しい Style.css ファイルに基づいたカスタム テーマを作成します。  
  
    `Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}  `

7.  新しいテーマをアクティブ化します。  
  

    `Set-AdfsWebConfig -ActiveThemeName custom ` 


これで、サインイン ページの下部にある著作権が不要になった表示されます。

![著作権情報を削除します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
