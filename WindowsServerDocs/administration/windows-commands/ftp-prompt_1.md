---
title: ftp prompt_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 08c7f9c14f4168bb5d3aa874711669eede8d0d87
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376201"
---
# <a name="ftp-prompt_1"></a>ftp: prompt_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

間で切り替わる **プロンプト** モード オン/オフします。   
## <a name="syntax"></a>構文  
```  
prompt  
```  
### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>コメント  
- 既定では、 **プロンプト** にします。  
- **ftp**では、ファイルを選択して取得または保存できるように、複数のファイル転送中にプロンプトが表示されます。  **Mget** と **mput** 場合は、すべてのファイルを転送 **プロンプト** は無効になっています。  
  ## <a name="BKMK_Examples"></a>例  
  オンとオフは、プロンプト モードを切り替えます。  
  ```  
  prompt  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
