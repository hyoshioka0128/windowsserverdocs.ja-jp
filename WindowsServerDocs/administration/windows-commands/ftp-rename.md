---
title: ftp の名前変更
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 977baa042a6b0d9c23db7cb398bee997c2049227
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376018"
---
# <a name="ftp-rename"></a>ftp: 名前の変更

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートファイルの名前を変更します。   
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
リモートファイルの**例**の名前を example1 に変更し**ます**。  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
