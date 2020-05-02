---
title: logman カウンターの作成
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e214c32-b704-43c1-b548-e1cf43b583c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: feff7ad1597232ad441e2ad23ee73638b4ad68ea
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724398"
---
# <a name="logman-create-counter"></a>logman カウンターの作成

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カウンターデータコレクターを作成します。  

## <a name="syntax"></a>構文  
```  
logman create counter <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|                    パラメーター                     |                                                                               説明                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    状況依存のヘルプを表示します。                                                                     |
|                -s<computer name>                |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|                 -config <value>                  |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|                   [-n]<name>                    |                                                                       対象オブジェクトの名前。                                                                        |
| -f <bin&#124;bincirc&#124;csv&#124;tsv&#124;sql> |                                                            データコレクターのログの形式を指定します。                                                             |
|             -[-] u <ユーザー [パスワード] >              | として実行するユーザーを指定します。 パスワードの\*を入力すると、パスワードの入力を求めるメッセージが表示されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
|    -m < [開始] [停止] [[開始] [停止] [...]]>    |                                                スケジュールされた開始時刻または終了時刻ではなく、手動の開始または停止に変更します。                                                 |
|                -rf < [[hh:] mm:] ss>                |                                                        指定された期間、データコレクターを実行します。                                                         |
|        -b <M/d/yyyy h:mm: ss [AM&#124;PM] >         |                                                              指定された時間にデータの収集を開始します。                                                               |
|        -e <M/d/yyyy h:mm: ss [AM&#124;PM] >         |                                                               指定された時刻にデータ収集を終了します。                                                                |
|                -si < [[hh:] mm:] ss>                |                                                 パフォーマンスカウンターデータコレクターのサンプル間隔を指定します。                                                  |
|              -o <path&#124;dsn! log>              |                                              SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。                                               |
|                      -[-] r                       |                                                  指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。                                                  |
|                      -[-] a                       |                                                                     既存のログファイルに追加します。                                                                     |
|                      -[-] o                      |                                                                     既存のログファイルを上書きします。                                                                     |
|           -[-] v <nnnnnn&#124;mmddhhmm>           |                                                   ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。                                                   |
|                  -[-] rc<task>                   |                                                         ログが閉じられるたびに、指定されたコマンドを実行します。                                                          |
|                 -[-] 最大 <value>                  |                                                 SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。                                                  |
|              -[-] my.cnf < [[hh:] mm:] ss>              |     時間を指定した場合は、指定した時間が経過した時点で新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                        -y                        |                                                             確認を求めずにすべての質問に対して [はい] を回答します。                                                              |
|                  -cf<filename>                  |                       収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。                        |
|               -c <パス [] >               |                                                              収集するパフォーマンスカウンターを指定します。                                                               |
|                   -sc <value>                    |                                      パフォーマンスカウンターデータコレクターを使用して収集するサンプルの最大数を指定します。                                      |

## <a name="remarks"></a>Remarks  
[-] が一覧表示されている場合は、オプションを追加して否定します。  
## <a name="examples"></a>例  
次のコマンドは、Processor (_Total) カウンターカテゴリの% Processor time カウンターを使用して、perf_log というカウンターを作成します。  
```  
logman create counter perf_log -c \Processor(_Total)\% Processor time  
```  
次のコマンドは、プロセッサ (_Total) カウンターカテゴリの% Processor time カウンターを使用して perf_log というカウンターを作成し、最大サイズが 10 MB のログファイルを作成し、1分と0秒間データを収集します。  
```  
logman create counter perf_log -c \Processor(_Total)\% Processor time -max 10 -rf 01:00  
```  
## <a name="additional-references"></a>その他のリファレンス  
[logman](logman.md)  
