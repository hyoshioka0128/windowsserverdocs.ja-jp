---
title: サーバーでの WinSAT スコアの設定
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819953"
---
# <a name="set-the-winsat-score-on-the-server"></a>サーバーでの WinSAT スコアの設定

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

ビデオ ストリーミング解像度を最適化するために、Windows Server Essentials オペレーティング システムを実行しているサーバーの WinSAT CPU スコアを設定する必要があります。 これには、WinSAT スコア情報を含む .xml ファイルを作成してインストールします。  
  
## <a name="obtain-the-winsat-cpu-score"></a>WinSAT CPU スコアの取得  
 OPK には WinServerSAT.exe という名前のプログラムが付属しており、WinSAT CPU スコアを検出して、その情報を WinServerSAT.xml ファイルに格納します。オペレーティング システムはこのファイルを読み取ります。  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>WinSAT CPU スコアを取得するには  
  
1.  コピー、Resources\WinServerSAT\\* ADK メディアの参照コンピューターにします。  
  
2.  参照コンピューター上で、昇格した [コマンド プロンプト] ウィンドウを開きます。  
  
3.  %ProgramFiles%\Windows Server\Bin\OEM フォルダーがない場合は、次のコマンドを入力して Enter キーを押します。  
  
     **mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**  
  
4.  次のコマンドを入力して Enter キーを押します。  
  
     **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**  
  
 次の例では、作成される WinServerSAT.xml ファイルの XML コンテンツを示します。  
  
```  
  
<?xml version="1.0" encoding="UTF-16"?>  
<WinSAT>  
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>  
</WinSAT>  
```  
  
 ここで *WinSAT_Score* は、サーバー上で検出された値に置き換えられます。  
  
> [!IMPORTANT]
>  イメージをキャプチャする前に、WinServerSAT.exe、winsat.prx、winsat.wmv、および WinSATEncode.wmv ファイルを参照コンピューターから削除する必要があります。
