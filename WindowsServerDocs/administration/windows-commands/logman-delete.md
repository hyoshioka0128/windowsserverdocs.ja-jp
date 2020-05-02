---
title: logman delete
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b30fd6eb7915d3d0296988a98968dcde58bdbc2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724373"
---
# <a name="logman-delete"></a>logman delete

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のデータコレクターを削除します。  

## <a name="syntax"></a>構文  
```  
logman delete <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                               説明                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    状況依存のヘルプを表示します。                                                                     |
|   -s<computer name>    |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|     -config <value>     |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|       [-n]<name>       |                                                                   ターゲットデータコレクターの名前。                                                                    |
|          -/           |                                              イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。                                               |
| -[-] u <ユーザー [パスワード] > | として実行するユーザーを指定します。 パスワードの\*を入力すると、パスワードの入力を求めるメッセージが表示されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |

## <a name="examples"></a>例  
次のコマンドを実行すると、データコレクター perf_log が削除されます。  
```  
logman delete perf_log  
```  
## <a name="additional-references"></a>その他のリファレンス  
[logman](logman.md)  
