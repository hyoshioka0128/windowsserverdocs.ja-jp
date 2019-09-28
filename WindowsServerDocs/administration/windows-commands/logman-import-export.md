---
title: logman import |輸出
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 309274b5288bd1c17259e01cf563ae8685a2094e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374462"
---
# <a name="logman-import--export"></a>logman import |輸出

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

XML ファイルからデータコレクターセットをインポートするか、データコレクターセットを XML ファイルにエクスポートします。  

## <a name="syntax"></a>構文  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                        説明                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             状況依存のヘルプを表示します。                                                              |
|   -s <computer name>    |                                                   指定したリモートコンピューターでコマンドを実行します。                                                   |
|     -config <value>     |                                                  コマンドオプションを含む設定ファイルを指定します。                                                  |
|       [-n] <name>       |                                                                ターゲットオブジェクトの名前。                                                                 |
|       -xml <name>       |                                                         インポートまたはエクスポートする XML ファイルの名前。                                                         |
|          -/           |                                       イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。                                        |
| -[-] u < ユーザー [パスワード] > | 実行するユーザー。 パスワードの \* を入力すると、パスワードの入力を求めるプロンプトが生成されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
|           -y            |                                                      確認を求めずにすべての質問に対して [はい] を回答します。                                                       |

## <a name="BKMK_examples"></a>例  
次のコマンドは、perf_log というデータコレクターセットとしてコンピューター server_1 から XML ファイル c:\windows\perf_log.xml をインポートします。  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
