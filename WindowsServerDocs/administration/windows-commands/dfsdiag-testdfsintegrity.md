---
title: dfsdiag TestDFSIntegrity
description: 分散ファイルシステム (DFS) 名前空間の整合性をチェックする**dfsdiag TestDFSIntegrity**のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21aa6ef3d7d4a7b4a9c64fc51aec77f49f1e0a0c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719576"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag TestDFSIntegrity

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム (DFS) 名前空間の整合性をチェックします。

- DFS メタデータの破損またはドメインコントローラー間の不整合を確認します。

- アクセスベースの列挙の構成を検証して、DFS メタデータと名前空間サーバー共有の間で一貫性があることを確認します。

- 重複する DFS フォルダー (リンク)、重複するフォルダー、フォルダーターゲットが重複するフォルダーを検出します。

## <a name="syntax"></a>構文

```
dfsdiag /TestDFSIntegrity /DFSRoot: <DFS root path> [/Recurse] [/Full]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
|-------|--------|
| /Dfs ルート:`<DFS root path>`| 診断する DFS 名前空間。 |
| /Recurse | 名前空間の interlinks を含むテストを実行します。 |
| /Full | すべてのフォルダーターゲットで、共有と NTFS Acl およびクライアント側の構成の整合性を確認します。 また、online プロパティが設定されていることを確認します。 |

## <a name="examples"></a>例

```
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

-   [dfsdiag](dfsdiag.md)


