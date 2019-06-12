---
title: ftp prompt_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65f7505dfcb3677fcaace9bd645cca7e7ba70b7d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438593"
---
# <a name="ftp-prompt1"></a>ftp: prompt_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

間で切り替わる **プロンプト** モード オン/オフします。   
## <a name="syntax"></a>構文  
```  
prompt  
```  
### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>注釈  
- 既定では、 **プロンプト** にします。  
- **ftp**選択的に取得およびファイルを保存することができるように複数のファイル転送中にメッセージが表示されます。  **Mget** と **mput** 場合は、すべてのファイルを転送 **プロンプト** は無効になっています。  
  ## <a name="BKMK_Examples"></a>例  
  オンとオフは、プロンプト モードを切り替えます。  
  ```  
  prompt  
  ```  
  ## <a name="additional-references"></a>その他の参照  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
