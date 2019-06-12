---
title: logman query
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e00e1ca7e6e090fd618af5b0ca2307bb573ab8c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437722"
---
# <a name="logman-query"></a>logman query

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データ コレクターのクエリまたはデータ コレクターは、プロパティを設定します。  

## <a name="syntax"></a>構文  
```  
logman query [providers|"Data Collector Set name"] [options]  
```  
## <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       ヘルプ コンテキストを表示します。                       |
| -s <computer name> |            指定したリモート コンピューター上のコマンドを実行します。             |
|  -config <value>   |           コマンド オプションを含む設定ファイルを指定します。            |
|    [-n] <name>     |                          ターゲット オブジェクトの名前。                          |
|        -ets        | イベント トレース セッションを保存したり、スケジュール設定なしで直接コマンドを送信します。 |

## <a name="BKMK_examples"></a>例  
次のコマンドは、ターゲット システムで構成されているすべてのデータ コレクター セットを一覧表示します。  
```  
logman query  
```  
次のコマンドは、データ コレクター セット perf_log という名前に含まれているデータ コレクターを一覧表示します。  
```  
logman query "perf_log"  
```  
次のコマンドは、ターゲット システム上のデータ コレクターのすべての利用可能なプロバイダーを一覧表示します。  
```  
logman query providers  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
