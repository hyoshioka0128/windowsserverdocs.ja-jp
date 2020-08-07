---
title: reg
description: レジストリエントリのレジストリサブキーの情報と値に対する操作を実行する reg コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: c97496b2-d1ff-4887-b5d2-6e1524be465a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18a9f243001758393597f6cc5803dd42cdc32dae
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883970"
---
# <a name="reg"></a>reg

レジストリ エントリをレジストリ サブキー情報と値に対して操作を実行します。

一部の操作では、ローカルコンピューターまたはリモートコンピューター上のレジストリエントリを表示または構成できますが、他の操作ではローカルコンピューターのみを構成できます。 使用して **reg** コンピューターをリモート レジストリを構成するには、制限の一部の操作で使用できるパラメーターです。 各操作の構文とパラメーターを確認して、リモートコンピューターで使用できることを確認します。

> [!CAUTION]
> 代替手段がなければ、レジストリを直接編集しないでください。 レジストリエディターでは、標準のセーフガードがバイパスされるため、パフォーマンスを低下させたり、システムに損害を与えたり、Windows の再インストールが必要になることもあります。 ほとんどのレジストリ設定は、コントロールパネルまたは Microsoft 管理コンソール (MMC) のプログラムを使用して、安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。

## <a name="syntax"></a>構文

```
reg add
reg compare
reg copy
reg delete
reg export
reg import
reg load
reg query
reg restore
reg save
reg unload
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| [reg add](reg-add.md) | 新しいサブキーまたはエントリをレジストリに追加します。 |
| [reg compare](reg-compare.md) | 比較では、レジストリ サブキーまたはエントリを指定します。 |
| [reg copy](reg-copy.md) | ローカルまたはリモート コンピューター上の指定の場所にレジストリ エントリをコピーします。 |
| [reg delete](reg-delete.md) | レジストリからサブキーまたはエントリを削除します。 |
| [reg export](reg-export.md) | 他のサーバーに転送するためのファイルに指定されたサブキー、エントリ、およびローカル コンピューターの値をコピーします。 |
| [reg import](reg-import.md) | コピーを含むファイルの内容は、ローカル コンピューターのレジストリにレジストリ キー、エントリ、および値をエクスポートします。 |
| [reg load](reg-load.md) | 書き込みは、サブキーと別のサブキーにエントリをレジストリに保存します。 |
| [reg query](reg-query.md) | 次の層のサブキーと、レジストリで指定したサブキーの下にあるエントリの一覧を返します。 |
| [reg restore](reg-restore.md) | 書き込みが保存されたサブキーとエントリは、レジストリをバックアップします。 |
| [reg save](reg-save.md) | 指定したファイルで指定されたサブキー、エントリ、およびレジストリの値のコピーを保存します。 |
| [reg unload](reg-unload.md) | レジストリを使用して既に読み込まれているセクションを削除、 **reg ロード** 操作します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
