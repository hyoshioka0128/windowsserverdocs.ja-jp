---
title: dfsdiag TestDFSIntegrity
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7f344e2d1fecc542efc39688f20165fd3e39a04a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378430"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag TestDFSIntegrity

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム \(DFS @ no__t 名前空間の整合性をチェックします。  
  
-   DFS メタデータの破損またはドメインコントローラー間の不整合を確認します。  
  
-   Access @ no__t-0based 列挙型の構成を検証して、DFS メタデータと名前空間サーバー共有の間で一貫性があることを確認します。  
  
-   では、重複する DFS @no__t フォルダーが検出されます。 0links @ no__t、重複するフォルダー、フォルダーターゲットが重複しているフォルダーを検出します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/DFSRoot: <DFS root path>|診断する DFS 名前空間。|  
|\/Recurse|名前空間の interlinks を含むテストを実行します。|  
|\/Full|すべてのフォルダーターゲットで、共有と NTFS Acl およびクライアント側の構成の整合性を確認します。 また、online プロパティが設定されていることを確認します。|  
  
## <a name="BKMK_Examples"></a>例  
次のように入力します。  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

