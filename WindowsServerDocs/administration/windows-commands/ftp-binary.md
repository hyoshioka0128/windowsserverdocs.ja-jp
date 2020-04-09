---
title: ftp バイナリ
description: Ftp バイナリの Windows コマンドに関するトピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20b2f72517826576cfee643eda0c54063b162c94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843725"
---
# <a name="ftp-binary"></a>ftp: バイナリ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送の種類をバイナリに設定します。   
## <a name="syntax"></a>構文  
```  
binary  
```  
#### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks-optional-section"></a>解説 <optional section>  
**ftp**では、ASCII とバイナリの両方のイメージファイル転送がサポートされています。 実行可能ファイルを転送するときにバイナリを使用します。 バイナリモードでは、ファイルは1バイト単位で転送されます。 ASCII ファイル転送の詳細については、「 **ftp:** その他の参照情報」を参照してください。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
ファイル転送の種類をバイナリに設定します。  
```  
binary  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
