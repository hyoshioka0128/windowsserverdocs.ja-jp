---
title: typeperf
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 087b201c51d5aec8e6f61c7469c59307d3ed8b4d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392296"
---
# <a name="typeperf"></a>typeperf



**Typeperf**コマンドは、パフォーマンスデータをコマンドウィンドウまたはログファイルに書き込みます。 **Typeperf**を停止するには、Ctrl + C キーを押します。

**Typeperf**の使用方法の例については、「[例](#BKMK_EXAMPLES)」を参照してください。

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
|\<counter [カウンター [...]]>|監視するパフォーマンスカウンターを指定します。|

> [!NOTE]
> **\<counter >** は *\\ @ no__t-4Computer\Object (インスタンス) \ カウンター*形式のパフォーマンスカウンターの完全な名前です (例: **\\ @ no__t-7Server1\Processor (0) \% ユーザー時間)** 。

## <a name="options"></a>および

|                   OPTION                   |                                                         説明                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               状況依存のヘルプを表示します。                                               |
| -f \<CSV @ no__t-1TSV @ no__t-2BIN @ no__t-3SQL > |                                    出力ファイルの形式を指定します。 既定値は CSV です。                                     |
|              -cf \<filename >               |              監視するパフォーマンスカウンターの一覧を含むファイルを指定します。1行につき1つのカウンターがあります。               |
|             -si < [[hh:] mm:] ss >             |                                  サンプル間隔を指定します。 既定値は1秒です。                                   |
|               -o \<filename >               |     出力ファイルまたは SQL データベースのパスを指定します。 既定値は STDOUT (コマンドウィンドウに書き込まれます) です。      |
|                -q [オブジェクト]                 | インストールされているカウンターの一覧を表示します (インスタンスなし)。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。 \* @ NO__T @ NO__T-2EXAMPLE |
|                -qx [オブジェクト]                |        インストールされているカウンターの一覧をインスタンスと共に表示します。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。        |
|               -sc \<samples >               |             収集するサンプルの数を指定します。 既定では、CTRL + C キーが押されるまでデータが収集されます。              |
|            -config \<ファイル名 >             |                                    コマンドオプションを含む設定ファイルを指定します。                                     |
|            -s \<computer_name >             |                   カウンターパスにコンピューターが指定されていない場合に、監視するリモートコンピューターを指定します。                    |
|                     -y                     |                                        確認を求めずにすべての質問に対して [はい] を回答します。                                        |

## <a name="BKMK_EXAMPLES"></a>例

- 次の例では、ローカルコンピューターのパフォーマンスカウンターの値 **\\ @ no__t-2processor (_total) \% プロセッサ時間**を既定のサンプル間隔である1秒で、CTRL + C キーを押します。  
  ```
  typeperf "\Processor(_Total)\% Processor Time"
  ```  
- 次の例では、50サンプルが収集されるまでの5秒のサンプル間隔で、ファイル**カウンター .txt**内のカウンターの一覧の値をタブ区切りファイル**domain2**に書き込みます。  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- 次の例では、カウンターオブジェクト**PhysicalDisk**のインスタンスを使用してインストールされているカウンターに対してクエリを行い、結果の一覧をファイル**カウンター .txt**に書き込みます。  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
