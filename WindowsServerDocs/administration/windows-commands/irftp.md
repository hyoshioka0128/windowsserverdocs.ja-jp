---
title: irftp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d469270b744a9de881efd9b0cfa6f1105f70519a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848423"
---
# <a name="irftp"></a>irftp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

赤外線リンク経由でファイルを送信します。    
## <a name="syntax"></a>構文  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|ドライブ:\|赤外線リンク経由で送信するファイルが含まれているドライブを指定します。|  
|[path]FileName|赤外線リンク経由で送信するファイルの場所とファイルの名前を指定します。 一連のファイルを指定する場合は、各ファイルの完全なパスを指定する必要があります。|  
|/h|非表示モードを指定します。 非表示モードを使用すると、ワイヤレス リンク ダイアログ ボックスを表示せず、ファイルが送信されます。|  
|/s|ファイルまたはコマンドラインを使用して、ドライブ、パス、およびファイル名を指定せずに送信するファイルのセットを選択するには、ワイヤレス リンク ダイアログ ボックスが開きます。|  

## <a name="remarks"></a>注釈  
-   このコマンドを使用する前に、赤外線リンク経由で通信するデバイスが赤外線機能を有効にでき、正常に動作していること、およびデバイス間で赤外線リンクが確立されていることを確認します。  
-   パラメーターなしで使用したり **/s**、 **irftp**開きます、**ワイヤレス リンク** ダイアログ ボックスで、コマンドラインを使用せずに送信するファイルを選択できます。  

## <a name="BKMK_Examples"></a>例  
Example.txt を赤外線リンク経由で送信します。  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
