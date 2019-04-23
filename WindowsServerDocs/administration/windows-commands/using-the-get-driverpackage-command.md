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
ms.openlocfilehash: 6574177f1f0a8ead0cc2fa596380eb2c980f8d1f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888523"
---
# <a name="using-the-get-driverpackage-command"></a>Get DriverPackage コマンドを使用してください。



サーバー上のドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/DriverPackage:\<Name>]|表示するドライバー パッケージの名前を指定します。|
|[/PackageId:\<ID>]|表示するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、ID を指定する必要があります。|
|[/Show: {ドライバー | ファイル | All}]|(指定した場合) を表示するには、どのような情報を示します。 場合 **/show** が指定されていない、既定では、パッケージ メタデータ ドライバーのみを返します。 **ドライバー** パッケージのすべてのドライバーが表示されます。 **ファイル** パッケージにファイルの一覧が表示されます。 **すべて** ドライバー、ファイル、およびメタデータが表示されます。|

## <a name="BKMK_examples"></a>例

ドライバー パッケージについての情報を表示するには、次のいずれかを入力します。
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)