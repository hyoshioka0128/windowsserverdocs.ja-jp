---
title: logman の更新の通知
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fddc654d0cfe37a167c0337dcc451cdb1755e43
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437703"
---
# <a name="logman-update-alert"></a>logman の更新の通知

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のアラート データ コレクターのプロパティを更新します。  

## <a name="syntax"></a>構文  
```  
logman update alert <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|                 パラメーター                  |                                                                               説明                                                                               |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /?                     |                                                                    ヘルプ コンテキストを表示します。                                                                     |
|             -s <computer name>             |                                                          指定したリモート コンピューター上のコマンドを実行します。                                                          |
|              -config <value>               |                                                         コマンド オプションを含む設定ファイルを指定します。                                                         |
|                [-n] <name>                 |                                                                       ターゲット オブジェクトの名前。                                                                        |
|          -[-] u < ユーザー [password] >           | 実行するユーザーを指定します。 入力、\*のパスワードがパスワードのプロンプトが生成されます。 パスワード プロンプトで入力すると、パスワードは表示されません。 |
| -m <[start] [stop] [[start] [stop] [...]]> |                                                変更を手動で開始またはスケジュールされた begin または end の時間ではなく停止します。                                                 |
|             -rf < [hh:] mm:] ss >             |                                                        指定した期間には、データ コレクターを実行します。                                                         |
|     -b < m/d/yyyy h:mm:ss [AM&#124;PM] >      |                                                              指定した時刻のデータの収集を開始します。                                                               |
|     -e < m/d/yyyy h:mm:ss [AM&#124;PM] >      |                                                               指定した時間にデータ収集を終了します。                                                                |
|             -si < [hh:] mm:] ss >             |                                                 パフォーマンス カウンターのデータ コレクターのサンプリング間隔を指定します。                                                  |
|           -o <path&#124;dsn!log>           |                                              出力ログ ファイルまたは DSN とログは、SQL database の名を設定を指定します。                                               |
|                   -[-] r                    |                                                  指定した開始と終了時刻に毎日データ コレクターを繰り返します。                                                  |
|                   -[-]、                    |                                                                     既存のログ ファイルに追加します。                                                                     |
|                   -[-] ow                   |                                                                     既存のログ ファイルを上書きします。                                                                     |
|        -[-] v < ウズベキスタン&#124;指定されない >        |                                                   ファイルのバージョン管理情報をログ ファイル名の末尾にアタッチします。                                                   |
|               -[-] rc <task>                |                                                         指定されたコマンドを実行するたびに、ログは閉じられます。                                                          |
|              -[-] の最大数 <value>               |                                                 最大ログ ファイルのサイズは、mb 単位または SQL ログ レコードの最大数。                                                  |
|           -[-] cnf < [hh:] mm:] ss >           |     時間を指定すると、指定した時間が経過すると、新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                     -y                     |                                                             メッセージを表示せず、すべての質問に [はい] 回答します。                                                              |
|               -cf <filename>               |                       収集するパフォーマンス カウンターの一覧を含むファイルを指定します。 ファイルには、1 行につき 1 つのパフォーマンス カウンターの名前を含める必要があります。                        |
|                   -[-] el                   |                                                                有効またはイベント ログに報告を無効にします。                                                                 |
|     -th <threshold [threshold [...]]>      |                                                        カウンターとアラートのしきい値の値を指定します。                                                        |
|              -[-] rdcs <name>               |                                                     アラートが発生したときに開始するデータ コレクター セットを指定します。                                                      |
|               -[-] tn <task>                |                                                             警告の発生時に実行するタスクを指定します。                                                              |
|            -[-] のターゲット <argument>             |                                               -Tn を使用して指定されたタスクで使用するタスクの引数を指定します。                                                |

## <a name="remarks"></a>注釈  
[-] がリスト表示と、余分なオプションを無効にします。  
## <a name="BKMK_examples"></a>例  
次の例では、既存のデータ コレクター new_alert、40 %processor (_total) カウンター グループのカウンターの % Processor time のしきい値の設定を更新します。  
```  
logman update alert new_alert -th "\Processor(_Total)\% Processor time>40"  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
[logman アラートを作成します。](logman-create-alert.md)  
