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
ms.openlocfilehash: b7bcca3f29cec8ff5c30256dfd123acc7fbb804d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849193"
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
-   既定のファイル転送の種類は ASCII です。  
-   ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 たとえば、対象のオペレーティング システムに基づいて、必要に応じて、行末の文字が変換されます。  
-   **ftp** ASCII とバイナリの画像ファイル転送の種類の両方をサポートします。 テキスト ファイルを転送するときに、ASCII を使用します。 バイナリ ファイルの転送の詳細については、次を参照してください。 **ftp: バイナリ**で参照を追加します。  
## <a name="BKMK_Examples"></a>例  
Ascii ファイル転送の種類を設定します。  
```  
ascii  
```  
## <a name="additional-references"></a>その他の参照  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
