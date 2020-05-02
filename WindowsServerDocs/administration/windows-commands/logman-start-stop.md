---
title: logman start |停止
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68f570d99d4b3eaa818c9fbdcce76c42d1cb12d4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724342"
---
# <a name="logman-start--stop"></a>logman start |停止

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターを起動し、開始時刻を手動に設定するか、データコレクターセットを停止して、終了時刻を手動に設定します。  

## <a name="syntax"></a>構文  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 [説明]                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       状況依存のヘルプを表示します。                       |
| -s<computer name> |            指定したリモートコンピューターでコマンドを実行します。             |
|  -config <value>   |           コマンドオプションを含む設定ファイルを指定します。            |
|    [-n]<name>     |                          対象オブジェクトの名前。                          |
|        -/        | イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。 |
|        -as         |               要求された操作を非同期に実行します。                |

## <a name="examples"></a>例  
次のコマンドを実行すると、リモートコンピューター server_1 のデータコレクター perf_log が開始されます。  
```  
logman start perf_log -s server_1  
```  
## <a name="additional-references"></a>その他のリファレンス  
[logman](logman.md)  
