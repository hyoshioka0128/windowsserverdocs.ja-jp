---
title: irftp
description: Irftp コマンドのリファレンストピック。赤外線リンク経由でファイルを送信します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d19e4f0c325baf46c0a92bf04e39bc63863fe90
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818312"
---
# <a name="irftp"></a>irftp

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

赤外線リンクを介してファイルを送信します。

> [!IMPORTANT]
> 赤外線リンクを経由した通信用のデバイスが赤外線機能を有効にし、正常に動作していることを確認します。 また、デバイス間に赤外線リンクが確立されていることを確認します。

## <a name="syntax"></a>構文

```
irftp [<drive>:\] [[<path>] <filename>] [/h][/s]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>:\` | 赤外線リンクを介して送信するファイルが格納されているドライブを指定します。 |
| `[path]<filename>` | 赤外線リンクを介して送信するファイルまたはファイルのセットの場所と名前を指定します。 ファイルのセットを指定する場合は、各ファイルの完全なパスを指定する必要があります。 |
| /h | 非表示モードを指定します。 非表示モードを使用すると、[ワイヤレスリンク] ダイアログボックスを表示せずにファイルが送信されます。 |
| /s | [**ワイヤレスリンク**] ダイアログボックスを開きます。これにより、コマンドラインを使用せずに、ドライブ、パス、およびファイル名を指定して、送信するファイルまたはファイルのセットを選択できます。 パラメーターを指定せずにこのコマンドを使用すると、[**ワイヤレスリンク**] ダイアログボックスも開きます。 |

### <a name="examples"></a>例

赤外線リンク経由で*c:\example.txt*を送信するには、次のように入力します。

```
irftp c:\example.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
