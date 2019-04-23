---
title: MultiPoint Services の移行の計画ワークシート
description: Windows Server 2016 で MultiPoint Services に移行するための計画ワークシートを提供します。
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 864405bb-47ed-4c83-97a2-8df4c6e6f96b
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: a9d9b62bced9be90c658b79338c6f4ef07710fc3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880583"
---
# <a name="planning-worksheet-for-multipoint-services-migration"></a>MultiPoint Services の移行の計画ワークシート

>適用先:Windows Server 2016

MultiPoint Services の移行中に必要な設定を収集するのにには、次のリストとテーブルを使用します。

## <a name="source-server-settings"></a>移行元サーバー設定

サーバーの設定を見つけることができます、**ホーム**MultiPoint マネージャー タブ。 ソース サーバーで使用するには、各設定の横にあるチェック マークを配置します。

- 複数のセッションが 1 つのアカウントを許可します。
- このコンピューターをリモートで管理を許可します。
- このコンピューターのデスクトップの監視を許可します。
- 常にコンソール モードで起動します。
- 最初のユーザーのログオン時にプライバシーに関する通知を表示しません。
- 各ステーションに一意の IP を割り当てます。
- このコンピューターでは、MultiPoint ダッシュ ボードとユーザー セッションの間の IM を許可します。
- 管理者と MultiPoint ダッシュ ボードのユーザー セッションのオーケストレーションを許可します。
- GPU ハードウェア レンダリングを使用するステーションを使用できます。

## <a name="managed-servers-and-computers"></a>管理対象サーバーとコンピューター

管理対象サーバーとコンピューターの名前を記録します。 この情報を見つけることができます、**ホーム**MultiPoint マネージャー タブ。

| コンピューター | コンピューター名 |
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


## <a name="stations"></a>ステーション

ローカルのステーションとその設定を記録します。 この情報を見つけることができます、**ステーション**MultiPoint マネージャー タブ。

| #  | ステーション名 | 自動ログオンのユーザー アカウント | 表示の向き |
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

## <a name="administrators-and-multipoint-dashboard-users"></a>管理者と MultiPoint ダッシュ ボード ユーザー

管理者と MultiPoint ダッシュ ボードのユーザーのユーザー名をコピーします。 この情報を見つけることができます、**ユーザー** MultiPoint マネージャー タブ。

Administrators:

- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:

ダッシュ ボード ユーザー:

- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:
- ユーザー名:

## <a name="vdi-template-and-virtual-desktops"></a>VDI のテンプレートと仮想デスクトップ

MultiPoint Services の展開では、VDI のテンプレート情報と仮想デスクトップの名前を記録します。 この情報を見つけることができます、**仮想デスクトップ**MultiPoint マネージャー タブ。

**テンプレートの場所を VDI**: 

| # | 仮想デスクトップの名前      |
|---|---------------------------|
| 1 |                           |
| 2 |                           |
| 3 |                           |
| 4 |                           |
| 5 |                           |