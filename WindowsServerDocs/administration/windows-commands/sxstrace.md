---
title: sxstrace
description: サイドバイサイドの問題を診断する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ece727b68eb620e839cbfb8efe02dbe775666498
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833615"
---
# <a name="sxstrace"></a>sxstrace

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイド バイ サイドの問題を診断します。    

## <a name="syntax"></a>構文  
```  
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]  
```  

#### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|トレース|Sxs (サイド バイ サイド) のトレースを有効に|  
|-logfile|未処理のログ ファイルを指定します。|  
|\<ファイル名 >|トレース ログが保存 *FileName*します。|  
|-nostop|トレースを停止するように求めるメッセージは指定されません。|  
|解析|生のトレース ファイルに変換します。|  
|-出力|出力ファイル名を指定します。|  
|ParsedFile の \<>|解析されたファイルのファイル名を指定します。|  
|-フィルター|フィルター選択される出力を使用します。|  
|\<AppName >|アプリケーションの名前を指定します。|  
|stoptrace|前に停止していない場合は、トレースを停止します。|  
|-?|コマンド プロンプトでヘルプを表示します。|  

## <a name="examples"></a><a name="BKMK_Examples"></a>例  
トレースを有効にして、トレース ファイルを保存して **sxstrace.etl**:  
```  
sxstrace trace -logfile:sxstrace.etl  
```  
生のトレース ファイルを人間が読める形式に変換し、結果を保存 **sxstrace.txt**:  
```  
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
