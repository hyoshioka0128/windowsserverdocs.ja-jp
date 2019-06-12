---
title: logman delete
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e396d79dc936f56a69fac9469c020348640f1094
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437782"
---
# <a name="logman-delete"></a>logman delete

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のデータ コレクターを削除します。  

## <a name="syntax"></a>構文  
```  
logman delete <[-n] <name>> [options]  
```  
## <a name="parameters"></a>パラメーター  

|        パラメーター        |                                                                               説明                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    ヘルプ コンテキストを表示します。                                                                     |
|   -s <computer name>    |                                                          指定したリモート コンピューター上のコマンドを実行します。                                                          |
|     -config <value>     |                                                         コマンド オプションを含む設定ファイルを指定します。                                                         |
|       [-n] <name>       |                                                                   ターゲットのデータ コレクターの名前です。                                                                    |
|          -ets           |                                              イベント トレース セッションを保存したり、スケジュール設定なしで直接コマンドを送信します。                                               |
| -[-] u < ユーザー [password] > | 実行するユーザーを指定します。 入力、\*のパスワードがパスワードのプロンプトが生成されます。 パスワード プロンプトで入力すると、パスワードは表示されません。 |

## <a name="BKMK_examples"></a>例  
次のコマンドは、データ コレクターの perf_log を削除します。  
```  
logman delete perf_log  
```  
#### <a name="additional-references"></a>その他の参照  
[logman](logman.md)  
