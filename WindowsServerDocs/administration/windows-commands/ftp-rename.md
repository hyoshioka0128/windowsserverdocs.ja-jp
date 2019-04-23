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
ms.openlocfilehash: f99b3a43192a48e8adffaa60c25b46cfcaa8e3c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861863"
---
# <a name="ftp-rename"></a>ftp: 名前の変更

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ファイルの名前を変更します。   
## <a name="syntax"></a>構文  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<FileName>|名前を変更するファイルを指定します。|  
|<NewFileName>|新しいファイル名を指定します。|  
## <a name="BKMK_Examples"></a>例  
リモート ファイルの名前を変更**example.txt**に**example1.txt**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
