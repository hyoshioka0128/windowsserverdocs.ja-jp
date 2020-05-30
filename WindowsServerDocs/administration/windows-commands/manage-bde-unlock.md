---
title: manage-bde のロック解除
description: 復元パスワードまたは回復キーを使用して BitLocker で保護されているドライブのロックを解除する manage-bde unlock コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67d4c0ec78870af45f0b98f2ab04d85b19e92af9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222155"
---
# <a name="manage-bde-unlock"></a>manage-bde のロック解除

回復パスワードまたは回復キーを使用して BitLocker で保護されたドライブのロックを解除します。

## <a name="syntax"></a>構文

```
manage-bde -unlock {-recoverypassword <password>|-recoverykey <pathtoexternalkeyfile>} <drive> [-certificate {-cf pathtocertificatefile | -ct certificatethumbprint} {-pin}] [-password] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -recoverypassword | 回復パスワードを使用してドライブのロックを解除することを指定します。 また、 **-rp**をこのコマンドの省略版として使用することもできます。 |
| `<password>` | ドライブのロックを解除するために使用する回復パスワードを表します。 |
| -recoverykey | 外部の回復キー ファイルがドライブのロック解除に使用されることを指定します。 このコマンドの省略版として **-rk**を使用することもできます。 |
| `<pathtoexternalkeyfile>` | ドライブのロックを解除するために使用される、外部の回復キー ファイルを表します。 |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -証明書 | ボリュームのロックを解除する BitLocker 証明書のローカルユーザー証明書は、ローカルユーザーの証明書ストアにあります。 使用することも **-cert** としてこのコマンドの簡易版です。 |
| -cf`<pathtocertificatefile>` | 証明書ファイルへのパス |
| -ct`<certificatethumbprint>` | 必要に応じて、暗証番号 (pin) を含む証明書の拇印 (の暗証番号 (pin))。 |
| -パスワード | ボリュームのロックを解除するパスワードを入力するプロンプトが表示されます。 使用することも **- pw** としてこのコマンドの簡易版です。 |
| -computername | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

別のドライブのバックアップフォルダーに保存されている回復キーファイルを使用してドライブ E のロックを解除するには、次のように入力します。

```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
