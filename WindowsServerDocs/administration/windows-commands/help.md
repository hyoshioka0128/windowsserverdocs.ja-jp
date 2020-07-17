---
title: help
description: 使用可能なコマンドの一覧または指定されたコマンドの詳細なヘルプ情報を表示する、ヘルプコマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 562bb725998cb58eb9a4a9ce9078a833bc0e7781
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924571"
---
# <a name="help"></a>help

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用可能なコマンドの一覧、または指定したコマンドの詳細なヘルプ情報を表示します。 パラメーターを指定せずに使用する場合は、すべてのシステムコマンドについての説明と**ヘルプ**が表示されます。

## <a name="syntax"></a>構文

```
help [<command>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<command>` | 詳細なヘルプ情報を表示するコマンドを指定します。 |

### <a name="examples"></a>例

**Robocopy**コマンドに関する情報を表示するには、次のように入力します。

```
help robocopy
```

DiskPart で使用可能なすべてのコマンドの一覧を表示するには、次のように入力します。

```
help
```

DiskPart で**create partition primary**コマンドを使用する方法に関する詳細なヘルプ情報を表示するには、次のように入力します。

```
help create partition primary
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
