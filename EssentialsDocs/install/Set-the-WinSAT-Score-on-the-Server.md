---
title: "サーバーの WinSAT スコアを設定します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 77866acccac13ac48da8779700c8654f2c7f3277
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="set-the-winsat-score-on-the-server"></a>サーバーの WinSAT スコアを設定します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

ビデオ ストリーミング解像度を最適化するために、Windows Server Essentials オペレーティング システムを実行しているサーバーの WinSAT CPU スコアを設定する必要があります。 これを行うを作成し、WinSAT スコア情報を含む .xml ファイルをインストールします。  
  
## <a name="obtain-the-winsat-cpu-score"></a>WinSAT CPU スコアを取得します。  
 WinSAT CPU スコアを検出し、オペレーティング システムを読み取る WinServerSAT.xml ファイルにその情報を格納する、WinServerSAT.exe opk プログラムが提供されます。  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>WinSAT CPU スコアを取得するには  
  
1.  参照コンピューターに ADK メディアの Resources\WinServerSAT\\ * をコピーします。  
  
2.  参照コンピューターでは、管理者特権のコマンド プロンプト ウィンドウを開きます。  
  
3.  %ProgramFiles%\Windows server \bin\OEM フォルダーが存在しない場合、次のコマンドを入力し、Enter キーを押します。  
  
     **mkdir"%ProgramFiles%\Windows server \bin\OEM"**  
  
4.  次のコマンドを入力し、Enter キーを押します。  
  
     **WinServerSAT.exe"%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**  
  
 次の例では、作成される WinServerSAT.xml ファイルの XML の内容を示します。  
  
```  
  
<?xml version="1.0" encoding="UTF-16"?>  
<WinSAT>  
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>  
</WinSAT>  
```  
  
 ここで*WinSAT_Score*は、サーバー上で検出された値に置き換えられます。  
  
> [!IMPORTANT]
>  イメージをキャプチャする前に、参照コンピューターから WinServerSAT.exe、winsat.prx、winsat.wmv、および WinSATEncode.wmv ファイルを削除する必要があります。
