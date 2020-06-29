---
title: print
description: プリンターにテキストファイルを送信する print コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d9cbb4230976572ddd7a26565d616c87ce2ea8d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472317"
---
# <a name="print"></a>print

テキスト ファイルをプリンターに送信します。 ファイルは、ローカル コンピューターのシリアル ポートまたはパラレル ポートに接続されているプリンターに送信する場合、バック グラウンドで印刷できます。

> [!NOTE]
> コマンドプロンプトから多くの構成タスクを実行するには、[[モード] コマンド](mode.md)を使用します。これには、パラレルポートまたはシリアルポートに接続されているプリンターの構成、プリンターの状態の表示、またはコードページ切り替え用のプリンターの準備が含まれます。

## <a name="syntax"></a>構文

```
print [/d:<printername>] [<drive>:][<path>]<filename>[ ...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| d`<printername>` | ジョブを印刷するプリンターを指定します。 ローカルに接続されたプリンターに印刷するには、プリンターが接続されているコンピューターで、ポートを指定します。 パラレルポートの有効な値は、 **LPT1**、 **LPT2**、および**LPT3**です。 シリアルポートの有効な値は、 **COM1**、 **COM2**、 **COM3**、および**COM4**です。 また、キュー名 () を使用して、ネットワークプリンターを指定することもでき `\\server_name\printer_name` ます。 プリンターを指定しない場合、既定で印刷ジョブは**LPT1**に送信されます。 |
| `<drive>`: | 印刷するファイルの場所の論理的または物理的なドライブを指定します。 印刷するファイルが現在のドライブにある場合、このパラメーターは必要ありません。 |
| `<path>` | 印刷するファイルの場所を指定します。 印刷するファイルが現在のディレクトリにある場合、このパラメーターは必要ありません。 |
| `<filename>[ ...]` | 必須です。 印刷するファイルを指定します。 1 つのコマンドでは、複数のファイルを含めることができます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

現在のディレクトリにある**report.txt**ファイルを、ローカルコンピューター上の**lpt2**に接続されているプリンターに送信するには、次のように入力します。

```
print /d:lpt2 report.txt
```

**C:\ アカウンティング**ディレクトリにある**report.txt**ファイルを、 **/d: \\ copyroom**サーバーの**printer1**印刷キューに送信するには、次のように入力します。

```
print /d:\\copyroom\printer1 c:\accounting\report.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)

- [モードコマンド](mode.md)