---
title: dfsdiag TestDFSIntegrity
description: DFS (分散ファイルシステム) 名前空間の整合性をチェックする、 **dfsdiag TestDFSIntegrity**の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 714b79369898338a4e4a6e4fad8487709ab4fc60
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846275"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag TestDFSIntegrity

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム (DFS) 名前空間の整合性をチェックします。

- DFS メタデータの破損またはドメインコントローラー間の不整合を確認します。

- アクセスベースの列挙の構成を検証して、DFS メタデータと名前空間サーバー共有の間で一貫性があることを確認します。

- 重複する DFS フォルダー (リンク)、重複するフォルダー、フォルダーターゲットが重複するフォルダーを検出します。

## <a name="syntax"></a>構文

```
dfsdiag /TestDFSIntegrity /DFSRoot: <DFS root path> [/Recurse] [/Full]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|-------|--------|
| /Dfs ルート: `<DFS root path>`| 診断する DFS 名前空間。 |
| /Recurse | 名前空間の interlinks を含むテストを実行します。 |
| /Full | すべてのフォルダーターゲットで、共有と NTFS Acl およびクライアント側の構成の整合性を確認します。 また、online プロパティが設定されていることを確認します。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例

```
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

-   [dfsdiag](dfsdiag.md)


