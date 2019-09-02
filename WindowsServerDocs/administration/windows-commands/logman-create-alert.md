---
title: logman 作成アラート
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93e6fc2b-5bf5-413b-84b4-be8b9dd3a57d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37a13ab5623a295f96bde2f734bcb17e1eca2be9
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "66437847"
---
# <a name="logman-create-alert"></a>logman 作成アラート

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アラートデータコレクターを作成します。  

## <a name="syntax"></a>構文  
```  
logman create alert <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|                 パラメーター                  |                                                                               説明                                                                               |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /?                     |                                                                    状況依存のヘルプを表示します。                                                                     |
|             -s<computer name>             |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|              -config <value>               |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|                [-n]<name>                 |                                                                       ターゲットオブジェクトの名前。                                                                        |
|          -[-] u < ユーザー [パスワード] >           | として実行するユーザーを指定します。 パスワードの\*を入力すると、パスワードの入力を求めるメッセージが表示されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
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
|               -[-] rc<task>                |                                                         ログが閉じられるたびに、指定されたコマンドを実行します。                                                          |
|              -[-] 最大 <value>               |                                                 SQL ログの最大ログファイルサイズ (MB 単位または最大レコード数)。                                                  |
|           -[-] my.cnf < [[hh:] mm:] ss >           |     時間を指定した場合は、指定した時間が経過した時点で新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                     -y                     |                                                             確認を求めずにすべての質問に対して [はい] を回答します。                                                              |
|               -cf<filename>               |                       収集するパフォーマンスカウンターを一覧表示するファイルを指定します。 ファイルには、1行につき1つのパフォーマンスカウンター名を含める必要があります。                        |
|                   -[-] el                   |                                                                イベントログレポートを有効または無効にします。                                                                 |
|     -th < threshold [しきい値 [...]]>      |                                                        警告のカウンターとそのしきい値を指定します。                                                        |
|              -[-] rdcs<name>               |                                                     警告が発生したときに開始するデータコレクターセットを指定します。                                                      |
|               -[-] tn<task>                |                                                             警告が発生したときに実行するタスクを指定します。                                                              |
|            -[-] targ<argument>             |                                               -Tn を使用して指定されたタスクで使用されるタスク引数を指定します。                                                |

## <a name="remarks"></a>コメント  
[-] が一覧表示されている場合は、オプションを追加して否定します。  
## <a name="BKMK_examples"></a>例  
次のコマンドは、new_alert という名前のアラートを作成します。このアラートは、Processor (_Total) カウンターグループのパフォーマンスカウンターの% Processor time が、カウンター値50を超えた場合に発生します。  
```  
logman create alert new_alert -th "\Processor(_Total)\% Processor time>50"  
```  
> [!NOTE]
> 定義されているしきい値は、カウンターによって収集された値に基づいています。したがって、この例では、50の値は 50% Processor time に相当します。  
> #### <a name="additional-references"></a>その他の参照情報  
> [logman](logman.md)  
