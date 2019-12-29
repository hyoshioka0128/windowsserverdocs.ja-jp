---
title: 複数の Active Directory フォレスト内のリソースを管理する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5fad1062b65b4784a8a5ddfde927951230cb6ab8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355233"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>複数の Active Directory フォレスト内のリソースを管理する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、複数の Active Directory フォレスト内のドメインコントローラー、DHCP サーバー、および DNS サーバーを IPAM を使用して管理する方法について説明します。  
  
IPAM を使用してリモート Active Directory フォレスト内のリソースを管理するには、管理する各フォレストに、IPAM がインストールされているフォレストと双方向の信頼関係がある必要があります。  
  
異なる Active Directory フォレストの検出プロセスを開始するには、サーバーマネージャーを開き、[IPAM] をクリックします。 IPAM クライアントコンソールで、 **[サーバー検出の構成]** をクリックし、 **[フォレストの取得]** をクリックします。 これにより、信頼されたフォレストとそのドメインを検出するバックグラウンドタスクが開始されます。 検出プロセスが完了したら、 **[サーバー検出の構成]** をクリックすると、次のダイアログボックスが開きます。  
  
![サーバー検出の設定](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>フォレスト間の Active Directory シナリオでグループポリシー\-ベースのプロビジョニングを行う場合は、信頼する側のドメイン Dc ではなく、IPAM サーバーで次の Windows PowerShell コマンドレットを実行してください。 たとえば、IPAM サーバーがフォレスト corp.contoso.com に参加していて、信頼する側のフォレストが fabrikam.com である場合、corp.contoso.com の IPAM サーバーで次の Windows PowerShell コマンドレットを実行して、fabrikam.com フォレストでグループポリシー\-ベースのプロビジョニングを行うことができます。 このコマンドレットを実行するには、fabrikam.com フォレストの Domain Admins グループのメンバーである必要があります。

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

**[サーバー検出の構成]** ダイアログボックスで、 **[フォレストを選択]** する をクリックし、IPAM で管理するフォレストを選択します。 また、管理するドメインを選択し、 **[追加]** をクリックします。

**[検出するサーバーの役割を選択**してください] で、管理するドメインごとに、検出するサーバーの種類を指定します。 **[ドメインコントローラー]** 、 **[DHCP サーバー]** 、 **[DNS サーバー]** のオプションがあります。

既定では、ドメインコントローラー、DHCP サーバー、および DNS サーバーが検出されるので、これらの種類のサーバーのいずれかを検出しない場合は、そのオプションのチェックボックスをオフにしてください。

上の図の例では、IPAM サーバーが contoso.com フォレストにインストールされ、fabrikam.com フォレストのルートドメインが IPAM 管理用に追加されています。 選択したサーバーの役割により、IPAM は fabrikam.com ルートドメインと contoso.com ルートドメイン内のドメインコントローラー、DHCP サーバー、および DNS サーバーを検出して管理できます。

フォレスト、ドメイン、およびサーバーの役割を指定したら、[ **OK]** をクリックします。 IPAM によって検出が実行され、探索が完了すると、ローカルとリモートの両方のフォレストのリソースを管理できます。
