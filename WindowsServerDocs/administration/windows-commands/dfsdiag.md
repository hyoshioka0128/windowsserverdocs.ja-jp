---
title: dfsdiag
description: DFS 名前空間の診断情報を提供する dfsdiag コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97f39d740bc321ebcece69ff0690dfac7aab6567
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928664"
---
# <a name="dfsdiag"></a>dfsdiag

DFS 名前空間の診断情報を提供します。

## <a name="syntax"></a>構文

```
dfsdiag /testdcs [/domain:<domain name>]
dfsdiag /testsites </machine:<server name>| /DFSPath:<namespace root or DFS folder> [/recurse]> [/full]
dfsdiag /testdfsconfig /DFSRoot:<namespace>
dfsdiag /testdfsintegrity /DFSRoot:<DFS root path> [/recurse] [/full]
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | ドメインコントローラーの構成を確認します。 |
| [dfsdiag testsites](dfsdiag-testsites.md) | サイトの関連付けを確認します。 |
| [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | DFS 名前空間の構成を確認します。 |
| [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | DFS 名前空間の整合性を確認します。 |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | 紹介応答を確認します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
