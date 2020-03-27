---
title: DNS ゾーンを作成する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a9762d15d0b95954623bbefdec38696885676975
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312634"
---
# <a name="create-a-dns-zone"></a>DNS ゾーンを作成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS ゾーンを作成できます。  
  
この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-create-a-dns-zone"></a>DNS ゾーンを作成するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウの **[監視と管理]** で、 **[DNS および DHCP サーバー]** をクリックします。 表示ウィンドウで、 **[サーバーの種類]** をクリックし、 **[DNS]** をクリックします。 IPAM によって管理されているすべての DNS サーバーが検索結果に一覧表示されます。  
  
3.  ゾーンを追加するサーバーを見つけて、サーバーを右クリックします。  **[DNS ゾーンの作成]** をクリックします。  
  
    ![DNS ゾーンの作成](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  **[DNS ゾーンの作成]** ダイアログボックスが表示されます。 **[全般プロパティ**] で、ゾーンカテゴリとゾーンの種類を選択し、 **[ゾーン名]** に名前を入力します。 また、 **[詳細プロパティ]** で、展開に適した値を選択し、 **[OK]** をクリックします。  
  
    ![詳細プロパティ](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>参照  
[DNS ゾーンの管理](DNS-Zone-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


