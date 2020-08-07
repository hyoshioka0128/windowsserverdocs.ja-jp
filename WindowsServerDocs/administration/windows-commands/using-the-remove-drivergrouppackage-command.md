---
title: 削除 DriverGroupPackage
description: 削除 DriverGroupPackage に関するリファレンス記事。サーバー上のドライバーグループからドライバーパッケージを削除します。
ms.topic: article
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a677204f593c5c9b791d0e68f726cc75c6f94764
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892400"
---
# <a name="remove-drivergrouppackage"></a>削除 DriverGroupPackage



サーバー上のドライバー グループからドライバー パッケージを削除します。

## <a name="syntax"></a>構文

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[/Server:\<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/DriverPackage:\<Name>]|削除するドライバー パッケージの名前を指定します。|
|[/パッケージ Id:\<ID>]|削除するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。|

## <a name="examples"></a>例

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)