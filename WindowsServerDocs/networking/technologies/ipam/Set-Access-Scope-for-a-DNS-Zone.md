---
title: DNS ゾーンのアクセス スコープを設定する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca1899a4d49639b047b672c42b9743fb27df8a67
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860605"
---
# <a name="set-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセス スコープを設定する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS ゾーンのアクセススコープを設定できます。  
  
この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセススコープを設定するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウで、 **[DNS ゾーン数]** をクリックします。 表示ウィンドウで、アクセススコープを変更する DNS ゾーンを右クリックし、 **[アクセススコープの設定]** をクリックします。  
  
    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  **[アクセススコープの設定]** ダイアログボックスが表示されます。 デプロイに必要な場合は、 **[親からのアクセススコープの継承]** をクリックして選択を解除します。 **[アクセススコープの選択]** で項目を選択し、 **[OK]** をクリックします。  
  
    ![アクセススコープの選択](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  IPAM クライアントコンソールの表示ウィンドウで、ゾーンのアクセススコープが変更されていることを確認します。  
  
    ![ゾーンのアクセススコープが変更されていることを確認します。](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>参照  
[ロールベースの Access Control](Role-based-Access-Control.md)  
[IPAM の管理](Manage-IPAM.md)  
  


