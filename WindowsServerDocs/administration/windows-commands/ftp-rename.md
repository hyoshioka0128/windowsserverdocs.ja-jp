---
title: ftp の名前変更
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5dc5006c82df8417a8652a9c0ba20f7f1a002e7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725109"
---
# <a name="ftp-rename"></a>ftp: 名前の変更

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートファイルの名前を変更します。   
## <a name="syntax"></a>構文  
```  
rename <FileName> <NewFileName>  
```  
#### <a name="parameters"></a>パラメーター  

|   パラメーター   |                 [説明]                 |
|---------------|---------------------------------------------|
|  <FileName>   | 名前を変更するファイルを指定します。 |
| <NewFileName> |        新しいファイル名を指定します。         |

## <a name="examples"></a>例  
リモートファイルの**例**の名前を example1 に変更し**ます**。  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
