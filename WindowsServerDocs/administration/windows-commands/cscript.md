---
title: cscript
description: Cscript コマンドのリファレンストピック。コマンドライン環境で実行されるようにスクリプトを開始します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfba4b6a1c75183d58664e74da22bb7f8b866739
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993157"
---
# <a name="cscript"></a>cscript

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドライン環境で実行するスクリプトを開始します。

>[!IMPORTANT]
> このタスクを実行するときは、管理資格情報は必要ありません。 そのため、セキュリティ対策として、このタスクは管理資格情報のないユーザーとして実行することを検討してください。

## <a name="syntax"></a>構文

```
cscript <scriptname.extension> [/b] [/d] [/e:<engine>] [{/h:cscript | /h:wscript}] [/i] [/job:<identifier>] [{/logo | /nologo}] [/s] [/t:<seconds>] [x] [/u] [/?] [<scriptarguments>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| scriptname | オプションのファイル名拡張子を持つスクリプトファイルのパスとファイル名を指定します。 |
| /b | アラート、スクリプトエラー、入力プロンプトを表示しないバッチモードを指定します。 |
| /d | デバッガーを起動します。 |
| /e:`<engine>` | スクリプトの実行に使用するエンジンを指定します。 |
| /h: cscript | スクリプトを実行するための既定のスクリプトホストとして cscript.exe を登録します。 |
| /h: wscript | スクリプトを実行するための既定のスクリプトホストとして wscript.exe を登録します。 既定値です。 |
| /i | アラート、スクリプトエラー、および入力プロンプトを表示する対話モードを指定します。 これは既定値であり、の`/b`逆です。 |
| /ジョブ (<identifier> | Wsf スクリプトファイル内の*識別子*によって識別されるジョブを実行します。 |
| /ロゴ | スクリプトを実行する前に、Windows スクリプトホストバナーをコンソールに表示することを指定します。 これは既定値であり、の`/nologo`逆です。 |
| /nologo | スクリプトを実行する前に、Windows スクリプトホストバナーを表示しないように指定します。 |
| /s | 現在のユーザーの現在のコマンドプロンプトオプションを保存します。 |
| /t: <seconds> | スクリプトを実行できる最長時間を秒単位で指定します。 最大32767秒を指定できます。 既定では、時間制限はありません。 |
| /U | コンソールからリダイレクトされる入力と出力の Unicode を指定します。 |
| /x | デバッガーでスクリプトを開始します。 |
| /? | 使用可能なコマンドパラメーターを表示し、それらを使用するためのヘルプを提供します。 これは、パラメーターを指定せずに**cscript.exe**を入力し、スクリプトを使用しない場合と同じです。 |
| scriptarguments | スクリプトに渡される引数を指定します。 各スクリプト引数の前にはスラッシュ (**/**) を付ける必要があります。 |

#### <a name="remarks"></a>Remarks

- 各パラメーターは省略可能です。ただし、スクリプトを指定せずにスクリプトの引数を指定することはできません。 スクリプトまたはスクリプトの引数を指定しない場合、cscript.exe 構文と有効なホストオプションが cscript.exe によって表示されます。

- **/T**パラメーターを指定すると、タイマーを設定することによって、スクリプトの過剰な実行を防ぐことができます。 実行時間が指定された値を超えると、cscript はスクリプトエンジンを中断し、プロセスを終了します。

- Windows スクリプトファイルは、通常、次のファイル名拡張子のいずれかになります。 wsf、.vbs、.js。 Windows スクリプトホストでは、wsf スクリプトファイルを使用できます。 各 wsf ファイルは、複数のスクリプトエンジンを使用して複数のジョブを実行できます。

- 拡張子が関連付けられていないスクリプトファイルをダブルクリックすると、[**ファイルを開くアプリケーション**の選択] ダイアログボックスが表示されます。 [Wscript] または [cscript] を選択し、[この**ファイルの種類を開くには常にこのプログラムを使用する**] を選択します。 これにより、このファイルの種類のファイルの既定のスクリプトホストとして wscript.exe または cscript が登録されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
