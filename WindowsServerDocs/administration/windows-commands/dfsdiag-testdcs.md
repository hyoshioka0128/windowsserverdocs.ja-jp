---
title: dfsdiag TestDCs
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a193e68b6f015b1535a98e20b52deb2a4a14034c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378439"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag TestDCs

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン内の各ドメインコントローラーで次のテストを実行して、ドメインコントローラーの構成を確認します。  
  
-   分散ファイルシステム \(DFS @ no__t 名前空間サービスが実行されており、そのスタートアップの種類が [自動] に設定されていることを確認します。  
  
-   では、NETLOGON と SYSvol のサイト @ no__t-0costed 参照がサポートされているかどうかを確認します。  
  
-   ホスト名と IP アドレスによるサイトの関連付けの整合性を確認します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/Domain: <Domain name>|確認するドメイン。|  
  
## <a name="remarks"></a>コメント  
\/Domain は省略可能なパラメーターです。 既定値は、ローカルホストが参加しているローカルドメインです。  
  
## <a name="BKMK_Examples"></a>例  
Contoso.com ドメイン内のドメインコントローラーの構成を確認するには、次のように入力します。  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

