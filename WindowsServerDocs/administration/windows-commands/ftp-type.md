---
title: ftp の種類
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb254d1c9b17ac6baadf6b84702d2812f1117a93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375899"
---
# <a name="ftp-type"></a>ftp: 種類

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

設定またはファイル転送の種類を表示します。   
## <a name="syntax"></a>構文  
```  
type [<typeName>]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |            説明            |
|--------------|-----------------------------------|
| [<typeName>] | ファイル転送の種類を指定します。 |

## <a name="remarks"></a>コメント  
- *typeName*が指定されていない場合は、現在の型が表示されます。  
- **ftp**では、ASCII とバイナリという2種類のファイル転送がサポートされています。  
  既定のファイル転送の種類は ASCII です。  **Ascii** コマンドは、テキスト ファイルを転送するときに使用する必要があります。 ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 行末の文字は変換など、転送先にオペレーティング システムに基づき、必要です。  
  **バイナリ** コマンドは、実行可能ファイルを転送するときに使用する必要があります。 バイナリ モードでは、1 バイト単位で、ファイルが移動します。  
  ## <a name="BKMK_Examples"></a>例  
  Ascii ファイル転送の種類を設定します。  
  ```  
  type ascii  
  ```  
  転送ファイルの種類をバイナリに設定します。  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
