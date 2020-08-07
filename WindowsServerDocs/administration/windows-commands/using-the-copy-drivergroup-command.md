---
title: コピー DriverGroup
description: フィルター、ドライバーパッケージ、有効/無効の状態を含む、サーバー上の既存のドライバーグループを複製する、コピー DriverGroup の参照記事。
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff36f3761be0a4cd772e287a3e672fd07f2d4f02
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896551"
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