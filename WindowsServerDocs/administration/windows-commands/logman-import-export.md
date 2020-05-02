---
title: logman import |輸出
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffc2e42f353352f69cf61dfb1f108a7d53cb7c4b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724360"
---
# <a name="logman-import--export"></a>logman import |輸出

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

XML ファイルからデータコレクターセットをインポートするか、データコレクターセットを XML ファイルにエクスポートします。  

## <a name="syntax"></a>構文  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                        [説明]                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             状況依存のヘルプを表示します。                                                              |
|   -s<computer name>    |                                                   指定したリモートコンピューターでコマンドを実行します。                                                   |
|     -config <value>     |                                                  コマンドオプションを含む設定ファイルを指定します。                                                  |
|       [-n]<name>       |                                                                対象オブジェクトの名前。                                                                 |
|       -xml<name>       |                                                         インポートまたはエクスポートする XML ファイルの名前。                                                         |
|          -/           |                                       イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。                                        |
| -[-] u <ユーザー [パスワード] > | 実行するユーザー。 パスワードの\*を入力すると、パスワードの入力を求めるメッセージが表示されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |
|           -y            |                                                      確認を求めずにすべての質問に対して [はい] を回答します。                                                       |

## <a name="examples"></a>例  
次のコマンドは、perf_log という名前のデータコレクターセットとしてコンピューター server_1 から XML ファイル c:\ をインポートし perf_log します。  
```  
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml  
```  
## <a name="additional-references"></a>その他のリファレンス  
[logman](logman.md)  
