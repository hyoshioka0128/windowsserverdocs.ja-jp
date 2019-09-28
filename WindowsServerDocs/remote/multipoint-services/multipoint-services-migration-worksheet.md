---
title: MultiPoint Services の移行計画ワークシート
description: Windows Server 2016 の MultiPoint Services への移行に役立つ計画ワークシートを提供します。
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 864405bb-47ed-4c83-97a2-8df4c6e6f96b
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: d3d2ecca4062d28d210196d9191e08710eb731c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394629"
---
# <a name="planning-worksheet-for-multipoint-services-migration"></a>MultiPoint Services の移行計画ワークシート

>適用先:Windows Server 2016

MultiPoint Services の移行時に必要な設定を収集するには、次の一覧と表を使用します。

## <a name="source-server-settings"></a>移行元サーバーの設定

サーバーの設定は、MultiPoint マネージャーの **[ホーム]** タブで確認できます。 移行元サーバーで使用されている各設定の横にチェックマークを配置します。

- 1つのアカウントに複数のセッションを許可します。
- このコンピューターをリモートで管理できるようにします。
- このコンピューターのデスクトップの監視を許可します。
- 常にコンソールモードで起動します。
- 最初のユーザーログオン時にプライバシーに関する通知を表示しない
- 各ステーションに一意の IP を割り当てます。
- このコンピューターの MultiPoint ダッシュボードとユーザーセッションの間で IM を許可します。
- 管理者と MultiPoint ダッシュボードのユーザーセッションのオーケストレーションを許可します。
- ステーションが GPU ハードウェアレンダリングを使用できるようにします。

## <a name="managed-servers-and-computers"></a>管理されたサーバーとコンピューター

管理されているサーバーとコンピューターの名前を記録します。 この情報は、MultiPoint マネージャーの **[ホーム]** タブで確認できます。

| [Computer] | コンピューター名 |
|----------|---------------|
| 1        |               |
| 2        |               |
| 3        |               |
| 4        |               |
| 5        |               |
| 6        |               |
| 7        |               |
| 8        |               |
| 9        |               |
| 10       |               |


## <a name="stations"></a>番組

ローカルステーションとその設定を記録します。 この情報は、MultiPoint マネージャーの **[ステーション]** タブで確認できます。

| #  | ステーション名 | 自動ログオンユーザーアカウント | 表示の向き |
|----|--------------|-------------------------|---------------------|
| 1  |              |                         |                     |
| 2  |              |                         |                     |
| 3  |              |                         |                     |
| 4  |              |                         |                     |
| 5  |              |                         |                     |
| 6  |              |                         |                     |
| 7  |              |                         |                     |
| 8  |              |                         |                     |
| 9  |              |                         |                     |
| 10 |              |                         |                     |

## <a name="administrators-and-multipoint-dashboard-users"></a>管理者と MultiPoint ダッシュボードユーザー

Administrators および MultiPoint ダッシュボードユーザーのユーザー名をコピーします。 この情報は、MultiPoint マネージャーの **[ユーザー]** タブで確認できます。

Administrators:

- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:

ダッシュボードユーザー:

- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:

## <a name="vdi-template-and-virtual-desktops"></a>VDI テンプレートと仮想デスクトップ

MultiPoint サービスのデプロイで、VDI テンプレート情報と仮想デスクトップの名前を記録します。 この情報は、MultiPoint マネージャーの **[仮想デスクトップ]** タブで確認できます。

**VDI テンプレートの場所**: 

| # | 仮想デスクトップ名      |
|---|---------------------------|
| 1 |                           |
| 2 |                           |
| 3 |                           |
| 4 |                           |
| 5 |                           |