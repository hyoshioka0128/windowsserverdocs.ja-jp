---
title: typeperf
description: Typeperf の Windows コマンドに関するトピックでは、パフォーマンスデータがコマンドウィンドウまたはログファイルに書き込まれます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac5f7def37939a472eb8f47cf65edf184a2fe2fc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832365"
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

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<カウンタ [カウンター [...]]>|監視するパフォーマンスカウンターを指定します。|

> [!NOTE]
> **\<カウンタ >** は *\\\\Computer\Object (インスタンス) \ カウンター*形式のパフォーマンスカウンターの完全な名前です **(\\\\Server1\Processor (0)\% User Time**など)。

## <a name="options"></a>オプション

|                   オプション                   |                                                         説明                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               状況依存のヘルプを表示します。                                               |
| -f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL > |                                    出力ファイルの形式を指定します。 既定値は CSV です。                                     |
|              -cf \<ファイル名 >               |              監視するパフォーマンスカウンターの一覧を含むファイルを指定します。1行につき1つのカウンターがあります。               |
|             -si < [[hh:] mm:] ss >             |                                  サンプル間隔を指定します。 既定値は1秒です。                                   |
|               -o \<ファイル名 >               |     出力ファイルまたは SQL データベースのパスを指定します。 既定値は STDOUT (コマンドウィンドウに書き込まれます) です。      |
|                -q [オブジェクト]                 | インストールされているカウンターの一覧を表示します (インスタンスなし)。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。 \*\*\*の例 |
|                -qx [オブジェクト]                |        インストールされているカウンターの一覧をインスタンスと共に表示します。 1つのオブジェクトのカウンターを一覧表示するには、オブジェクト名を含めます。        |
|               -sc \<のサンプル >               |             収集するサンプルの数を指定します。 既定では、CTRL + C キーが押されるまでデータが収集されます。              |
|            -config \<ファイル名 >             |                                    コマンドオプションを含む設定ファイルを指定します。                                     |
|            -s \<computer_name >             |                   カウンターパスにコンピューターが指定されていない場合に、監視するリモートコンピューターを指定します。                    |
|                     -y                     |                                        確認を求めずにすべての質問に対して [はい] を回答します。                                        |

## <a name="examples"></a><a name=BKMK_EXAMPLES></a>例

- 次の例では、ローカルコンピューターのパフォーマンスカウンター **\\\\processor (_Total\%)** の値をコマンドウィンドウに書き込みます。既定のサンプル間隔は1秒で、CTRL + C キーを押します。  
  ```
  typeperf \Processor(_Total)\% Processor Time
  ```  
- 次の例では、50サンプルが収集されるまでの5秒のサンプル間隔で、ファイル**カウンター .txt**内のカウンターの一覧の値をタブ区切りファイル**domain2**に書き込みます。  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- 次の例では、カウンターオブジェクト**PhysicalDisk**のインスタンスを使用してインストールされているカウンターに対してクエリを行い、結果の一覧をファイル**カウンター .txt**に書き込みます。  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
