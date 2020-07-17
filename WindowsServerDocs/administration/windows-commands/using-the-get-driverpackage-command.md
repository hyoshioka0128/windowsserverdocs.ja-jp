---
title: get DriverPackage
description: サーバー上のドライバーパッケージに関する情報を表示する、get DriverPackage のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0ca307b9f42d0921c896df2fe622c5b0f8a853d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932253"
---
# <a name="get-driverpackage"></a>get DriverPackage

サーバー上のドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                           説明                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server name>] |              サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。               |
| [/DriverPackage:\<Name>] |                                                        表示するドライバー パッケージの名前を指定します。                                                         |
|    [/パッケージ Id:\<ID>]    | 表示するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、ID を指定する必要があります。 |
|     [/Show: {Drivers     |                                                                              Files                                                                               |

## <a name="examples"></a>例

ドライバー パッケージについての情報を表示するには、次のいずれかを入力します。
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)