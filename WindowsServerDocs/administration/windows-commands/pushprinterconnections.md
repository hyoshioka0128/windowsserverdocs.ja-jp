---
title: pushprinterconnections
description: Pushprinter connections コマンドのリファレンストピックです。このコマンドは、展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開/削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 701089f2597b1d4e7bc05f7949dbc80dee3535bb
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472127"
---
# <a name="pushprinterconnections"></a>pushprinterconnections

展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開または削除します。

> [!IMPORTANT]
> このユーティリティは、コンピューターのスタートアップまたはユーザーのログオンスクリプトで使用するためのものであり、コマンドラインから実行しないでください。

## <a name="syntax"></a>構文

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| <-ログ > | ユーザーごとのデバッグログファイルを *% temp*に書き込みます。または、コンピューターごとのデバッグログを *%windir%\temp*に書き込みます。 |
| <-? > | コマンド プロンプトでヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)

- [グループ ポリシーを使用してプリンターを展開します。](https://go.microsoft.com/fwlink/?LinkId=230627)
