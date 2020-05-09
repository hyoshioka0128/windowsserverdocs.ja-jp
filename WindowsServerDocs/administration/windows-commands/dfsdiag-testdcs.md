---
title: dfsdiag testdcs
description: 指定されたドメイン内のドメインコントローラーの構成をチェックする、dfs diag testdcs コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0bbe47474f99edb1626e61a372b02090d3a45ee3
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993001"
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

## <a name="examples"></a>使用例

*Contoso.com*ドメイン内のドメインコントローラーの構成を確認するには、次のように入力します。

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [dfsdiag コマンド](dfsdiag.md)
