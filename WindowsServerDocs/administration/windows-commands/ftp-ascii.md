---
title: ftp ascii
description: Ftp ascii のリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa33637f43ef8d26635f36b40dbd21cfe2bff42e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725392"
---
# <a name="ftp-ascii"></a>ftp: ascii

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送の種類を ASCII に設定します。   
## <a name="syntax"></a>構文  
```  
ascii  
```  
#### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>Remarks  
- 既定のファイル転送の種類は ASCII です。  
- ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 たとえば、行末の文字は、対象のオペレーティングシステムに基づいて必要に応じて変換されます。  
- **ftp**では、ASCII とバイナリの両方のイメージファイル転送がサポートされています。 テキストファイルを転送するときは、ASCII を使用します。 バイナリファイル転送の詳細については、「 **ftp:** 追加の参照でのバイナリ」を参照してください。  
  ## <a name="examples"></a>例  
  Ascii ファイル転送の種類を設定します。  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- [ftp: バイナリ](ftp-binary.md)  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
