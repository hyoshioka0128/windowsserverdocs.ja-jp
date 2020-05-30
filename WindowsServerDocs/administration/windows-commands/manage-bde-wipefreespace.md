---
title: manage-bde wipefreespace 領域
description: Manage-bde wipefreespace 領域内に存在していた可能性のあるデータフラグメントを削除する、ボリューム上の空き領域をワイプするための参照トピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09bc59ab631dd1fa2177b50aa4187b30239571bd
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222123"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde wipefreespace 領域

ボリュームの空き領域を消去し、その領域内に存在していた可能性のあるデータフラグメントを削除します。 **使用領域のみ**の暗号化方法を使用して暗号化されたボリュームでこのコマンドを実行すると、**完全なボリューム暗号化**の暗号化方法と同じレベルの保護が提供されます。

## <a name="syntax"></a>構文

```
manage-bde -wipefreespace|-w [<drive>] [-cancel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -キャンセル | プロセスでは、空き領域のクリーン インストールをキャンセルします。 |
| -computername | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

ドライブ C の空き領域をワイプするには、「\」と入力します。

```
manage-bde -w C:
```

```
manage-bde -wipefreespace C:
```

C ドライブの空き領域のワイプをキャンセルするには、次のように入力します。

```
manage-bde -w -cancel C:
```

```
manage-bde -wipefreespace -cancel C:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
