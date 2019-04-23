---
title: MultiPoint Services - 移行後のタスク
description: 検証し、MultiPoint Services への移行を終了する方法について説明します
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: e3fa3c812355a14289ea4eeff3ab1e7e92e00d97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863503"
---
# <a name="multipoint-services---post-migration-tasks"></a>MultiPoint Services - 移行後のタスク

>適用先:Windows Server 2016

Windows Server 2016 で MultiPoint Services に移行した後、移行を検証し、クリーンアップ手順を実行するには、次の情報を使用します。

## <a name="validate-the-migration-by-running-a-pilot-program"></a>パイロット プログラムを実行して移行を検証します。

MultiPoint Services の移行を検証するには、運用環境にパイロット プロジェクトを作成します。 デプロイが予想どおりに動作することを確認するには、実稼働環境に移行した役割サービスを配置する前に、サーバー上でパイロット プロジェクトを実行します。 最初はゆっくりと MultiPoint Services にアクセスするユーザーの数を増やすこと、接続の数を制限することを検討してください。

> [!NOTE] 
> 常にテスト アカウントを使用して、移行をテストします。 有効なユーザーには、管理者特権のアカウントとアカウントを使用します。

## <a name="retire-the-source-server"></a>移行元サーバーの使用を停止する
移行を検証した後は、シャット ダウンまたは移行元サーバーをネットワークから切断します。 サーバーがドメインに参加している場合は、切断する前に、ドメインから削除します。

