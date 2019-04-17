---
title: 複数の Active Directory フォレスト内のリソースを管理します。
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b01680d4b35461ff85965781ebc60e7a613d1cb8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>複数の Active Directory フォレスト内のリソースを管理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、IPAM を使用して、ドメイン コントローラー、DHCP サーバー、および複数の Active Directory フォレスト内の DNS サーバーを管理するのに方法について説明します。  
  
IPAM を使用してをリモート Active Directory フォレスト内のリソースを管理するには、2 つの IPAM がインストールされているフォレストと信頼できる方法を管理する各フォレスト必要があります。  
  
別の Active Directory フォレストの探索プロセスを開始するには、サーバー マネージャーを開き [IPAM] をクリックします。 IPAM クライアント コンソールで、をクリックして**サーバー検出の構成**、] をクリックし、**フォレストを取得する**します。 これは、信頼されるフォレストおよびドメインを検出するバック グラウンド タスクを開始します。 検出プロセスが完了したら、クリックして**サーバー検出の構成**、次のダイアログ ボックスが開きます。  
  
![サーバー検出を構成します。](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>グループ ポリシー ベースの Active Directory のフォレスト間のシナリオのプロビジョニング、および信頼する側のドメイン Dc ではなく、IPAM サーバーでは、次の Windows PowerShell コマンドレットを実行することを確認します。 例として、IPAM サーバーが corp.contoso.com のフォレストに参加していて、信頼する側のフォレストは fabrikam.com は corp.contoso.com fabrikam.com フォレストでグループ ポリシー ベースのプロビジョニング用に IPAM サーバーが、次の Windows PowerShell コマンドレットを実行することができます。 このコマンドレットを実行するには、fabrikam.com フォレスト内の Domain Admins グループのメンバーがあります。

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

**サーバー検出の構成**ダイアログ ボックスで、をクリックして**フォレストを選択**、し、IPAM で管理するフォレストを選択します。 管理、およびをクリックするドメインを選択しても**追加**します。

**を検出するサーバーの役割の選択**、管理するドメインごとに検出するサーバーの種類を指定します。 オプションは、**ドメイン コントローラー**、**DHCP サーバー**、および**DNS サーバー**します。

既定では、ドメイン コントローラー、DHCP サーバー、および DNS サーバーが検出された - 場合、これらの種類のサーバーのいずれかを検出しないようにそのオプションのチェック ボックスをオフにします。

上記の例の図で contoso.com フォレストで、IPAM サーバーがインストールされているし、IPAM の管理の fabrikam.com フォレストのルート ドメインを追加します。 選択したサーバーの役割には、IPAM を検出し、ドメイン コントローラー、DHCP サーバー、および fabrikam.com ルート ドメインと contoso.com ルート ドメイン内の DNS サーバーの管理ができるようにします。

フォレスト、ドメイン、およびサーバーの役割を指定したら、クリックして**OK**します。 IPAM は、探索を実行し、検出が完了したら、ローカルおよびリモートの両方のフォレスト内のリソースを管理することができます。
