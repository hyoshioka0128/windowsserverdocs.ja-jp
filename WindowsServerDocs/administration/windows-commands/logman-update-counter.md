---
title: logman 更新カウンター
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 607df6d5-876c-428d-a0b3-f59cb244e2ce britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c0696b6077a919d93106cb39329c986e91883fa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374355"
---
# <a name="logman-update-counter"></a>logman 更新カウンター

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のカウンターデータコレクターのプロパティを更新します。  

## <a name="syntax"></a>構文  
```  
logman update counter <[-n] <name>> [options]  
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
|                  -cf <filename>                  |                       収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。                        |
|               -c < パス [] >               |                                                              収集するパフォーマンスカウンターを指定します。                                                               |
|                   -sc <value>                    |                                      パフォーマンスカウンターデータコレクターを使用して収集するサンプルの最大数を指定します。                                      |

## <a name="remarks"></a>コメント  
[-] が一覧表示されている場合は、オプションを追加して否定します。  
## <a name="BKMK_examples"></a>例  
次のコマンドでは、データコレクター perf_log を更新します。サンプル間隔を10に変更し、ログ形式を CSV に変更して、mmddhhmm 形式でログファイル名にバージョン管理を追加します。  
```  
logman update perf_log -si 10 -f csv -v mmddhhmm  
```  
#### <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
[logman カウンターの作成](logman-create-counter.md)  
