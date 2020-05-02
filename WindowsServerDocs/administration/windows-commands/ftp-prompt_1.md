---
title: ftp prompt_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1abb697316a1072a9185a5132dfd22a1d8fd67dd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725181"
---
# <a name="ftp-prompt_1"></a>ftp: prompt_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

間で切り替わる **プロンプト** モード オン/オフします。   
## <a name="syntax"></a>構文  
```  
prompt  
```  
#### <a name="parameters"></a>パラメーター  
なし  
## <a name="remarks"></a>Remarks  
- 既定では、 **プロンプト** にします。  
- **ftp**では、ファイルを選択して取得または保存できるように、複数のファイル転送中にプロンプトが表示されます。  **Mget** と **mput** 場合は、すべてのファイルを転送 **プロンプト** は無効になっています。  
  ## <a name="examples"></a>例  
  オンとオフは、プロンプト モードを切り替えます。  
  ```  
  prompt  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
