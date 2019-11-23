---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Microsoft 著作権情報を削除する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0c24173dd03e03f9e8a19ef5981a6dc1259d62d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407516"
---
# <a name="remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除する 


 
既定では、AD FS のページには Microsoft 著作権情報が含まれています。 この著作権情報をカスタマイズ済みページから削除するには、次の手順に従います。 

![著作権情報の削除](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除するには  
  
1. 既定のテーマに基づいてカスタム テーマを作成します。

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. 出力フォルダーを指定してテーマをエクスポートします。  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. 出力フォルダーにある `Style.css` ファイルを見つけます。 前の例を使用すると、パスは `C:\CustomWebTheme\Css\Style.css.`
  
4. メモ帳などのエディターを使用して、`Style.css` ファイルを開きます。  
  
5. `#copyright` の部分を見つけたら、次のように変更します。  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. 新しい `Style.css` ファイルに基づいたカスタムテーマを作成します。  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. 新しいテーマをアクティブ化します。  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

サインインページの下部に著作権情報が表示されなくなります。

![著作権情報の削除](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md) 
