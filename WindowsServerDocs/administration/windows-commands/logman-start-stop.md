---
title: logman start |停止
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2bd81a33779aa58e7528d0173a7a4b49489de8f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840625"
---
# <a name="logman-start--stop"></a>logman start |停止

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターを起動し、開始時刻を手動に設定するか、データコレクターセットを停止して、終了時刻を手動に設定します。  

## <a name="syntax"></a>構文  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       状況依存のヘルプを表示します。                       |
| -s <computer name> |            指定したリモートコンピューターでコマンドを実行します。             |
|  -config <value>   |           コマンドオプションを含む設定ファイルを指定します。            |
|    [-n] <name>     |                          ターゲットオブジェクトの名前。                          |
|        -/        | イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。 |
|        -as         |               要求された操作を非同期に実行します。                |

## <a name="examples"></a><a name=BKMK_examples></a>例  
次のコマンドを実行すると、リモートコンピューター server_1 のデータコレクター perf_log が開始されます。  
```  
logman start perf_log -s server_1  
```  
## <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
