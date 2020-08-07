---
title: dfsdiag testdfsconfig
description: 分散ファイルシステム (DFS) 名前空間の構成をチェックする、dfsdiag testdfsconfig のリファレンス記事。
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c714780d43f0fbd95c18f2041c54df8fd23282e8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891163"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag testdfsconfig

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のアクションを実行して、分散ファイルシステム (DFS) 名前空間の構成を確認します。

- DFS 名前空間サービスが実行されていること、およびすべての名前空間サーバーでそのスタートアップの種類が [**自動**] に設定されていることを確認します。

- DFS レジストリの構成が名前空間サーバー間で一貫していることを確認します。

- クラスター化された名前空間サーバーの次の依存関係を検証します。

  - 名前空間のルートリソースがネットワーク名リソースに依存しています。

  - IP アドレスリソースに対するネットワーク名リソースの依存関係。

  - 物理ディスクリソースに対する名前空間のルートリソースの依存関係。

## <a name="syntax"></a>構文

```
dfsdiag /testdfsconfig /DFSroot:<namespace>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /Dfs ルート:`<namespace>` | 診断する名前空間 (DFS ルート)。 |

## <a name="examples"></a>例

*Com\MyNamespace*で分散ファイルシステム (DFS) 名前空間の構成を確認するには、次のように入力します。

```
dfsdiag /testdfsconfig /DFSroot:\contoso.com\MyNamespace
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [dfsdiag コマンド](dfsdiag.md)
