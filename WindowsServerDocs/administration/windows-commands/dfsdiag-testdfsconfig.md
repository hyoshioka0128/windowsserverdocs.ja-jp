---
title: dfsdiag TestDFSConfig
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8008e02d588edaa6fe7700a331c43f9680d89431
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378420"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag TestDFSConfig

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次の操作を実行して、分散ファイルシステム \(DFS\) 名前空間の構成を確認します。  
  
-   DFS 名前空間サービスが実行されていること、およびすべての名前空間サーバーでそのスタートアップの種類が [自動] に設定されていることを確認します。  
  
-   DFS レジストリの構成が名前空間サーバー間で一貫していることを確認します。  
  
-   は、Windows Server 2008 以降を実行しているクラスター化された名前空間サーバーで、次の依存関係を検証します。  
  
    -   名前空間のルートリソースがネットワーク名リソースに依存しています。  
  
    -   IP アドレスリソースに対するネットワーク名リソースの依存関係。  
  
    -   物理ディスクリソースに対する名前空間のルートリソースの依存関係。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
### <a name="parameters"></a>パラメーター  
  
|       パラメーター       |               説明               |
|-----------------------|-----------------------------------------|
| \/DFSRoot:<namespace> | 診断する DFS ルート\) \(名前空間。 |
  
## <a name="BKMK_Examples"></a>例  
次のように入力します。  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

