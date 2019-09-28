---
title: ftp ユーザー
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63281a0ffdd646d3652eb3a442a8edd9acec9cce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375870"
---
# <a name="ftp-user"></a>ftp: ユーザー

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューターにユーザーを指定します。   
## <a name="syntax"></a>構文  
```  
user <UserName> [<Password>] [<Account>]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                                                                      説明                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          リモート コンピューターへのログオンに使用するユーザー名を指定します。                                           |
| [<Password>] |               パスワードを指定 *UserName*します。 パスワードが指定されていない場合は必須では  **ftp** パスワードを入力するように求められます。               |
| [<Account>]  | リモート コンピューターへのログオンに使用するアカウントを指定します。 場合、 *アカウント* が指定されていないが必要な  **ftp** アカウントのメッセージが表示されます。 |

## <a name="BKMK_Examples"></a>例  
Password1 パスワードを使用して User1 を指定します。  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
