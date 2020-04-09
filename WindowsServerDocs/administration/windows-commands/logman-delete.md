---
title: logman delete
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0ab38eab988770de4fbcef8af2c7be6a6137b16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840755"
---
# <a name="logman-delete"></a>logman delete

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のデータコレクターを削除します。  

## <a name="syntax"></a>構文  
```  
logman delete <[-n] <name>> [options]  
```  
### <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                               説明                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    状況依存のヘルプを表示します。                                                                     |
|   -s <computer name>    |                                                          指定したリモートコンピューターでコマンドを実行します。                                                          |
|     -config <value>     |                                                         コマンドオプションを含む設定ファイルを指定します。                                                         |
|       [-n] <name>       |                                                                   ターゲットデータコレクターの名前。                                                                    |
|          -/           |                                              イベントを保存またはスケジュールせずに直接イベントトレースセッションに送信します。                                               |
| -[-] u < ユーザー [パスワード] > | として実行するユーザーを指定します。 パスワードの \* を入力すると、パスワードの入力を求めるプロンプトが生成されます。 パスワードは、パスワードプロンプトで入力しても表示されません。 |

## <a name="examples"></a><a name=BKMK_examples></a>例  
次のコマンドを実行すると、データコレクター perf_log が削除されます。  
```  
logman delete perf_log  
```  
## <a name="additional-references"></a>その他の参照情報  
[logman](logman.md)  
