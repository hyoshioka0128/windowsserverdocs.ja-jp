---
title: logman 更新トレース
description: 既存のイベントトレースデータコレクターのプロパティを更新する logman update トレースコマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7111f7f-4162-4d1a-8e53-d766db0ede1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9edb8df5d5d7e2f3c3f1ccf17fbd817efe4faa10
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222751"
---
# <a name="logman-update-trace"></a>logman 更新トレース

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のイベントトレースデータコレクターのプロパティを更新します。

## <a name="syntax"></a>構文

```
logman update trace <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -s`<computer name>` | 指定されたリモートコンピューターでコマンドを実行します。 |
| -config`<value>` | コマンドオプションを含む設定ファイルを指定します。 |
| -/ | イベントトレースセッションに直接コマンドを送信します。保存もスケジュールもされません。 |
| [-n]`<name>` | 対象オブジェクトの名前。 |
| -f`<bin|bincirc>` | データコレクターのログの形式を指定します。 |
| -[-] u`<user [password]>` | として実行するユーザーを指定します。 パスワードのを入力すると、パスワードの入力を `*` 求めるメッセージが表示されます。 パスワードは、パスワード用プロンプトで入力した場合は表示されません。 |
| -m`<[start] [stop] [[start] [stop] [...]]>` | スケジュールされた開始時刻または終了時刻ではなく、手動で開始または停止するように変更します。 |
| -rf`<[[hh:]mm:]ss>` | 指定した期間だけデータコレクターを実行します。 |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時間にデータの収集を開始します。 |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時間にデータ収集を終了します。 |
| -o`<path|dsn!log>` | SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。 |
| -[-] r | 指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。 |
| -[-] a | 既存のログファイルを追加します。 |
| -[-] o | 既存のログファイルを上書きします。 |
| -[-] v`<nnnnnn|mmddhhmm>` | ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。 |
| -[-] rc`<task>` | ログが閉じられるたびに、指定されたコマンドを実行します。 |
| -[-] 最大`<value>` | SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。 |
| -[-] my.cnf`<[[hh:]mm:]ss>` | 時間を指定すると、指定した時間が経過すると新しいファイルが作成されます。 時間が指定されていない場合は、最大サイズを超えたときに、によって新しいファイルが作成されます。 |
| -y | プロンプトを表示せずにすべての質問に対する回答を表示します。 |
| -ct`<perf|system|cycle>` | イベントトレースセッションのクロックの種類を指定します。 |
| -ln`<logger_name>` | イベントトレースセッションのロガー名を指定します。 |
| -ft`<[[hh:]mm:]ss>` | イベントトレースセッションのフラッシュタイマーを指定します。 |
| -[-] p`<provider [flags [level]]>` | 有効にする1つのイベントトレースプロバイダーを指定します。 |
| -pf`<filename>` | 有効にする複数のイベントトレースプロバイダーを一覧表示するファイルを指定します。 ファイルは、1行に1つのプロバイダーを含むテキストファイルである必要があります。 |
| -[-] rt | イベントトレースセッションをリアルタイムモードで実行します。 |
| -[-] ul | ユーザーのイベントトレースセッションを実行します。 |
| -bs`<value>` | イベントトレースセッションのバッファーサイズを kb 単位で指定します。 |
| -nb`<min max>` | イベントトレースセッションバッファーの数を指定します。 |
| -モード`<globalsequence|localsequence|pagedmemory>` | イベントトレースセッションロガーモードを次のように指定します。<ul><li>**Globalsequence** -イベントトレーサーは、イベントを受信したトレースセッションに関係なく、受信したすべてのイベントにシーケンス番号を追加します。</li><li>**Localsequence** -イベントトレーサーが特定のトレースセッションで受信したイベントのシーケンス番号を追加することを指定します。 このオプションを使用すると、すべてのセッションで重複するシーケンス番号が存在する可能性がありますが、各トレースセッション内で一意になります。</li><li>**Pagedmemory** -イベントトレーサーが、既定の非ページメモリプールではなく、ページングされたメモリを内部バッファー割り当てに使用することを指定します。</li></ul> |
| /? | 状況依存のヘルプを表示します。 |

#### <a name="remarks"></a>解説

- [-] が一覧表示されている場合は、余分なハイフン (-) を追加すると、オプションが無効になります。

### <a name="examples"></a>例

*Trace_log*という既存のイベントトレースデータコレクターを更新するには、ログの最大サイズを 10 MB に変更し、ログファイルの形式を CSV に更新して、ファイルのバージョン管理を mmddhhmm の形式で追加します。次のように入力します。

```
logman update trace trace_log -max 10 -f csv -v mmddhhmm
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman 作成トレースコマンド](logman-create-trace.md)

- [logman コマンド](logman.md)
