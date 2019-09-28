---
title: MultiPoint Services への移行を準備する
description: Windows Server 2016 の MultiPoint Services に移行する前に収集する情報について説明します。
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3060c531-98a2-4957-a02c-be273f25f493
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: d0f1fd22b00bdb2e5e3684a541dd14532fd885e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394646"
---
# <a name="prepare-to-migrate-to-multipoint-services-in-windows-server-2016"></a>Windows Server 2016 の MultiPoint Services への移行の準備

>適用先:Windows Server 2016

以前のリリースの Windows Server 2016 を実行している移行元サーバーから Windows Server 2016 RTM を実行している移行先サーバーに MultiPoint Services の役割サービスを移行するために必要な情報を収集するには、次の情報を使用します。

少なくとも、MultiPoint Services をインストール、削除、または設定するには、移行元サーバーと移行先サーバーの Administrators グループのメンバーである必要があります。

>[!NOTE]
> ここでは、ユーザーフォルダーまたは共有フォルダーに保存されたデータを移行する方法については説明しません。 移行を開始する前に、ユーザーがデータをバックアップしていることを確認します。

MultiPoint マネージャーを使用して、移行に必要な情報を取得します。 MultiPoint マネージャーを使用するには、サーバー管理者のアクセス許可が必要です。

MultiPoint サーバー、ユーザー、および環境の設定を、[移行データ収集ワークシート](multipoint-services-migration-worksheet.md)に記録します。 その情報を収集するには、次の手順に従います。

## <a name="multipoint-server-settings-for-the-local-server"></a>ローカルサーバーの MultiPoint Server 設定
1. MultiPoint マネージャーを起動します。
2. **[ホーム]** タブで、ローカルサーバーを選択し、 **[サーバー設定の編集]** をクリックします。
3. データワークシートに設定を記録します。
4. [設定] ウィンドウを閉じます。

## <a name="managed-servers-and-computers"></a>管理されたサーバーとコンピューター

管理されているサーバーとコンピューターの名前は、MultiPoint マネージャーの **[ホーム]** タブで確認できます。

## <a name="station-settings"></a>ステーションの設定
自動ログオンまたは表示の向きがステーション用に構成されている場合は、次の手順に従って、その情報を取得します。 それ以外の場合は、この手順を省略できます。

ステーションの設定を取得するには:

1. MultiPoint マネージャーの **[ステーション]** タブにアクセスします。
2. **自動ログオン**列に "yes" があるステーションを検索します。
3. そのステーションを選択し、 **[ステーションの構成]** をクリックします。
4. 自動ログオンに使用するユーザーを記録します。

画面の向きの設定を取得するには、各ステーションの**ステーション設定**を表示します。

## <a name="list-of-users"></a>ユーザーの一覧
1. MultiPoint マネージャーの **[ユーザー]** タブをクリックします。
2. **管理者**と**MultiPoint ダッシュボードユーザーのログオン**を記録します。
3. 標準ユーザーを記録します。

## <a name="vdi-template-location"></a>VDI テンプレートの場所
 以前に VDI テンプレート機能を有効にした場合は、VDI テンプレートの場所を記録してください。 移行元サーバーと移行先サーバーが同じネットワーク上にある限り、MultiPoint マネージャーを使用してテンプレートをインポートできます。
 
## <a name="next-step"></a>次の手順
これで、Windows Server 2016 の RTM リリースで[MultiPoint Services に移行](multipoint-services-migration-steps.md)する準備が整いました。