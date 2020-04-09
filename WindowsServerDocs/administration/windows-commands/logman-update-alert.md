---
title: logman 更新アラート
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13bd7fbef96b75d9308b1e2c8475389d10bbb921
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840605"
---
# <a name="logman-update-alert"></a>logman 更新アラート

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のアラートデータコレクターのプロパティを更新します。  

## <a name="syntax"></a>構文  
```  
logman update alert <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|                 パラメーター                  |                                                                               説明                                                                               |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /?                     |                                                                    状況依存のヘルプを表示します。                                                                     |
|             -s <computer name>             |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|              -config <value>               |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|                [-n] <name>                 |                                                                       ターゲットオブジェクトの名前。                                                                        |
|          -[-] u < ユーザー [パスワード] >           | として実行するユーザーを指定します。 パスワードの \* を入力すると、パスワードの入力を求めるプロンプトが生成されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
| -m < [開始] [停止] [[開始] [停止] [...]]> |                                                スケジュールされた開始時刻または終了時刻ではなく、手動の開始または停止に変更します。                                                 |
|             -rf < [[hh:] mm:] ss >             |                                                        指定された期間、データコレクターを実行します。                                                         |
|     -b < M/d/yyyy h:mm: ss [AM&#124;PM] >      |                                                              指定された時間にデータの収集を開始します。                                                               |
|     -e < M/d/yyyy h:mm: ss [AM&#124;PM] >      |                                                               指定された時刻にデータ収集を終了します。                                                                |
|             -si < [[hh:] mm:] ss >             |                                                 パフォーマンスカウンターデータコレクターのサンプル間隔を指定します。                                                  |
|           -o < path&#124;dsn! ログ >           |                                              SQL データベースの出力ログファイルまたは DSN およびログセット名を指定します。                                               |
|                   -[-] r                    |                                                  指定された開始時刻と終了時刻にデータコレクターを毎日繰り返します。                                                  |
|                   -[-] a                    |                                                                     既存のログファイルに追加します。                                                                     |
|                   -[-] o                   |                                                                     既存のログファイルを上書きします。                                                                     |
|        -[-] v < nnnnnn&#124;mmddhhmm >        |                                                   ファイルのバージョン管理情報をログファイル名の末尾にアタッチします。                                                   |
|               -[-] rc <task>                |                                                         ログが閉じられるたびに、指定されたコマンドを実行します。                                                          |
|              -[-] 最大 <value>               |                                                 SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。                                                  |
|           -[-] my.cnf < [[hh:] mm:] ss >           |     時間を指定した場合は、指定した時間が経過した時点で新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                     -y                     |                                                             確認を求めずにすべての質問に対して [はい] を回答します。                                                              |
|               -cf <filename>               |                       収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。                        |
|                   -[-] el                   |                                                                イベントログレポートを有効または無効にします。                                                                 |
|     -th < threshold [しきい値 [...]]>      |                                                        警告のカウンターとそのしきい値を指定します。                                                        |
|              -[-] rdcs <name>               |                                                     警告が発生したときに開始するデータコレクターセットを指定します。                                                      |
|               -[-] tn <task>                |                                                             警告が発生したときに実行するタスクを指定します。                                                              |
|            -[-] targ <argument>             |                                               -Tn を使用して指定されたタスクで使用されるタスク引数を指定します。                                                |

## <a name="remarks"></a>コメント  
[-] が一覧表示されている場合は、オプションを追加して否定します。  
## <a name="examples"></a><a name=BKMK_examples></a>例  
次の例では、既存のデータコレクター new_alert を更新し、Processor (_Total) カウンターグループのカウンタ% Processor time のしきい値を40% に設定します。  
```  
logman update alert new_alert -th \Processor(_Total)\% Processor time>40  
```  
## <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
[logman 作成アラート](logman-create-alert.md)  
