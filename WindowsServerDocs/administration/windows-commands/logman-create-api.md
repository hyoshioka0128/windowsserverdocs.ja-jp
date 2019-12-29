---
title: logman api の作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ecc0a75-2613-464a-8616-c5dc404bb736
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 512602213fcfd95770af0e27b721a589ed489771
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374603"
---
# <a name="logman-create-api"></a>logman api の作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

API トレースデータコレクターを作成します。  

## <a name="syntax"></a>構文  
```  
logman create api <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|                    パラメーター                     |                                                                               説明                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    状況依存のヘルプを表示します。                                                                     |
|                -s <computer name>                |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|                 -config <value>                  |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|                   [-n] <name>                    |                                                                       ターゲットオブジェクトの名前。                                                                        |
| -f < ビン&#124;ビン circ&#124;csv&#124;tsv&#124;sql > |                                                            データコレクターのログの形式を指定します。                                                             |
|             -[-] u < ユーザー [パスワード] >              | として実行するユーザーを指定します。 パスワードの \* を入力すると、パスワードの入力を求めるプロンプトが生成されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
|    -m < [開始] [停止] [[開始] [停止] [...]]>    |                                                スケジュールされた開始時刻または終了時刻ではなく、手動の開始または停止に変更します。                                                 |
|                -rf < [[hh:] mm:] ss >                |                                                        指定された期間、データコレクターを実行します。                                                         |
|        -b < M/d/yyyy h:mm: ss [AM&#124;PM] >         |                                                              指定された時間にデータの収集を開始します。                                                               |
|        -e < M/d/yyyy h:mm: ss [AM&#124;PM] >         |                                                               指定された時刻にデータ収集を終了します。                                                                |
|                -si < [[hh:] mm:] ss >                |                                                 パフォーマンスカウンターデータコレクターのサンプル間隔を指定します。                                                  |
|              -o < path&#124;dsn! ログ >              |                                              SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。                                               |
|                      -[-] r                       |                                                  指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。                                                  |
|                      -[-] a                       |                                                                     既存のログファイルに追加します。                                                                     |
|                      -[-] o                      |                                                                     既存のログファイルを上書きします。                                                                     |
|           -[-] v < nnnnnn&#124;mmddhhmm >           |                                                   ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。                                                   |
|                  -[-] rc <task>                   |                                                         ログが閉じられるたびに、指定されたコマンドを実行します。                                                          |
|                 -[-] 最大 <value>                  |                                                 SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。                                                  |
|              -[-] my.cnf < [[hh:] mm:] ss >              |     時間を指定した場合は、指定した時間が経過した時点で新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                        -y                        |                                                             確認を求めずにすべての質問に対して [はい] を回答します。                                                              |
|            -mods < パス [path [...]]>             |                                                          API 呼び出しのログを記録するモジュールの一覧を指定します。                                                           |
|     -inapis < module! api [module! api [...]]>      |                                                         ログに記録する API 呼び出しの一覧を指定します。                                                          |
|     -exapis < module! api [module! api [...]]>      |                                                        ログから除外する API 呼び出しの一覧を指定します。                                                         |
|                     -[-] ano                      |                                                     Log (-ano) API 名のみ、またはログのみ (-ano) API 名をログに記録します。                                                     |
|                  -[-] recursive                   |                                          ログ (-recursive) を実行するか、最初のレイヤーを越えて再帰的に Api をログに記録しないようにします。                                           |
|                   -exe <value>                   |                                                        API トレースの実行可能ファイルへの完全パスを指定します。                                                        |

## <a name="remarks"></a>コメント  
[-] が一覧表示されている場合は、オプションを追加して否定します。  
## <a name="BKMK_examples"></a>例  
次のコマンドは、実行可能ファイル c:\windows\notepad.exe に対して trace_notepad という API トレースカウンターを作成し、結果をファイルに出力します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -o c:\notepad.etl  
```  
次のコマンドは、モジュール c:\windows\system32\advapi32.dll. によって生成された値を収集する c:\windows\notepad.exe の実行可能ファイルに対して、trace_notepad という API トレースカウンターを作成します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -mods c:\windows\system32\advapi32.dll  
```  
次のコマンドは、モジュール kernel32.dll によって生成された API 呼び出し TlsGetValue を除く、実行可能ファイル c:\windows\notepad.exe の trace_notepad という API トレースカウンターを作成します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue  
```  
#### <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
