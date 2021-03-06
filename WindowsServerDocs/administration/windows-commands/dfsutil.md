---
title: dfsutil
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 45545b4e12d31c293ead5b18b83efd50d7bc37bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439653"
---
# <a name="dfsutil"></a>dfsutil

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Dfsutil コマンドは、DFS 名前空間、サーバーおよびクライアントを管理します。 dfsutil コマンドは、ほとんどのコマンドの説明として提供される更新の DFS 名前空間用語と、元の分散ファイル システムの用語を使用します。

このコマンドの使用方法の例については、次を参照してください。 

## <a name="syntax"></a>構文

```
command </parameter> </param2>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|[dfsutil Root](dfsutil-root.md)|表示されます、作成を削除します、インポート、名前空間のルートをエクスポートします。|
|[dfsutil リンク](dfsutil-link.md)|表示、作成、削除、またはフォルダーに移動\(リンク\)します。|
|[dfsutil ターゲット](dfsutil-target.md)|表示されたらは、作成、フォルダー ターゲットまたは名前空間サーバーを削除します。|
|[dfsutil プロパティ](dfsutil-property.md)|表示またはフォルダー ターゲットまたは名前空間サーバーを変更します。|
|[dfsutil クライアント](dfsutil-client.md)|表示またはクライアントの情報またはレジストリ キーを変更します。|
|[dfsutil サーバー](dfsutil-server.md)|表示または名前空間の構成を変更します。|
|[dfsutil 診断](dfsutil-diag.md)|診断を実行または表示 dfsdirs\/dfspath します。|
|[dfsutil ドメイン](dfsutil-domain.md)|すべてのドメインが表示されます\-ベースのドメイン内の名前空間。|
|[dfsutil キャッシュ](dfsutil-cache.md)|表示またはクライアント キャッシュをフラッシュします。|
|[dfsutil oldcli](dfsutil-oldcli.md)|使用、dfsutil \/oldcli コマンドで、元の dfsutil 構文の使用します。|

## <a name="remarks-optional-section"></a>「解説」 <optional section>
オブジェクトを指定した場合\(名前空間サーバーなど\)ほとんどのコマンドがパラメーターやコマンドは、さらに必要とせず、オブジェクトに関する情報を表示するコマンドの最後に、します。 たとえば、dfsutil Root コマンドを使用する場合は、ルートに関する情報を表示するコマンドに名前空間のルートを追加できます。

## <a name="BKMK_Examples"></a>例
&lt;次に、例の詳細な説明を配置する場所を示します。&gt;

```
This /is /the /example /of /calling /command /with /parameters
```

&lt;別の例の詳細な説明を配置する場所を示します。&gt;

```
This /is /a:different /example
```

## <a name="additional-references"></a>その他の参照

-   [コマンド ライン構文の記号](command-line-syntax-key.md)


