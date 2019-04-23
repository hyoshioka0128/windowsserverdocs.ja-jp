---
title: Dfsdiag TestDFSIntegrity
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a79e034f7c60be89266eb29dcd69e8f73b2aafe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837093"
---
# <a name="dfsdiag-testdfsintegrity"></a>Dfsdiag TestDFSIntegrity

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

分散ファイル システムの整合性をチェック\(DFS\)次のテストを実行することによって名前空間。  
  
-   DFS のメタデータの破損またはドメイン コント ローラーの間の不整合を確認します。  
  
-   アクセスの構成を検証\-ベースの列挙が DFS メタデータと名前空間サーバーの共有間で一貫性のあることを確認します。  
  
-   重複する DFS フォルダーが検出\(リンク\)、重複するフォルダーおよびフォルダー ターゲットを重複しているフォルダー。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/します。<DFS root path>|DFS 名前空間を診断します。|  
|\/Recurse|名前空間のインター リンク テストなどを実行します。|  
|\/完全です|共有とすべてのフォルダー ターゲット上で NTFS の Acl とクライアント側の構成の一貫性を確認します。 オンライン プロパティを設定することも確認します。|  
  
## <a name="BKMK_Examples"></a>例  
TBD を入力します。  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

