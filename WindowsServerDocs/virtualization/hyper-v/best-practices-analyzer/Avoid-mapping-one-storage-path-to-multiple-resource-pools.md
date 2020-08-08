---
title: 1つのストレージパスを複数のリソースプールにマップしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 38e0fdb5956197984a78d195ea23a7e856634575
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942070"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>1つのストレージパスを複数のリソースプールにマップしない

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|操作|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*ストレージファイルのパスは、複数のリソースプールにマップされます。*

## <a name="impact"></a>**影響**
*指定された記憶域プールの種類では、次の親プールと子プールが同じストレージパスを共有します。*

\<list of pools>

## <a name="resolution"></a>**解決策**
*複数のプールが同じストレージパスを使用しないように、Windows PowerShell を使用してストレージリソースプールを再構成します。*



