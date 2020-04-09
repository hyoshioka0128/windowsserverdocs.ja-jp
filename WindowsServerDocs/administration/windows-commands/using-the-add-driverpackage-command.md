---
title: 追加 DriverPackage
description: ドライバーパッケージをサーバーに追加する追加 DriverPackage の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2ccdfcddd2f605eccd9cd32fed7b8c6921297fc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832015"
---
# <a name="add-driverpackage"></a>追加 DriverPackage

ドライバー パッケージをサーバーに追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>パラメーター

|          パラメーター           |                                                              説明                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile:\<Inf ファイルのパス >   |                                           追加する .inf ファイルの完全なパスを指定します。                                            |
|    /Server:\<サーバー名 >    | サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。 |
|      /アーキテクチャ: {x86      |                                                                 ia64                                                                  |
| [/Drivergroup:\<グループ名 >] |                             パッケージの追加先となるドライバー グループの名前を指定します。                              |
|   [/Name:\<のフレンドリ名 >]   |                                           ドライバー パッケージのフレンドリ名を示しています。                                            |

## <a name="examples"></a><a name=BKMK_examples></a>例

ドライバー パッケージを追加するには、次のいずれかを入力します。
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

