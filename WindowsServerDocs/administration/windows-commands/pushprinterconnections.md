---
title: pushprinterconnections
description: Pushprinter connections コマンドの参照記事。このコマンドは、展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開または削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b22fd5143a9477b40a515df44c9a0b5663dfd7a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931387"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)

- [グループ ポリシーを使用してプリンターを展開します。](https://go.microsoft.com/fwlink/?LinkId=230627)
