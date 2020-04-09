---
title: コピー DriverGroup
description: Windows コマンドのトピック。コピー DriverGroup は、フィルター、ドライバーパッケージ、有効/無効の状態など、サーバー上の既存のドライバーグループを複製します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 277903150a25555b03b51c980436250656c597b1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831735"
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
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/Drivergroup:\<ソースグループ名 >|ソースのドライバー グループの名前を指定します。|
|/GroupName:\<新しいグループ名 >|新しいドライバー グループの名前を指定します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

ドライバー グループをコピーするには、次のいずれかを入力します。
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)