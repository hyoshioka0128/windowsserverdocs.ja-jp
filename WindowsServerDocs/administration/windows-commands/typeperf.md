---
title: typeperf
description: Typeperf のリファレンス記事。コマンドウィンドウまたはログファイルにパフォーマンスデータを書き込みます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90a53224b733489464b7432c6f8c9304dd62df18
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937317"
---
# <a name="typeperf"></a>typeperf

**Typeperf**コマンドは、パフォーマンスデータをコマンドウィンドウまたはログファイルに書き込みます。 **Typeperf**を停止するには、Ctrl + C キーを押します。

## <a name="syntax"></a>構文

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

### <a name="parameters"></a>パラメーター

|パラメーター|Description|
|---------|-----------|
|\<counter [counter […]]>|監視するパフォーマンスカウンターを指定します。|

> [!NOTE]
> **\<counter>*** \\ \\ Computer\Object (インスタンス) \ カウンター*形式のパフォーマンスカウンターの完全な名前を指定します (例: ** \\ \\ Server1\Processor (0) \% User Time)**。

## <a name="options"></a>オプション

|                   オプション                   |                                                         説明                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               状況依存のヘルプを表示します。                                               |
| -f\<CSV&verbar;TSV&verbar;BIN&verbar;SQL> |                                    出力ファイルの形式を指定します。 既定値は CSV です。                                     |
|              -cf\<filename>               |              監視するパフォーマンスカウンターの一覧を含むファイルを指定します。1行につき1つのカウンターがあります。               |
|             -si < [[hh:] mm:] ss>             |                                  サンプル間隔を指定します。 既定値は1秒です。                                   |
|               -o\<filename>               |     出力ファイルまたは SQL データベースのパスを指定します。 既定値は STDOUT (コマンドウィンドウに書き込まれます) です。      |
|                -q [オブジェクト]                 | インストールされているカウンターの一覧を表示します (インスタンスなし)。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。 \*\*\*よう |
|                -qx [オブジェクト]                |        インストールされているカウンターの一覧をインスタンスと共に表示します。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。        |
|               -sc\<samples>               |             収集するサンプルの数を指定します。 既定では、CTRL + C キーが押されるまでデータが収集されます。              |
|            -config\<filename>             |                                    コマンドオプションを含む設定ファイルを指定します。                                     |
|            -s\<computer_name>             |                   カウンターパスにコンピューターが指定されていない場合に、監視するリモートコンピューターを指定します。                    |
|                     -y                     |                                        確認を求めずにすべての質問に対して [はい] を回答します。                                        |

## <a name="examples"></a>例

- ローカルコンピューターのパフォーマンスカウンター ** \\ \\ プロセッサ (_Total) \% プロセッサ時間**の値をコマンドウィンドウに書き込むには、CTRL + C キーが押されるまで、既定のサンプル間隔は1秒に設定されます。
  ```
  typeperf \Processor(_Total)\% Processor Time
  ```
- ファイル**counters.txt**のカウンターの一覧の値を、50サンプルが収集されるまでの5秒のサンプル間隔で、タブ区切りファイル**domain2**に書き込みます。
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```
- カウンターオブジェクト**PhysicalDisk**のインスタンスを使用してインストールされたカウンターを照会し、結果の一覧をファイル**counters.txt**に書き込みます。
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
