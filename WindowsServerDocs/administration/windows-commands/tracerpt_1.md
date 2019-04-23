---
title: tracerpt
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4d943da40793be0680d6ea6a4d9de0960f65c72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861703"
---
# <a name="tracerpt"></a>tracerpt



**Tracerpt**コマンドは、イベント トレース ログ、パフォーマンス モニター、およびリアルタイムのイベント トレース プロバイダーによって生成されるログ ファイルの解析に使用できます。 ダンプ ファイル、レポート ファイル、およびレポートのスキーマを生成します。

使用する方法の例については**tracerpt**を参照してください[例](#BKMK_EXAMPLES)します。

## <a name="syntax"></a>構文

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>オプション

|オプション フラグ|説明|
|-----------|-----------|
|-?|ヘルプ表示のコンテキストに依存します。|
|-config \<filename>|コマンド オプションを含む設定ファイルを読み込みます。|
|-y|メッセージを表示せず、すべての質問に [はい] 回答します。|
|-f \<XML | HTML>|レポートの書式を定義します。|
|-の\<CSV | EVTX | XML &GT;|ダンプの形式を定義します。 既定値は XML です。|
|-df \<filename>|Microsoft 固有の仕様を作成するスキーマ ファイルのカウント/レポートします。|
|-int \<filename>|指定したファイルに解釈されたイベントの構造をダンプします。|
|rts-|生のタイムスタンプ。 レポートは、イベントのヘッダーをトレースします。 ありません - レポートや概要-o のみ使用できます。|
|-tmf \<filename>|トレース メッセージの書式定義ファイルを指定します。|
|-tp \<value>|TMF ファイルの検索パスを指定します。 セミコロン (;) で区切られた複数のパスを使用できます。|
|-i \<value>|プロバイダーのイメージのパスを指定します。 一致する PDB シンボル サーバーに配置されます。 セミコロン (;) で区切られた複数のパスを使用できます。|
|-pdb \<value>|シンボル サーバーのパスを指定します。 セミコロン (;) で区切られた複数のパスを使用できます。|
|-gmt|WPP ペイロードのタイムスタンプをグリニッジ標準時に変換します。|
|-rl \<value>|システム レポートのレベルを 1 から 5 を定義します。 既定値は 1 です。|
|-[ファイル名] の概要|概要レポートのテキスト ファイルを生成します。 ファイル名を指定しない場合は、summary.txt です。|
|-o [ファイル名]|テキスト出力ファイルを生成します。 ファイル名を指定しない場合は、dumpfile.xml です。|
|-レポートの [ファイル名]|テキスト出力レポート ファイルを生成します。 ファイル名を指定しない場合は、workload.xml です。|
|-lr|指定「緩い」 これは、イベント スキーマに一致しないイベントを最善の努力を使用します。|
|-export [filename]|イベント スキーマのエクスポート ファイルを生成します。 ファイル名を指定しない場合は、schema.man です。|
|[-l] \<value [value […]]>|処理するためのイベント トレース ログ ファイルを指定します。|
|-rt \<session_name [session_name […]]>|リアルタイムのイベント トレース セッションのデータ ソースを指定します。|

## <a name="BKMK_EXAMPLES"></a>例

-   この例は、2 つのイベント ログに基づくレポートを作成します。 **logfile1.etl**と**logfile2.etl**ダンプ ファイルを作成します**logdump.xml** XML 形式でします。  
    ```
    tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
    ```  
-   この例は、イベント ログに基づくレポートを作成します。 **logfile.etl**、ダンプ ファイルを作成します。 **logdmp.xml** 、XML 形式のスキーマではなくイベントを識別するために最善の努力を使用するには、概要レポート ファイルが生成されます。**logdump.txt**、レポート ファイルを生成します**logrpt.xml**します。  
    ```
    tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
    ```  
-   この例は、2 つのイベント ログを使用して**logfile1.etl**と**logfile2.etl**ダンプ ファイルとファイル名の既定のレポート ファイルを作成します。  
    ```
    tracerpt logfile1.etl logfile2.etl -o -report
    ```  
-   この例は、イベント ログを使用して**logfile.etl**とパフォーマンス ログ**counterfile.blg**レポート ファイルを生成するために**logrpt.xml**と、Microsoft 固有の XML スキーマファイル**schema.xml**します。  
    ```
    tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
    ```  
-   この例は、リアルタイムのイベント トレース セッション"NT Kernel Logger"を読み取り、ダンプ ファイルを生成**logfile.csv** CSV 形式でします。  
    ```
    tracerpt -rt "NT Kernel Logger" -o logfile.csv -of CSV
    ```