---
title: manage-bde forcerecovery
description: BitLocker で保護されたドライブを再起動時に強制的に復旧モードにする manage-bde forcerecovery コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 407ec574c66c057664d517bda35b82da908e0291
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886883"
---
# <a name="manage-bde-forcerecovery"></a>manage-bde forcerecovery

再起動時に復旧モードに BitLocker で保護されたドライブを強制します。 このコマンドは、すべてのトラステッドプラットフォームモジュール (TPM) 関連のキー保護機能をドライブから削除します。 コンピューターが再起動したら、回復パスワードまたは回復キーは、ドライブのロック解除に使用できます。

## <a name="syntax"></a>構文

```
manage-bde –forcerecovery <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

BitLocker がドライブ C の回復モードで起動するようにするには、次のように入力します。

```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
