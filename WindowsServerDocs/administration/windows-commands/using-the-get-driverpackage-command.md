---
title: Get DriverPackage コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0f123d281625140b3c4ba46316cb9b773bf5fee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440509"
---
# <a name="using-the-get-driverpackage-command"></a>Get DriverPackage コマンドを使用してください。



サーバー上のドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                           説明                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<サーバー名 >] |              サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。               |
| [/DriverPackage:\<Name>] |                                                        表示するドライバー パッケージの名前を指定します。                                                         |
|    [/PackageId:\<ID>]    | 表示するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、ID を指定する必要があります。 |
|     [/Show: {ドライバー     |                                                                              ファイル                                                                               |

## <a name="BKMK_examples"></a>例

ドライバー パッケージについての情報を表示するには、次のいずれかを入力します。
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)