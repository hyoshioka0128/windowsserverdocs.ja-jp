---
title: ftp の名前変更
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80d1a15f038017444c7654a44748bfd22be8e487
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438381"
---
# <a name="ftp-rename"></a>ftp: 名前の変更

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ファイルの名前を変更します。   
## <a name="syntax"></a>構文  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>パラメーター  

|   パラメーター   |                 説明                 |
|---------------|---------------------------------------------|
|  <FileName>   | 名前を変更するファイルを指定します。 |
| <NewFileName> |        新しいファイル名を指定します。         |

## <a name="BKMK_Examples"></a>例  
リモート ファイルの名前を変更**example.txt**に**example1.txt**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
