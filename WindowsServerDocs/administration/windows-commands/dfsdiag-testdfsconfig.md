---
title: Dfsdiag TestDFSConfig
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 922b78b87f3bb66765b87348a3bf136e14c9e837
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436129"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag TestDFSConfig

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

分散ファイル システムの構成をチェック\(DFS\)次の操作を実行することによって名前空間。  
  
-   DFS Namespace サービスが実行されていることと、名前空間のすべてのサーバー上で、スタートアップの種類を自動に設定されていることを確認します。  
  
-   DFS のレジストリ構成に名前空間サーバー間で整合性があることを確認します。  
  
-   Windows Server 2008 またはそれ以降を実行するクラスター化された名前空間サーバーで次の依存関係を検証します。  
  
    -   Namespace ネットワーク名リソースに依存関係のリソースをルートです。  
  
    -   ネットワークの IP アドレス リソースのリソースの依存関係の名前。  
  
    -   Namespace 物理ディスク リソースの依存関係のリソースをルートです。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
### <a name="parameters"></a>パラメーター  
  
|       パラメーター       |               説明               |
|-----------------------|-----------------------------------------|
| \/します。<namespace> | 名前空間\(DFS ルート\)を診断します。 |
  
## <a name="BKMK_Examples"></a>例  
TBD を入力します。  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

