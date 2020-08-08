---
title: フォルダー ターゲットの追加
description: このトピックでは、フォルダー ターゲット (UNC パス) を追加する方法について説明します。
ms.author: jgerend
manager: brianlic
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: bc229360a616e7fa56231e6211b4b909d45ec2de
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957820"
---
# <a name="add-folder-targets"></a>フォルダー ターゲットの追加

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

フォルダー ターゲットは、共有フォルダー、または名前空間内のフォルダーに関連付けられた別の名前空間の汎用名前付け規則 (UNC) パスです。 複数のフォルダー ターゲットを追加すると、名前空間の可用性が向上します。

## <a name="to-add-a-folder-target"></a>フォルダー ターゲットを追加するには

DFS の管理を使ってフォルダー ターゲットを追加するには、次の手順を使用します。

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの [**名前空間**] ノードで、フォルダーを右クリックし、[**フォルダー ターゲットを追加**] をクリックします。

3.  フォルダー ターゲットのパスを入力するか、[**参照**] をクリックしてフォルダー ターゲットを見つけます。

4.  フォルダーが DFS レプリケーションを使ってレプリケートされる場合、レプリケーション グループに新しいフォルダー ターゲットを追加するかどうかを指定できます。

> [!TIP]
> Windows PowerShell を使ってフォルダー ターゲットを追加するには、[New-DfsnFolderTarget](/powershell/module/dfsn/new-dfsnfoldertarget) コマンドレットを使います。 DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。

> [!NOTE]
> フォルダーには、フォルダー ターゲットまたは他の DFS フォルダーを含めることができますが、フォルダー階層の同じレベルに両方を含めることはできません。

## <a name="additional-references"></a>その他の参照情報

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS レプリケーションを使用してフォルダーターゲットをレプリケートする](replicate-folder-targets-using-dfs-replication.md)
