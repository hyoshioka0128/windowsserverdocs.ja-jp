---
title: モードの切り替え
description: MultiPoint Services でステーションとコンソールモードを切り替える方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 181324bff3227f7b071b8ae32f756d365b059a74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389240"
---
# <a name="switch-between-modes"></a>モードの切り替え
MultiPoint マネージャーには、さまざまな種類の MultiPoint サービス システムの管理を実行するのには、次のモードが含まれています。  
  
-   *ステーションモード*:既定では、MultiPoint Services システムはステーションモードで起動します。 ステーション モードの場合、MultiPoint サービス ステーションは、各ステーションが Windows を実行する個別のコンピューターを実行しているように動作します。また、複数のユーザーが同時に同じシステムを使用できます。 管理者とユーザーはファイルを共有し、必要な作業を実行できます。  
  
-   *コンソールモード*:MultiPoint Services システムがコンソールモードの場合は、ソフトウェアとドライバーをインストールおよび更新したり、その他のメンテナンスタスクを実行したりできます。 システムがコンソール モードの場合、他のコンピューター ユーザーから使用できる*ステーション*はありません。 MultiPoint マネージャーでは、このようなステーションは表示されません。 サーバーに直接接続されているすべてのモニターは、このコンピューターのシステムの表示として扱われます。   
  
> [!NOTE]
> サーバーの設定で既定値を変更して、コンソール モードでシステムを起動することを強制できます。  
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>ステーション モードからコンソール モードに切り替えるには  
  
1.  ステーション モードで MultiPoint マネージャーを開き、クリックして、 **ホーム**  タブをクリックします。  
  
2.  **[コンピューター]** 列で、モードを変更するコンピューターをクリックします。  
  
3.  [*コンピューター名*の**タスク**] で、[**コンソールモードに切り替え] を**クリックします。 コンピューターが再起動し、すべてのステーションを使用できなくなります。  
  
## <a name="to-switch-from-console-mode-to-station-mode"></a>コンソール モードからステーション モードに切り替えるには  
  
1.  コンソール モードで MultiPoint マネージャーを開き、クリックして、 **ホーム**  タブをクリックします。  
  
2.  **[コンピューター]** 列で、モードを変更するコンピューターをクリックします。  
  
3.  [*コンピューター名*の**タスク**] の [**ステーションモードに切り替え] を**クリックします。 コンピューターが再起動し、すべてのステーションが使用できるようになります。  
  
## <a name="see-also"></a>関連項目  
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)