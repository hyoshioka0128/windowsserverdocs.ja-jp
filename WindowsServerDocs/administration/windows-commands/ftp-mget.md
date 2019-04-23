---
title: ftp mget
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1160ec742dde318141da720bd35b7d60ab805bb1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888423"
---
# <a name="ftp-mget"></a>ftp: mget

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<remoteFile>|ローカル コンピューターにコピーするリモート ファイルを指定します。|  
## <a name="BKMK_Examples"></a>例  
リモート ファイルをコピー **a.exe**と**b.exe**現在のファイル転送の種類を使用してローカル コンピューターにします。  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
