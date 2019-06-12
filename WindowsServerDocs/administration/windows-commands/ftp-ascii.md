---
title: ascii を ftp します。
description: 'Windows コマンド」のトピックは、ascii を ftp します。 '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8e38c57b7a5ffd9afe677c4b49787383412621fe
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438800"
---
# <a name="ftp-ascii"></a>ftp: ascii

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ASCII ファイル転送の種類に設定します。   
## <a name="syntax"></a>構文  
```  
ascii  
```  
### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>注釈  
- 既定のファイル転送の種類は ASCII です。  
- ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 たとえば、対象のオペレーティング システムに基づいて、必要に応じて、行末の文字が変換されます。  
- **ftp** ASCII とバイナリの画像ファイル転送の種類の両方をサポートします。 テキスト ファイルを転送するときに、ASCII を使用します。 バイナリ ファイルの転送の詳細については、次を参照してください。 **ftp: バイナリ**で参照を追加します。  
  ## <a name="BKMK_Examples"></a>例  
  Ascii ファイル転送の種類を設定します。  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>その他の参照  
- [ftp: バイナリ](ftp-binary.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
