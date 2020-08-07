---
title: reg unload
description: Reg unload コマンドの参照記事。 reg 読み込み操作を使用して読み込まれたレジストリのセクションを削除します。
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d2ea6f5981ea613ae5e0d9d4dcae155464b505a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883985"
---
# <a name="reg-unload"></a>reg unload

レジストリを使用して既に読み込まれているセクションを削除、 **reg ロード** 操作します。

## <a name="syntax"></a>構文

```
reg unload <keyname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname>` | サブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **Reg アンロード**操作の戻り値は次のとおりです。

    | 値 | 説明 |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

## <a name="examples"></a>例

TempHive ファイル HKLM ハイブをアンロードするには、次のように入力します。

```
reg unload HKLM\TempHive
```

> [!CAUTION]
> 代替手段がなければ、レジストリを直接編集しないでください。 レジストリエディターでは、標準のセーフガードがバイパスされるため、パフォーマンスを低下させたり、システムに損害を与えたり、Windows の再インストールが必要になることもあります。 ほとんどのレジストリ設定は、コントロールパネルまたは Microsoft 管理コンソール (MMC) のプログラムを使用して、安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [reg load コマンド](reg-load.md)
