---
title: logman api を作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: feabb946c6dd492f38d9d6e2e1dc69795839e211
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840633"
---
# <a name="logman-create-api"></a>logman api を作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

API のトレース データ コレクターを作成します。  
  
## <a name="syntax"></a>構文  
```  
logman create api <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|/?|ヘルプ コンテキストを表示します。|  
|-s <computer name>|指定したリモート コンピューター上のコマンドを実行します。|  
|-config <value>|コマンド オプションを含む設定ファイルを指定します。|  
|[-n] <name>|ターゲット オブジェクトの名前。|  
|-f <bin&#124;bincirc&#124;csv&#124;tsv&#124;sql>|データ コレクターのログの形式を指定します。|  
|-[-] u < ユーザー [password] >|実行するユーザーを指定します。 入力、* のパスワードがパスワードのプロンプトが生成されます。 パスワード プロンプトで入力すると、パスワードは表示されません。|  
|-m <[start] [stop] [[start] [stop] [...]]>|変更を手動で開始またはスケジュールされた begin または end の時間ではなく停止します。|  
|-rf < [hh:] mm:] ss >|指定した期間には、データ コレクターを実行します。|  
|-b < m/d/yyyy h:mm:ss [AM&#124;PM] >|指定した時刻のデータの収集を開始します。|  
|-e < m/d/yyyy h:mm:ss [AM&#124;PM] >|指定した時間にデータ収集を終了します。|  
|-si < [hh:] mm:] ss >|パフォーマンス カウンターのデータ コレクターのサンプリング間隔を指定します。|  
|-o <path&#124;dsn!log>|出力ログ ファイルまたは DSN とログは、SQL database の名を設定を指定します。|  
|-[-] r|指定した開始と終了時刻に毎日データ コレクターを繰り返します。|  
|-[-]、|既存のログ ファイルに追加します。|  
|-[-] ow|既存のログ ファイルを上書きします。|  
|-[-] v < ウズベキスタン&#124;指定されない >|ファイルのバージョン管理情報をログ ファイル名の末尾にアタッチします。|  
|-[-] rc <task>|指定されたコマンドを実行するたびに、ログは閉じられます。|  
|-[-] の最大数 <value>|最大ログ ファイルのサイズは、mb 単位または SQL ログ レコードの最大数。|  
|-[-] cnf < [hh:] mm:] ss >|時間を指定すると、指定した時間が経過すると、新しいファイルを作成します。 時間が指定されていない場合は、最大サイズを超えたときに新しいファイルを作成します。|  
|-y|メッセージを表示せず、すべての質問に [はい] 回答します。|  
|-mods <path [path [...]]>|API 呼び出しをログにモジュールの一覧を指定します。|  
|-inapis < モジュール api [モジュール。 api [...]]。>|ログ記録に含める API 呼び出しの一覧を指定します。|  
|-exapis <module!api [module!api [...]]>|ログから除外する API 呼び出しの一覧を指定します。|  
|-[-] ano]|ログ (-ano) API 名のみ、のみログに記録しませんまたは (-ano) API 名。|  
|-[-] 再帰|ログ (-再帰的) ログに記録しないまたは (-再帰的な) Api を再帰的に最初のレイヤーを超える。|  
|exe <value>|API のトレースの実行可能ファイルへの完全パスを指定します。|  
## <a name="remarks"></a>注釈  
[-] がリスト表示と、余分なオプションを無効にします。  
## <a name="BKMK_examples"></a>例  
次のコマンドは、カウンターの実行可能ファイル c:\windows\notepad.exe trace_notepad と呼ばれる API のトレースを作成し、ファイル c:\notepad.etl に結果を出力します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -o c:\notepad.etl  
```  
次のコマンドでは、カウンターのモジュール c:\windows\system32\advapi32.dll によって生成された値を収集する実行可能ファイル c:\windows\notepad.exe trace_notepad と呼ばれる API のトレースを作成します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -mods c:\windows\system32\advapi32.dll  
```  
次のコマンドでは、カウンターの TlsGetValue モジュール kernel32.dll によって生成された API 呼び出しを除外する実行可能ファイル c:\windows\notepad.exe trace_notepad と呼ばれる API のトレースを作成します。  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
