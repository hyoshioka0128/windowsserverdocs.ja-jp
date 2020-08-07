---
title: logman create api
description: Logman create api コマンドのリファレンス記事。 API トレースデータコレクターを作成します。
ms.topic: article
ms.assetid: 2ecc0a75-2613-464a-8616-c5dc404bb736
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2e3e9291bcd113ced9c27eb7cc3449f715f9893
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887455"
---
# <a name="logman-create-api"></a>logman create api

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

API トレースデータコレクターを作成します。

## <a name="syntax"></a>構文

```
logman create api <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -s `<computer name>` | 指定されたリモートコンピューターでコマンドを実行します。 |
| -config`<value>` | コマンドオプションを含む設定ファイルを指定します。 |
| [-n]`<name>` | 対象オブジェクトの名前。 |
| -f`<bin|bincirc>` | データコレクターのログの形式を指定します。 |
| -[-] u`<user [password]>` | として実行するユーザーを指定します。 パスワードのを入力すると、パスワードの入力を `*` 求めるメッセージが表示されます。 パスワードは、パスワード用プロンプトで入力した場合は表示されません。 |
| -m `<[start] [stop] [[start] [stop] [...]]>` | スケジュールされた開始時刻または終了時刻ではなく、手動の開始または停止に変更されました。 |
| -rf`<[[hh:]mm:]ss>` | 指定された期間、データコレクターを実行します。 |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時間にデータの収集を開始します。 |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | 指定された時刻にデータ収集を終了します。 |
| -si`<[[hh:]mm:]ss>` | パフォーマンスカウンターデータコレクターのサンプル間隔を指定します。 |
| -o`<path|dsn!log>` | SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。 |
| -[-] r | 指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。 |
| -[-] a | 既存のログファイルを追加します。 |
| -[-] o | 既存のログファイルを上書きします。 |
| -[-] v`<nnnnnn|mmddhhmm>` | ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。 |
| -[-] rc`<task>` | ログが閉じられるたびに、指定されたコマンドを実行します。 |
| -[-] 最大`<value>` | SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。 |
| -[-] my.cnf`<[[hh:]mm:]ss>` | 時間を指定すると、指定した時間が経過すると新しいファイルが作成されます。 時間が指定されていない場合は、最大サイズを超えたときに、によって新しいファイルが作成されます。 |
| -y | 確認を求めずにすべての質問に対して [はい] を回答します。 |
| -mods`<path [path [...]]>` | API 呼び出しのログを記録するモジュールの一覧を指定します。 |
| -inapis` <module!api [module!api [...]]>` | ログに記録する API 呼び出しの一覧を指定します。 |
| -exapis`<module!api [module!api [...]]>` | ログから除外する API 呼び出しの一覧を指定します。 |
| -[-] ano | Log (-ano) API 名のみ、またはログのみ (-ano) API 名をログに記録します。 |
| -[-] recursive | ログ (-recursive) を実行するか、最初のレイヤーを越えて再帰的に Api をログに記録しないようにします。 |
| -exe`<value>` | API トレースの実行可能ファイルへの完全パスを指定します。 |
| /? | 状況依存のヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- [-] が一覧表示されている場合は、余分なハイフン (-) を追加すると、オプションが無効になります。

### <a name="examples"></a>例

実行可能ファイル c:\windows\notepad.exe に対して trace_notepad という API トレースカウンターを作成し、結果をファイル c:\notepad.etl に格納するには、次のように入力します。

```
logman create api trace_notepad -exe c:\windows\notepad.exe -o c:\notepad.etl
```

Trace_notepad という API トレースカウンターを作成するには、実行可能ファイル c:\windows\notepad.exe に対して、c:\windows\system32\advapi32.dll でモジュールによって生成された値を収集するために、次のように入力します。

```
logman create api trace_notepad -exe c:\windows\notepad.exe -mods c:\windows\system32\advapi32.dll
```

モジュール kernel32.dll によって生成された API 呼び出し TlsGetValue を除く、実行可能ファイル c:\windows\notepad.exe に対して trace_notepad という API トレースカウンターを作成するには、次のように入力します。
```
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman 更新 api コマンド](logman-update-api.md)

- [logman コマンド](logman.md)
