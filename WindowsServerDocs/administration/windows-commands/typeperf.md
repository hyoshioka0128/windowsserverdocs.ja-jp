---
title: typeperf
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1337066f547367b381a531dbab6627ad78d280ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848453"
---
# <a name="typeperf"></a>typeperf



**Typeperf**コマンドがコマンド ウィンドウまたはログ ファイルに、パフォーマンス データを書き込みます。 停止する**typeperf**、ctrl キーを押しながら C キーを押します。

使用する方法の例については**typeperf**を参照してください[例](#BKMK_EXAMPLES)します。

## <a name="syntax"></a>構文

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<counter [counter […]]>|監視するパフォーマンス カウンターを指定します。|

> [!NOTE]
> **\<カウンター >** でパフォーマンス カウンターの完全な名前 *\\ \\Computer\Object (インスタンス) \Counter*書式設定など **\\ \\Server1\(0)\% User Time**します。

## <a name="options"></a>オプション

|オプション|説明|
|---------|-----------|
|-?|ヘルプ コンテキストを表示します。|
|-f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL>|出力ファイルの形式を指定します。 既定値は、CSV です。|
|-cf \<filename>|1 行につき 1 つのカウンターを監視するパフォーマンス カウンターの一覧を含むファイルを指定します。|
|-si < [hh:] mm:] ss >|サンプリング間隔を指定します。 既定では、1 秒間は。|
|-o \<filename>|出力ファイル、または SQL データベースのパスを指定します。 既定値は、STDOUT (コマンド ウィンドウに書き込まれますです)。|
|-q [object]|インストールされているカウンター (インスタンス) の一覧を表示します。 1 つのオブジェクトのカウンターを一覧表示するには、オブジェクト名が含まれます。 例|
|-qx [object]|インスタンスにインストールされているカウンターの一覧を表示します。 1 つのオブジェクトのカウンターを一覧表示するには、オブジェクト名が含まれます。|
|-sc \<samples>|収集するサンプルの数を指定します。 既定では、CTRL キーを押しながら C キーが押されるまでデータを収集します。|
|-config \<filename>|コマンド オプションを含む設定ファイルを指定します。|
|-s \<computer_name>|カウンター パスでコンピューターが指定されていない場合に監視するリモート コンピューターを指定します。|
|-y|メッセージを表示せず、すべての質問に [はい] 回答します。|

## <a name="BKMK_EXAMPLES"></a>例

-   次の例は、ローカル コンピューターのパフォーマンス カウンターの値を書き込みます **\\ \\processor (_total)\%プロセッサ時間**1 秒の既定のサンプル間隔で、コマンド ウィンドウCTRL キーを押しながら C キーが押されるとまでします。  
    ```
    typeperf "\Processor)_Total)\% Processor Time"
    ```  
-   次の例は、ファイル内のカウンターの一覧の値を書き込みます**counters.txt**タブ区切りファイルに**domain2.tsv** 50 のサンプルが収集されるまで 5 秒間のサンプル間隔。  
    ```
    typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
    ```  
-   次の例のクエリ カウンター オブジェクトのインスタンスにインストールされているカウンター **PhysicalDisk**し、結果のリストをファイルに書き込みます**counters.txt**します。  
    ```
    typeperf -qx PhysicalDisk -o counters.txt
    ```
