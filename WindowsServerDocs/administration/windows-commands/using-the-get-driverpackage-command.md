---
title: get DriverPackage
description: サーバー上のドライバーパッケージに関する情報を表示する、get DriverPackage のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4fc6bc327b46f8219a7c40fa47e85cc94b6fc749
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719944"
---
# <a name="get-driverpackage"></a>get DriverPackage

サーバー上のドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                           [説明]                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<サーバー名>] |              サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。               |
| [/Driverpackage:\<名前>] |                                                        表示するドライバー パッケージの名前を指定します。                                                         |
|    [/PackageId:\<ID>]    | 表示するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、ID を指定する必要があります。 |
|     [/Show: {Drivers     |                                                                              ファイル                                                                               |

## <a name="examples"></a>例

ドライバー パッケージについての情報を表示するには、次のいずれかを入力します。
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)