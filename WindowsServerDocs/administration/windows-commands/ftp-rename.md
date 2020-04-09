---
title: ftp の名前変更
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbe159f2833ce52921b46e46881a1d7aed8c5df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843025"
---
# <a name="ftp-rename"></a>ftp: 名前の変更

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートファイルの名前を変更します。   
## <a name="syntax"></a>構文  
```  
rename <FileName> <NewFileName>  
```  
#### <a name="parameters"></a>パラメーター  

|   パラメーター   |                 説明                 |
|---------------|---------------------------------------------|
|  <FileName>   | 名前を変更するファイルを指定します。 |
| <NewFileName> |        新しいファイル名を指定します。         |

## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモートファイルの**例**の名前を example1 に変更し**ます**。  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
