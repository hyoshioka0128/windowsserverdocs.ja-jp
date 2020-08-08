---
title: モード間の切り替え
description: MultiPoint Services でステーションとコンソールモードを切り替える方法について説明します。
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: efd6a8fd62fa32bc892fcab43935b2a1d8a8f676
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969289"
---
# <a name="switch-between-modes"></a>モード間の切り替え
MultiPoint マネージャーには、さまざまな種類の MultiPoint サービス システムの管理を実行するのには、次のモードが含まれています。

-   *ステーション モード*: 既定では、MultiPoint サービスはステーション モードで開始されます。 ステーション モードの場合、MultiPoint サービス ステーションは、各ステーションが Windows を実行する個別のコンピューターを実行しているように動作します。また、複数のユーザーが同時に同じシステムを使用できます。 管理者とユーザーはファイルを共有し、必要な作業を実行できます。

-   *コンソール モード*: MultiPoint サービス システムがコンソール モードの場合、ソフトウェアまたはドライバーをインストールおよび更新するか、他のメンテナンス タスクを実行できます。 システムがコンソール モードの場合、他のコンピューター ユーザーから使用できる*ステーション*はありません。 MultiPoint マネージャーでは、このようなステーションは表示されません。 サーバーに直接接続されているすべてのモニターは、このコンピューターのシステムの表示として扱われます。

> [!NOTE]
> サーバーの設定で既定値を変更して、コンソール モードでシステムを起動することを強制できます。
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>ステーション モードからコンソール モードに切り替えるには

1.  ステーション モードで MultiPoint マネージャーを開き、クリックして、 **ホーム** ] タブをクリックします。

2.  **[コンピューター]** 列で、モードを変更するコンピューターをクリックします。

3.  [*コンピューター名* **のタスク]** の **[コンソール モードに切り替える]** をクリックします。 コンピューターが再起動し、すべてのステーションを使用できなくなります。

## <a name="to-switch-from-console-mode-to-station-mode"></a>コンソール モードからステーション モードに切り替えるには

1.  コンソール モードで MultiPoint マネージャーを開き、クリックして、 **ホーム** ] タブをクリックします。

2.  **[コンピューター]** 列で、モードを変更するコンピューターをクリックします。

3.  [*コンピューター名* **のタスク]** の **[ステーション モードに切り替える]** をクリックします。 コンピューターが再起動し、すべてのステーションが使用できるようになります。

## <a name="see-also"></a>参照
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)