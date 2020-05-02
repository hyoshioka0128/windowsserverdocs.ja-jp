---
title: dfsdiag TestDCs
description: 指定されたドメイン内のドメインコントローラーの構成を確認する、dfsdiag TestDCs のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ac7fe1a7bae6a7b3dab9004b6212b7d93774ade
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719593"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag TestDCs

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン内の各ドメインコントローラーで次のテストを実行して、ドメインコントローラーの構成を確認します。  
  
-   分散ファイルシステム (DFS) 名前空間サービスが実行されており、そのスタートアップの種類が [自動] に設定されていることを確認します。  
  
-   では、NETLOGON と SYSvol のサイトの見積もりの参照がサポートされているかどうかを確認します。  
  
-   ホスト名と IP アドレスによるサイトの関連付けの整合性を確認します。

## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|[説明]|  
|-------|--------|  
|領域`<domain_name>`|確認するドメイン。|  
  
## <a name="remarks"></a>Remarks  

/Domain は省略可能なパラメーターです。 既定値は、ローカルホストが参加しているローカルドメインです。  
  
## <a name="examples"></a>例  
Contoso.com ドメイン内のドメインコントローラーの構成を確認するには、次のように入力します。  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

