---
title: ftp ユーザー
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb4f0f47f23bec312c57266479c261c96535e8cc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725061"
---
# <a name="ftp-user"></a>ftp: ユーザー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューターにユーザーを指定します。   
## <a name="syntax"></a>構文  
```  
user <UserName> [<Password>] [<Account>]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                                                                      [説明]                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          リモート コンピューターへのログオンに使用するユーザー名を指定します。                                           |
| [<Password>] |               パスワードを指定 *UserName*します。 パスワードが指定されていない場合は必須では  **ftp** パスワードを入力するように求められます。               |
| [<Account>]  | リモート コンピューターへのログオンに使用するアカウントを指定します。 場合、 *アカウント* が指定されていないが必要な  **ftp** アカウントのメッセージが表示されます。 |

## <a name="examples"></a>例  
Password1 パスワードを使用して User1 を指定します。  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
