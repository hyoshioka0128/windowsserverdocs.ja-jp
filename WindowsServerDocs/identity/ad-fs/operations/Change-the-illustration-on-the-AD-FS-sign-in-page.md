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
ms.openlocfilehash: 47a71fffc864f6ae5ecb46d562f92d2d9cece092
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519791"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS サインインページの図を変更する

## <a name="change-the-illustration"></a>図を変更する

サインインページに表示される左側の図を変更するには、 \- 次の Windows PowerShell コマンドレットと構文を使用します。

![図の変更](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> イラストの寸法は 1420x1080 ピクセル (96 DPI) に設定して、ファイル サイズは 200 KB 以下にすることをお勧めします。

```powershell
Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}
```

## <a name="additional-references"></a>その他のリファレンス

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
