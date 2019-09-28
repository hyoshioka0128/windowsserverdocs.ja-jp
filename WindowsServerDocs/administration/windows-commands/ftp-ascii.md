---
title: ftp ascii
description: 'Ftp ascii の Windows コマンドに関するトピック '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5ae0064f9c1679bb8b386271f042d589b158c73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376622"
---
# <a name="ftp-ascii"></a>ftp: ascii

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送の種類を ASCII に設定します。   
## <a name="syntax"></a>構文  
```  
ascii  
```  
### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>コメント  
- 既定のファイル転送の種類は ASCII です。  
- ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 たとえば、行末の文字は、対象のオペレーティングシステムに基づいて必要に応じて変換されます。  
- **ftp**では、ASCII とバイナリの両方のイメージファイル転送がサポートされています。 テキストファイルを転送するときは、ASCII を使用します。 バイナリファイル転送の詳細については、「 **ftp:** 追加の参照でのバイナリ」を参照してください。  
  ## <a name="BKMK_Examples"></a>例  
  Ascii ファイル転送の種類を設定します。  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [ftp: バイナリ](ftp-binary.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
