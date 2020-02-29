---
title: WSUS レプリカ モードを実行する
description: 'Windows Server Update Service (WSUS) のトピック-レプリカモードの構成方法 '
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d218cd6b-3b6b-4429-913b-31d412ce3356
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7da68fa9cbe71f8a67e74671d64d11908ae4654
ms.sourcegitcommit: 9687d3eb221b89061a48bf1e73fb3b25bee69f9a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78169562"
---
# <a name="running-wsus-replica-mode"></a>WSUS レプリカ モードを実行する

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

レプリカ モードで実行されている WSUS サーバーは、更新プログラムの承認と管理サーバーで作成したコンピューター グループを継承します。 レプリカ モードを使用するシナリオで、通常、1 つの管理サーバーで、サイトや組織の構造に基づいて、組織全体で 1 つ以上の従属レプリカ WSUS サーバーに分散します。 更新プログラムを承認し、レプリカ モードのサーバーをミラー化し、管理サーバー上のコンピューター グループを作成します。 レプリカ モードのサーバーは WSUS セットアップ中にのみ設定できますまたこのシナリオを実装する場合は重要な更新プログラム承認を組織では、コンピューター グループが一元的に管理します。

WSUS サーバーがレプリカ モードで実行されている場合は、では、主にサーバーを限定的な管理機能のみを実行することができます。

-   追加して、コンピューター グループからコンピューターを削除します。 コンピューター グループのメンバーシップがレプリカ サーバーに分散されなくなり、コンピューターのみグループ自体です。 そのため、レプリカ モードのサーバーでは、管理サーバーで作成したコンピューター グループを継承します。 ただし、コンピューター グループが空になります。 クライアントは、コンピューター グループにレプリカ サーバーに接続するコンピューターし、割り当てる必要があります。

-   同期スケジュールの設定

-   プロキシ サーバー設定を指定します。

-   更新プログラムのソースを指定します。 これは、管理サーバー以外のサーバーを指定できます。

-   利用可能な更新プログラムの表示

-   更新プログラム、同期、コンピューターの状態、および、サーバー上の WSUS 設定の監視

-   レプリカ モード サーバーで利用可能なすべての標準 WSUS を実行するレポートします。



