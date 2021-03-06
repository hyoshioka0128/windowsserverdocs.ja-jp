---
title: ftp の種類
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a261382da47501b416fa83c6d2497deae5711bb1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438348"
---
# <a name="ftp-type"></a>ftp: 型

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

## <a name="remarks"></a>注釈  
- 場合*typeName*が指定されていない、現在の型が表示されます。  
- **ftp**ファイル転送の種類、ASCII とバイナリを 2 つサポートします。  
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
  ## <a name="additional-references"></a>その他の参照  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
