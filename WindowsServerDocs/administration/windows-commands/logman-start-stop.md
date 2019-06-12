---
title: logman start |停止
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c6027c4c9a99e45bb1c2e95cdfd4a7687a5c43b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437683"
---
# <a name="logman-start--stop"></a>logman start |停止

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データ コレクターを開始を manual に開始時刻を設定するか、設定、終了時刻を手動に設定し、データ コレクターを停止します。  

## <a name="syntax"></a>構文  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       ヘルプ コンテキストを表示します。                       |
| -s <computer name> |            指定したリモート コンピューター上のコマンドを実行します。             |
|  -config <value>   |           コマンド オプションを含む設定ファイルを指定します。            |
|    [-n] <name>     |                          ターゲット オブジェクトの名前。                          |
|        -ets        | イベント トレース セッションを保存したり、スケジュール設定なしで直接コマンドを送信します。 |
|        -として         |               要求された操作を非同期的に実行します。                |

## <a name="BKMK_examples"></a>例  
次のコマンドは、リモート コンピューター server_1 にデータ コレクターの perf_log を開始します。  
```  
logman start perf_log -s server_1  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
