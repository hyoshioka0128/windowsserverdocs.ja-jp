---
title: ftp の種類
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5531da30118914599ed0f85bfd10bd02ae89ffcf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725086"
---
# <a name="ftp-type"></a>ftp: 種類

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

設定またはファイル転送の種類を表示します。   
## <a name="syntax"></a>構文  
```  
type [<typeName>]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |            [説明]            |
|--------------|-----------------------------------|
| [<typeName>] | ファイル転送の種類を指定します。 |

## <a name="remarks"></a>Remarks  
- *typeName*が指定されていない場合は、現在の型が表示されます。  
- **ftp**では、ASCII とバイナリという2種類のファイル転送がサポートされています。  
  既定のファイル転送の種類は ASCII です。  **Ascii** コマンドは、テキスト ファイルを転送するときに使用する必要があります。 ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 行末の文字は変換など、転送先にオペレーティング システムに基づき、必要です。  
  **バイナリ** コマンドは、実行可能ファイルを転送するときに使用する必要があります。 バイナリ モードでは、1 バイト単位で、ファイルが移動します。  
  ## <a name="examples"></a>例  
  Ascii ファイル転送の種類を設定します。  
  ```  
  type ascii  
  ```  
  転送ファイルの種類をバイナリに設定します。  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
