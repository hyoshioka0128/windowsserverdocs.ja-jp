---
title: logman start |停止
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 395d325b31ee596e1394e7ed796a444f159d15fc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374411"
---
# <a name="logman-start--stop"></a>logman start |停止

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターを起動し、開始時刻を手動に設定するか、データコレクターセットを停止して、終了時刻を手動に設定します。  

## <a name="syntax"></a>構文  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       状況依存のヘルプを表示します。                       |
| -s <computer name> |            指定したリモートコンピューターでコマンドを実行します。             |
|  -config <value>   |           コマンドオプションを含む設定ファイルを指定します。            |
|    [-n] <name>     |                          ターゲットオブジェクトの名前。                          |
|        -/        | イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。 |
|        -as         |               要求された操作を非同期に実行します。                |

## <a name="BKMK_examples"></a>例  
次のコマンドを実行すると、リモートコンピューター server_1 でデータコレクター perf_log が開始されます。  
```  
logman start perf_log -s server_1  
```  
#### <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
