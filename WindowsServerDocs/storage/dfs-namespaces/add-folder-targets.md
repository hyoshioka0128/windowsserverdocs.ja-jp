---
title: Add Folder Targets
description: このトピックでは、フォルダー ターゲット (UNC パス) を追加する方法について説明します。
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: d2f3845a612556a51692aaf51d256bbedd518e7a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854105"
---
# <a name="add-folder-targets"></a>Add folder targets

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

フォルダー ターゲットとは、ある名前空間内のフォルダーと関連付けられた別の名前空間または共有フォルダーへの汎用名前付け規則 (UNC) パスです。 複数のフォルダー ターゲットを追加すると、名前空間内のフォルダーの可用性が向上します。

## <a name="to-add-a-folder-target"></a>フォルダー ターゲットを追加するには

DFS の管理を使ってフォルダー ターゲットを追加するには、次の手順を使用します。

1.  **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、フォルダーを右クリックし、 **[フォルダー ターゲットを追加]** をクリックします。

3.  フォルダー ターゲットのパスを入力するか、 **[参照]** をクリックしてフォルダー ターゲットを見つけます。

4.  フォルダーが DFS レプリケーションを使ってレプリケートされる場合、レプリケーション グループに新しいフォルダー ターゲットを追加するかどうかを指定できます。

> [!TIP]
> Windows PowerShell を使ってフォルダー ターゲットを追加するには、[New-DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget) コマンドレットを使います。 DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。

> [!NOTE]
> フォルダーにはフォルダー ターゲットまたは他の DFS フォルダーを含めることができます。ただし、フォルダーの同じ階層に、それら両方を含めることはできません。

## <a name="see-also"></a>参照

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS レプリケーションを使用してフォルダーターゲットをレプリケートする](replicate-folder-targets-using-dfs-replication.md)