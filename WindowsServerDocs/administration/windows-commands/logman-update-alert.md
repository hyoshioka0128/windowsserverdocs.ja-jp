---
title: logman update alert
description: 既存のアラートデータコレクターのプロパティを更新する logman 更新アラートコマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84e198ef528d1f9192662ed89ad39b6884fab742
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932276"
---
# <a name="logman-update-alert"></a>logman update alert

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のアラートデータコレクターのプロパティを更新します。

## <a name="syntax"></a>構文

```
logman update alert <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -s`<computer name>` | 指定したリモートコンピューターでコマンドを実行します。 |
| -config`<value>` | コマンドオプションを含む設定ファイルを指定します。 |
| [-n]`<name>` | 対象オブジェクトの名前。 |
| -[-] u`<user [password]>` | として実行するユーザーを指定します。 パスワードのを入力すると、パスワードの入力を `*` 求めるメッセージが表示されます。 パスワードは、パスワード用プロンプトで入力した場合は表示されません。 |
| -m`<[start] [stop] [[start] [stop] [...]]>` | スケジュールされた開始時刻または終了時刻ではなく、手動で開始または停止するように変更します。 |
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
| -[-] my.cnf`<[[hh:]mm:]ss>` | 時間を指定すると、指定した時間が経過すると新しいファイルが作成されます。 時間が指定されていない場合は、最大サイズを超えたときに、によって新しいファイルが作成されます。 |
| -y | プロンプトを表示せずにすべての質問に対する回答を表示します。 |
| -cf`<filename>` | 収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。 |
| -[-] el | イベントログレポートを有効または無効にします。 |
| -th`<threshold [threshold [...]]>` | 警告のカウンターとそのしきい値を指定します。 |
| -[-] rdcs`<name>` | 警告が発生したときに開始するデータコレクターセットを指定します。 |
| -[-] tn`<task>` | 警告が発生したときに実行するタスクを指定します。 |
| -[-] targ`<argument>` | -Tn を使用して指定されたタスクで使用されるタスク引数を指定します。 |
| /? | 状況依存のヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- [-] が一覧表示されている場合は、余分なハイフン (-) を追加すると、オプションが無効になります。

### <a name="examples"></a>例

*New_alert*という名前の既存のアラートを更新するには、processor (_Total) カウンタグループのカウンタ% Processor time のしきい値を40% に設定し、次のように入力します。

```
logman update alert new_alert -th \Processor(_Total)\% Processor time>40
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman 作成アラートコマンド](logman-create-alert.md)

- [logman コマンド](logman.md)
