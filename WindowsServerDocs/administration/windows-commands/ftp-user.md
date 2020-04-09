---
title: ftp ユーザー
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29081bd8c5d537e1f060e4c848b720a60b4c8aea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842855"
---
# <a name="ftp-user"></a>ftp: ユーザー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューターにユーザーを指定します。   
## <a name="syntax"></a>構文  
```  
user <UserName> [<Password>] [<Account>]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                                                                      説明                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          リモート コンピューターへのログオンに使用するユーザー名を指定します。                                           |
| [<Password>] |               パスワードを指定 *UserName*します。 パスワードが指定されていない場合は必須では  **ftp** パスワードを入力するように求められます。               |
| [<Account>]  | リモート コンピューターへのログオンに使用するアカウントを指定します。 場合、 *アカウント* が指定されていないが必要な  **ftp** アカウントのメッセージが表示されます。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例  
Password1 パスワードを使用して User1 を指定します。  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
