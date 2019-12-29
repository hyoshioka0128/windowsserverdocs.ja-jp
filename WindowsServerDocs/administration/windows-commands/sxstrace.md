---
title: sxstrace
description: サイドバイサイドの問題を診断する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66326943bf1b056951ae5824df5a4f60892492cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370712"
---
# <a name="sxstrace"></a>sxstrace

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイド バイ サイドの問題を診断します。    

## <a name="syntax"></a>構文  
```  
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]  
```  

### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|trace|Sxs (サイド バイ サイド) のトレースを有効に|  
|-logfile|未処理のログ ファイルを指定します。|  
|\<ファイル名 >|トレース ログが保存 *FileName*します。|  
|-nostop|トレースを停止するように求めるメッセージは指定されません。|  
|解析|生のトレース ファイルに変換します。|  
|-出力|出力ファイル名を指定します。|  
|\<ParsedFile >|解析されたファイルのファイル名を指定します。|  
|-フィルター|フィルター選択される出力を使用します。|  
|\<AppName >|アプリケーションの名前を指定します。|  
|stoptrace|前に停止していない場合は、トレースを停止します。|  
|-?|コマンド プロンプトにヘルプを表示します。|  

## <a name="BKMK_Examples"></a>例  
トレースを有効にして、トレース ファイルを保存して **sxstrace.etl**:  
```  
sxstrace trace -logfile:sxstrace.etl  
```  
生のトレース ファイルを人間が読める形式に変換し、結果を保存 **sxstrace.txt**:  
```  
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
