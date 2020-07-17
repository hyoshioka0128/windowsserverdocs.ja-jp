---
title: dfsdiag testdcs
description: 指定されたドメイン内のドメインコントローラーの構成をチェックする、dfs diag testdcs コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eca75d233661d51a36b52b79230ad36b704e203
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930660"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag testdcs

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン内の各ドメインコントローラーで次のテストを実行して、ドメインコントローラーの構成を確認します。

- 分散ファイルシステム (DFS) 名前空間サービスが実行されており、そのスタートアップの種類が [**自動**] に設定されていることを確認します。

- では、NETLOGON と SYSvol のサイトの見積もりの参照がサポートされているかどうかを確認します。

- ホスト名と IP アドレスによるサイトの関連付けの整合性を確認します。

## <a name="syntax"></a>構文

```
dfsdiag /testdcs [/domain:<domain_name>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /domain`<domain_name>` | 確認するドメインの名前。 このパラメーターは省略可能です。 既定値は、ローカルホストが参加しているローカルドメインです。 |

## <a name="examples"></a>例

*Contoso.com*ドメイン内のドメインコントローラーの構成を確認するには、次のように入力します。

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [dfsdiag コマンド](dfsdiag.md)
