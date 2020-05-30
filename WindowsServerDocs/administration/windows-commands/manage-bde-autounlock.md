---
title: manage-bde 自動ロック解除
description: BitLocker で保護されたデータドライブの自動ロック解除を管理する manage-bde 自動ロック解除コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a214ba868e04a81e6282dc919c93ab626ef26725
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223003"
---
# <a name="manage-bde-autounlock"></a>manage-bde 自動ロック解除

BitLocker で保護されたデータ ドライブの自動ロック解除を管理します。

## <a name="syntax"></a>構文

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -を有効にします。 | データ ドライブの自動ロック解除を使用できます。 |
| -を無効にします。 | データ ドライブの自動ロック解除を無効にします。 |
| -clearallkeys | オペレーティング システム ドライブに格納されているすべての外部キーを削除します。 |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -computername | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

## <a name="examples"></a>例

データドライブ E の自動ロック解除を有効にするには、次のように入力します。

```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)