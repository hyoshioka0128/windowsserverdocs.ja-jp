---
title: dfsutil
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
robots: noindex,nofollow
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a06806b109bbd324213f935892bbbab415362df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377980"
---
# <a name="dfsutil"></a>dfsutil

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Dfsutil コマンドは、DFS 名前空間、サーバー、およびクライアントを管理します。 dfsutil コマンドでは、ほとんどのコマンドについて説明するように、更新された DFS 名前空間の用語を使用して、元の分散ファイルシステム用語を使用します。

このコマンドの使用方法の例については、「」を参照してください。 

## <a name="syntax"></a>構文

```
command </parameter> </param2>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|[dfsutil Root](dfsutil-root.md)|名前空間のルートを表示、作成、削除、インポート、エクスポートします。|
|[dfsutil リンク](dfsutil-link.md)|\)\(リンクを表示、作成、削除、または移動します。|
|[dfsutil ターゲット](dfsutil-target.md)|フォルダーターゲットまたは名前空間サーバーを表示、作成、削除します。|
|[dfsutil プロパティ](dfsutil-property.md)|フォルダーターゲットまたは名前空間サーバーを表示または変更します。|
|[dfsutil クライアント](dfsutil-client.md)|クライアント情報またはレジストリキーを表示または変更します。|
|[dfsutil サーバー](dfsutil-server.md)|名前空間の構成を表示または変更します。|
|[dfsutil Diag](dfsutil-diag.md)|診断を実行するか、dfs ディレクトリ\/dfspath を表示します。|
|[dfsutil ドメイン](dfsutil-domain.md)|ドメイン内のすべてのドメイン\-ベースの名前空間を表示します。|
|[dfsutil キャッシュ](dfsutil-cache.md)|クライアントキャッシュを表示またはフラッシュします。|
|[dfsutil oldcli](dfsutil-oldcli.md)|元の dfsutil 構文を使用するには、dfsutil \/oldcli コマンドを使用します。|

## <a name="remarks-optional-section"></a>解説 <optional section>
コマンドの最後で\) 名前空間サーバーなどのオブジェクト \(を指定した場合、ほとんどのコマンドには、追加のパラメーターやコマンドを必要とせずに、オブジェクトに関する情報が表示されます。 たとえば、dfsutil Root コマンドを使用する場合、コマンドに名前空間のルートを追加して、ルートに関する情報を表示できます。

## <a name="BKMK_Examples"></a>例
ここで &lt;、例の詳細な説明を入力します。&gt;

```
This /is /the /example /of /calling /command /with /parameters
```

ここで &lt;、別の例の詳細な説明を入力します。&gt;

```
This /is /a:different /example
```

## <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)


