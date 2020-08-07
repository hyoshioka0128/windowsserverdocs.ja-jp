---
title: help
description: 使用可能なコマンドの一覧または指定されたコマンドの詳細なヘルプ情報を表示する、ヘルプコマンドの参照記事です。
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b91b93b5ef8964cb73e9bb122f4e53d9d8343086
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888495"
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
