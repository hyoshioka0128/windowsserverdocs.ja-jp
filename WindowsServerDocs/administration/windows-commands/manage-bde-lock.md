---
title: manage-bde ロック
description: Manage-bde ロックコマンドのリファレンス記事。ロック解除キーが指定されていない場合、BitLocker で保護されているドライブをロックして、アクセスを防止します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8858e61-3a7e-4d03-8c98-5c09853f35e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b67342579c827ad195ddf506e529fbfb370a6d94
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931623"
---
# <a name="manage-bde-lock"></a>manage-bde ロック

BitLocker で保護されているドライブをロックして、ロック解除キーが指定されていない限り、アクセスできないようにします。

## <a name="syntax"></a>構文

```
manage-bde -lock [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

データドライブ D をロックするには、次のように入力します。

```
manage-bde –lock D:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
