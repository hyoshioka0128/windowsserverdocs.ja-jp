---
title: logman query
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6acf6cf5240dd59357f4c788577190699a354744
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374421"
---
# <a name="logman-query"></a>logman query

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データコレクターまたはデータコレクターセットのプロパティを照会します。  

## <a name="syntax"></a>構文  
```  
logman query [providers|"Data Collector Set name"] [options]  
```  
## <a name="parameters"></a>パラメーター  

|     パラメーター      |                                 説明                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       状況依存のヘルプを表示します。                       |
| -s <computer name> |            指定したリモートコンピューターでコマンドを実行します。             |
|  -config <value>   |           コマンドオプションを含む設定ファイルを指定します。            |
|    [-n] <name>     |                          ターゲットオブジェクトの名前。                          |
|        -/        | イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。 |

## <a name="BKMK_examples"></a>例  
次のコマンドは、ターゲットシステムで構成されているすべてのデータコレクターセットを一覧表示します。  
```  
logman query  
```  
次のコマンドは、perf_log という名前のデータコレクターセットに含まれているデータコレクターの一覧を表示します。  
```  
logman query "perf_log"  
```  
次のコマンドは、ターゲットシステム上のデータコレクターの使用可能なすべてのプロバイダーを一覧表示します。  
```  
logman query providers  
```  
#### <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
