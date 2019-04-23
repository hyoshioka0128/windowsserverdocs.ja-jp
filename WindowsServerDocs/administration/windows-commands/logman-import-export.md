---
title: logman import |エクスポート
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67621b109c379cc2758b4036460b6bb82df3e3d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848303"
---
# <a name="logman-import--export"></a>logman import |エクスポート

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

XML ファイルからデータ コレクター セットをインポートするか、データ コレクター セットを XML ファイルにエクスポートします。  
  
## <a name="syntax"></a>構文  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|-?|ヘルプ コンテキストを表示します。|  
|-s <computer name>|指定したリモート コンピューター上のコマンドを実行します。|  
|-config <value>|コマンド オプションを含む設定ファイルを指定します。|  
|[-n] <name>|ターゲット オブジェクトの名前。|  
|-xml <name>|インポートまたはエクスポートする XML ファイルの名前。|  
|-ets|イベント トレース セッションを保存したり、スケジュール設定なしで直接コマンドを送信します。|  
|-[-] u < ユーザー [password] >|ユーザーとして実行します。 入力、* のパスワードがパスワードのプロンプトが生成されます。 パスワード プロンプトで入力すると、パスワードは表示されません。|  
|-y|メッセージを表示せず、すべての質問に [はい] 回答します。|  
## <a name="BKMK_examples"></a>例  
次のコマンドは、データ コレクターと呼ばれる perf_log を設定すると、コンピューター server_1 から XML ファイルの c:\windows\perf_log.xml をインポートします。  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
