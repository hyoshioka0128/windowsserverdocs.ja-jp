---
title: コピー DriverGroup
description: フィルター、ドライバーパッケージ、有効/無効の状態を含む、サーバー上の既存のドライバーグループを複製する、コピー DriverGroup の参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d9be90f065cc76e16b7b45135c60b5206c7bf581
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934082"
---
# <a name="copy-drivergroup"></a>コピー DriverGroup

フィルター、ドライバー パッケージ、および有効/無効状態を含む、サーバー上の既存のドライバー グループを複製します。

## <a name="syntax"></a>構文

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[/Server:\<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|DriverGroup\<Source Group Name>|ソースのドライバー グループの名前を指定します。|
|GroupName\<New Group Name>|新しいドライバー グループの名前を指定します。|

## <a name="examples"></a>例

ドライバー グループをコピーするには、次のいずれかを入力します。
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)