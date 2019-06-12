---
title: ftp ユーザー
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1c9406af0868421fa54fe757742cf2a120561b9c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438344"
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
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
