---
title: irftp
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ad8a0b9b49d90223f830081f5a99c40995d9e4ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375364"
---
# <a name="irftp"></a>irftp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

赤外線リンクを介してファイルを送信します。    
## <a name="syntax"></a>構文  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|Drive: \|Specifies リンクを介して送信するファイルが格納されているドライブを指定します。|  
|道/Db|赤外線リンクを介して送信するファイルまたはファイルのセットの場所と名前を指定します。 ファイルのセットを指定する場合は、各ファイルの完全なパスを指定する必要があります。|  
|/h|非表示モードを指定します。 非表示モードを使用すると、[ワイヤレスリンク] ダイアログボックスを表示せずにファイルが送信されます。|  
|/s|[ワイヤレスリンク] ダイアログボックスを開きます。これにより、コマンドラインを使用せずに、ドライブ、パス、およびファイル名を指定して、送信するファイルまたはファイルのセットを選択できます。|  

## <a name="remarks"></a>コメント  
-   このコマンドを使用する前に、赤外線リンクを介して通信するデバイスで赤外線機能が有効になっており、正常に動作していること、およびデバイス間に赤外線リンクが確立されていることを確認してください。  
-   パラメーターを指定せずに使用するか、 **/s**と共に使用すると、 **Irftp**は **[ワイヤレスリンク]** ダイアログボックスを開きます。このダイアログボックスでは、コマンドラインを使用せずに、送信するファイルを選択できます。  

## <a name="BKMK_Examples"></a>例  
赤外線リンク経由で例 .txt を送信します。  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
