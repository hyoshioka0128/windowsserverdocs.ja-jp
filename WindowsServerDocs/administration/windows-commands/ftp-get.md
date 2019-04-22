---
title: ftp の取得
description: Ftp の Windows コマンド」のトピックを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 798317f3921cd0e5ff12b69b972e2ea423fa6b3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816733"
---
# <a name="ftp-get"></a>ftp: 取得

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<remoteFile>|コピーするリモート ファイルを指定します。|  
|[<LocalFile>]|ローカル コンピューターで使用するファイルの名前を指定します。 場合*ローカルファイル*が指定されていない、ファイルが指定された、 *remoteFile*名。|  
## <a name="remarks"></a>注釈  
**取得**コマンドと同じ、 **recv**コマンド。  
## <a name="BKMK_Examples"></a>例  
コピー **test.txt**現在のファイル転送の種類を使用してローカル コンピューターにします。  
```  
get test.txt  
```  
コピー **test.txt**として、ローカル コンピューターに**test1.txt**転送の種類を現在のファイルを使用します。  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
