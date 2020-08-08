---
title: MultiPoint Services-移行後のタスク
description: MultiPoint Services への移行を検証して終了する方法について説明します。
ms.date: 07/29/2016
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: ed3937cd6830de642c21616071e86eca3ad6cd5b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969249"
---
# <a name="multipoint-services---post-migration-tasks"></a>MultiPoint Services-移行後のタスク

>適用先:Windows Server 2016

Windows Server 2016 で MultiPoint Services に移行した後、次の情報を使用して移行を検証し、クリーンアップ手順を実行します。

## <a name="validate-the-migration-by-running-a-pilot-program"></a>パイロットプログラムを実行して移行を検証する

運用環境でパイロットプロジェクトを作成することによって、MultiPoint サービスの移行を検証できます。 移行された役割サービスを運用環境に配置する前に、サーバーで試験プロジェクトを実行して、展開が期待どおりに動作することを確認します。 最初に接続数を制限し、MultiPoint Services にアクセスするユーザーの数を徐々に増やしてください。

> [!NOTE]
> 移行をテストするには、常にテストアカウントを使用します。 管理者特権を持つアカウントと、有効なユーザーのアカウントを使用します。

## <a name="retire-the-source-server"></a>移行元サーバーの使用を停止する
移行を検証した後、移行元サーバーをネットワークからシャットダウンまたは切断することができます。 サーバーがドメインに参加している場合は、接続を切断する前にドメインから削除します。

