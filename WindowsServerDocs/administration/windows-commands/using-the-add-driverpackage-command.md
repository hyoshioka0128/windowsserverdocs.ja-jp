---
title: 追加 DriverPackage コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 893bcd3b28aaa5d501017fe65b7b5205e9452693
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440692"
---
# <a name="using-the-add-driverpackage-command"></a>追加 DriverPackage コマンドを使用してください。



ドライバー パッケージをサーバーに追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

## <a name="parameters"></a>パラメーター

|          パラメーター           |                                                              説明                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile:\<Inf ファイルのパス >   |                                           追加する .inf ファイルの完全なパスを指定します。                                            |
|    /Server:\<サーバー名 >    | サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。 |
|      /アーキテクチャ: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<グループ名 >] |                             パッケージの追加先となるドライバー グループの名前を指定します。                              |
|   [/Name:\<フレンドリ名 >]   |                                           ドライバー パッケージのフレンドリ名を示しています。                                            |

## <a name="BKMK_examples"></a>例

ドライバー パッケージを追加するには、次のいずれかを入力します。
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:"C:\Temp\Display.inf"
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:"C:\Temp\Display.inf" /Architecture:x86 /DriverGroup:x86Drivers /Name:"Display Driver"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

