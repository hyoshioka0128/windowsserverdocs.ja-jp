---
title: 追加 AllDriverPackages サブコマンドを使用します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f934d8c65da939fb60c564b375699f411b7c9ac
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440837"
---
# <a name="using-the-add-alldriverpackages-subcommand"></a>追加 AllDriverPackages サブコマンドを使用します。



サーバーにフォルダーに格納されているすべてのドライバー パッケージを追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

## <a name="parameters"></a>パラメーター

|          パラメーター           |                                                              説明                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  /FolderPath:\<フォルダーのパス >  |                      ドライバ パッケージの .inf ファイルを含むフォルダーへの完全パスを指定します。                      |
|   [/Server:\<サーバー名 >]   | サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。 |
|     [/アーキテクチャ: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<グループ名 >] |                             パッケージの追加先となるドライバー グループの名前を指定します。                             |

## <a name="BKMK_examples"></a>例

ドライバー パッケージを追加するには、次のいずれかを入力します。
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers" /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers\Printers" /DriverGroup:"Printer Drivers"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Add-WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)