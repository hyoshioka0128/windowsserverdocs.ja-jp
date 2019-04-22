---
title: MultiPoint Services への移行を準備する
description: Windows Server 2016 で MultiPoint Services に移行する前に収集する情報について説明します
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3060c531-98a2-4957-a02c-be273f25f493
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 9650ebcae7e6207a226617d401d892049405901f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824383"
---
# <a name="prepare-to-migrate-to-multipoint-services-in-windows-server-2016"></a>Windows Server 2016 で MultiPoint Services に移行するための準備します。

>適用先:Windows Server 2016

MultiPoint サービスの役割サービスを Windows Server 2016 RTM を実行している移行先サーバーに Windows Server 2016 の以前のリリースを実行している移行元サーバーから移行するのに必要がある情報を収集するのにには、次の情報を使用します。

少なくともには、インストール、削除、または MultiPoint Services をセットアップするには、移行元サーバーと移行先サーバーの Administrators グループのメンバーがあります。

>[!NOTE]
> 次の手順では、データを移行するユーザー フォルダーに保存または共有フォルダーのガイダンスは提供されません。 ユーザーは、移行を開始する前にデータをバックアップすることを確認します。

MultiPoint マネージャーを使用して、移行に必要な情報を取得します。 MultiPoint マネージャーを使用して、サーバー管理者のアクセス許可を必要があります。

MultiPoint サーバー、ユーザー、および環境の設定を記録、[移行データ収集ワークシート](multipoint-services-migration-worksheet.md)します。 次の手順を使用して、その情報を収集します。

## <a name="multipoint-server-settings-for-the-local-server"></a>ローカル サーバーの multiPoint Server の設定
1. MultiPoint マネージャーを起動します。
2. **ホーム**タブに、ローカル サーバーを選択してクリックして**サーバー設定を編集します。**
3. データのワークシートで、設定を記録します。
4. [設定] ウィンドウを閉じます。

## <a name="managed-servers-and-computers"></a>管理対象サーバーとコンピューター

管理対象サーバーとコンピューターの名前を確認するには、上、**ホーム**MultiPoint マネージャー タブ。

## <a name="station-settings"></a>ステーションの設定
ステーションで自動ログオンやディスプレイの向きが構成された場合は、次の手順を使用して情報を取得します。 それ以外の場合、この手順をスキップすることができます。

ステーションの設定を取得するには。

1. 移動して、**ステーション**MultiPoint マネージャー タブ。
2. "Yes"を持つステーション内の検索、**自動ログオン**列。
3. そのステーションを選択し、クリックして**ステーションを構成する**します。
4. 自動ログオンに使用するユーザーを記録します。

画面の向きの設定を取得するには、表示、**ステーション設定は**ステーションごと。

## <a name="list-of-users"></a>ユーザーの一覧
1. をクリックして、**ユーザー** MultiPoint マネージャー タブ。
2. レコード、**管理者**と**MultiPoint ダッシュ ボード ユーザー** accoutns します。
3. 標準のユーザーを記録します。

## <a name="vdi-template-location"></a>VDI のテンプレートの場所
 以前、VDI のテンプレート機能を有効にした場合は、VDI のテンプレートの場所を記録します。 同じネットワーク上の元と移行先サーバー、限り MultiPoint マネージャーを使用してテンプレートをインポートすることができます。
 
## <a name="next-step"></a>次の手順
準備ができました[MultiPoint Services への移行](multipoint-services-migration-steps.md)Windows Server 2016 の RTM リリースでします。