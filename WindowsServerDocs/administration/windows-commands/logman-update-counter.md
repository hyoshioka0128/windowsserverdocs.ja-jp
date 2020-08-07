---
title: logman update counter
description: 既存のカウンターデータコレクターのプロパティを更新する logman update カウンターコマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 607df6d5-876c-428d-a0b3-f59cb244e2ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53f6bd33e73c469960e99acddc044d0afea55dc7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887185"
---
# <a name="logman-update-counter"></a>logman update counter

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のカウンターデータコレクターのプロパティを更新します。

## <a name="syntax"></a>構文

```
logman update counter <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター


| パラメーター | 説明 |
| --------- | ----------- |
| -s `<computer name>` | 指定したリモートコンピューターでコマンドを実行します。 |
| -config`<value>` | コマンドオプションを含む設定ファイルを指定します。 |
| [-n]`<name>` | 対象オブジェクトの名前。 |
| -f`<bin|bincirc>` | データコレクターのログの形式を指定します。 |
| -[-] u`<user [password]>` | として実行するユーザーを指定します。 パスワードのを入力すると、パスワードの入力を `*` 求めるメッセージが表示されます。 パスワードは、パスワード用プロンプトで入力した場合は表示されません。 |
| -m `<[start] [stop] [[start] [stop] [...]]>` | スケジュールされた開始時刻または終了時刻ではなく、手動で開始または停止するように変更します。 |
| -rf`<[[hh:]mm:]ss>` | 指定した期間だけデータコレクターを実行します。 |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時間にデータの収集を開始します。 |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時間にデータ収集を終了します。 |
| -si`<[[hh:]mm:]ss>` | パフォーマンスカウンターデータコレクターのサンプル間隔を指定します。 |
| -o`<path|dsn!log>` | SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。 |
| -[-] r | 指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。 |
| -[-] a | 既存のログファイルを追加します。 |
| -[-] o | 既存のログファイルを上書きします。 |
| -[-] v`<nnnnnn|mmddhhmm>` | ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。 |
| -[-] rc`<task>` | ログが閉じられるたびに、指定されたコマンドを実行します。 |
| -[-] 最大`<value>` | SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。 |
| -[-] my.cnf`<[[hh:]mm:]ss>` | 時間を指定した場合は、指定した時間が経過した時点で新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。 |
| -y | プロンプトを表示せずにすべての質問に対する回答を表示します。 |
| -cf`<filename>` | 収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。 |
| -c`<path [path [ ]]>` | 収集するパフォーマンスカウンターを指定します。 |
| -sc`<value>` | パフォーマンスカウンターデータコレクターを使用して収集するサンプルの最大数を指定します。 |
| /? | 状況依存のヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- [-] が一覧表示されている場合は、余分なハイフン (-) を追加すると、オプションが無効になります。

### <a name="examples"></a>例

プロセッサ (_Total) カウンターカテゴリの% Processor time カウンターを使用して*perf_log*というカウンターを作成するには、次のように入力します。

```
logman create counter perf_log -c \Processor(_Total)\% Processor time
```

*Perf_log*という名前の既存のカウンターを更新するには、サンプル間隔を10に変更し、ログ形式を CSV に、mmddhhmm の形式でログファイル名にバージョン管理を追加して、次のように入力します。

```
logman update counter perf_log -si 10 -f csv -v mmddhhmm
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman カウンターの作成コマンド](logman-create-counter.md)

- [logman コマンド](logman.md)
