---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Microsoft 著作権情報を削除します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aa27a014b0803712a20fdd23f075486dc35f33c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820983"
---
# <a name="remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除します。 

>適用先:Windows Server 2016、Windows Server 2012 R2
 
既定では、AD FS ページには Microsoft 著作権情報が含まれます。 この著作権情報をカスタマイズ済みページから削除するには、次の手順に従います。 

![著作権情報を削除します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Microsoft 著作権情報を削除するには  
  
1. 既定のテーマに基づいてカスタム テーマを作成します。

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. 出力フォルダーを指定してテーマをエクスポートします。  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. 検索、`Style.css`出力フォルダーにあるファイル。 前の例を使用すると、パスになります。 `C:\CustomWebTheme\Css\Style.css.`
  
4. 開く、`Style.css`ファイルをメモ帳などのエディター。  
  
5. `#copyright` の部分を見つけたら、次のように変更します。  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. 新しいに基づいているカスタム テーマを作成する`Style.css`ファイル。  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. 新しいテーマをアクティブ化します。  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

ここで、サインイン ページの下部の著作権を不要になった表示されます。

![著作権情報を削除します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
