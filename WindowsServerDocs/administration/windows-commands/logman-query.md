---
title: logman query
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05448a4f129a59145813dd0da7199d4adf845c5c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724356"
---
# <a name="logman-query"></a>logman query

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターまたはデータコレクターセットのプロパティを照会します。  

## <a name="syntax"></a>構文  
```  
logman query [providers|Data Collector Set name] [options]  
```  
### <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       状況依存のヘルプを表示します。                       |
| -s<computer name> |            指定したリモートコンピューターでコマンドを実行します。             |
|  -config <value>   |           コマンドオプションを含む設定ファイルを指定します。            |
|    [-n]<name>     |                          対象オブジェクトの名前。                          |
|        -/        | イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。 |

## <a name="examples"></a>例  
次のコマンドは、ターゲットシステムで構成されているすべてのデータコレクターセットを一覧表示します。  
```  
logman query  
```  
次のコマンドは、perf_log という名前のデータコレクターセットに含まれているデータコレクターの一覧を表示します。  
```  
logman query perf_log  
```  
次のコマンドは、ターゲットシステム上のデータコレクターの使用可能なすべてのプロバイダーを一覧表示します。  
```  
logman query providers  
```  
## <a name="additional-references"></a>その他のリファレンス  
[logman](logman.md)  
