---
title: dfsdiag TestDCs
description: Dfsdiag TestDCs の Windows コマンドに関するトピック。指定されたドメインのドメインコントローラーの構成を確認します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 092ce3710eb6d209f596683bd4ad054dadd11aa3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846321"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag TestDCs

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン内の各ドメインコントローラーで次のテストを実行して、ドメインコントローラーの構成を確認します。  
  
-   分散ファイルシステム (DFS) 名前空間サービスが実行されており、そのスタートアップの種類が [自動] に設定されていることを確認します。  
  
-   では、NETLOGON と SYSvol のサイトの見積もりの参照がサポートされているかどうかを確認します。  
  
-   ホスト名と IP アドレスによるサイトの関連付けの整合性を確認します。

## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|/Domain:`<domain_name>`|確認するドメイン。|  
  
## <a name="remarks"></a>コメント  

/Domain は省略可能なパラメーターです。 既定値は、ローカルホストが参加しているローカルドメインです。  
  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
Contoso.com ドメイン内のドメインコントローラーの構成を確認するには、次のように入力します。  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

