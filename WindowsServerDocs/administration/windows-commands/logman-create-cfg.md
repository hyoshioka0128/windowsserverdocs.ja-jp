---
title: logman cfg を作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bfc87093-3ff5-4e19-aa93-d185fb8e2239
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1521ae20091f2c57094fa1c75bd583e517628126
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437776"
---
# <a name="logman-create-cfg"></a>logman cfg を作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データ コレクターの構成を作成します。  

## <a name="syntax"></a>構文  
```  
logman create cfg <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|                    パラメーター                     |                                                                               説明                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    ヘルプ コンテキストを表示します。                                                                     |
|                -s <computer name>                |                                                          指定したリモート コンピューター上のコマンドを実行します。                                                          |
|                 -config <value>                  |                                                         コマンド オプションを含む設定ファイルを指定します。                                                         |
|                   [-n] <name>                    |                                                                       ターゲット オブジェクトの名前。                                                                        |
| -f <bin&#124;bincirc&#124;csv&#124;tsv&#124;sql> |                                                            データ コレクターのログの形式を指定します。                                                             |
|             -[-] u < ユーザー [password] >              | 実行するユーザーを指定します。 入力、\*のパスワードがパスワードのプロンプトが生成されます。 パスワード プロンプトで入力すると、パスワードは表示されません。 |
|    -m <[start] [stop] [[start] [stop] [...]]>    |                                                変更を手動で開始またはスケジュールされた begin または end の時間ではなく停止します。                                                 |
|                -rf < [hh:] mm:] ss >                |                                                        指定した期間には、データ コレクターを実行します。                                                         |
|        -b < m/d/yyyy h:mm:ss [AM&#124;PM] >         |                                                              指定した時刻のデータの収集を開始します。                                                               |
|        -e < m/d/yyyy h:mm:ss [AM&#124;PM] >         |                                                               指定した時間にデータ収集を終了します。                                                                |
|                -si < [hh:] mm:] ss >                |                                                 パフォーマンス カウンターのデータ コレクターのサンプリング間隔を指定します。                                                  |
|              -o <path&#124;dsn!log>              |                                              出力ログ ファイルまたは DSN とログは、SQL database の名を設定を指定します。                                               |
|                      -[-] r                       |                                                  指定した開始と終了時刻に毎日データ コレクターを繰り返します。                                                  |
|                      -[-]、                       |                                                                     既存のログ ファイルに追加します。                                                                     |
|                      -[-] ow                      |                                                                     既存のログ ファイルを上書きします。                                                                     |
|           -[-] v < ウズベキスタン&#124;指定されない >           |                                                   ファイルのバージョン管理情報をログ ファイル名の末尾にアタッチします。                                                   |
|                  -[-] rc <task>                   |                                                         指定されたコマンドを実行するたびに、ログは閉じられます。                                                          |
|                 -[-] の最大数 <value>                  |                                                 最大ログ ファイルのサイズは、mb 単位または SQL ログ レコードの最大数。                                                  |
|              -[-] cnf < [hh:] mm:] ss >              |     時間を指定すると、指定した時間が経過すると、新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。     |
|                        -y                        |                                                             メッセージを表示せず、すべての質問に [はい] 回答します。                                                              |
|                      -[-] ni                      |                                                         有効にする (-ni) または無効にする (-ni) ネットワーク インターフェイスのクエリ。                                                          |
|             -reg <path [path [...]]>             |                                                                 収集するレジストリ値を指定します。                                                                 |
|            管理 - < クエリ [クエリ [...]>            |                                                      SQL クエリ言語を使用して収集するために WMI オブジェクトを指定します。                                                       |
|             -ftc < パス [パス [...]>             |                                                           収集するファイルへの完全パスを指定します。                                                            |

## <a name="remarks"></a>注釈  
[-] がリスト表示と、余分なオプションを無効にします。  
## <a name="BKMK_examples"></a>例  
次のコマンドは、レジストリ キー hkey_local_machine \software\microsoft\windows NT\Currentverion を使用する cfg_log と呼ばれる構成データ コレクターを作成します。\\します。  
```  
logman create cfg cfg_log -reg "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\"  
```  
次のコマンドは、データベース列 MSNdis_Vendordriverversion に root \wmi からすべての WMI オブジェクトを記録する cfg_log と呼ばれる構成データ コレクターを作成します。  
```  
logman create cfg cfg_log -mgt "root\wmi:select * FROM MSNdis_Vendordriverversion"  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
