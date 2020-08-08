---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: AD FS サインインページで会社のロゴを変更する
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.openlocfilehash: bc5bf9dcd0277980144d367e0bc539b555c05c83
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956649"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>AD FS サインインページで会社のロゴを変更する

## <a name="change-company-logo"></a>会社ロゴの変更

サインインページに表示される会社のロゴを変更するには \- 、次の Powershell Windows powershell コマンドレットと構文を使用します。

![ロゴの変更](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> ロゴの寸法は 260x35 ピクセル (96 DPI) に設定して、ファイル サイズは 10 KB 以下にすることをお勧めします。

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}
```

> [!NOTE]
> `TargetName` パラメーターは必須です。 AD FS と共にリリースされる既定のテーマには、 *default*という名前が付けられます。

## <a name="additional-references"></a>その他の参照情報

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
