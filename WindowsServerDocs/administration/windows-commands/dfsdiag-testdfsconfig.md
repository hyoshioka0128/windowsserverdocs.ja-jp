---
title: dfsdiag TestDFSConfig
description: 分散ファイルシステム (DFS) 名前空間の構成をチェックする、dfsdiag TestDFSConfig のリファレンストピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 057b0662fddb7148837be16380d190cdb37382c5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719587"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag TestDFSConfig

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のアクションを実行して、分散ファイルシステム (DFS) 名前空間の構成を確認します。  
  
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
  
#### <a name="parameters"></a>パラメーター  
  
|       パラメーター       |               [説明]               |
|-----------------------|-----------------------------------------|
| /Dfs ルート:`<namespace>` | 診断する名前空間 (DFS ルート)。 |
  
## <a name="examples"></a>例  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

