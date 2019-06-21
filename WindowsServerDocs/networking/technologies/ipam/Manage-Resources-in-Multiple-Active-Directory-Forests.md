---
title: 複数の Active Directory フォレスト内のリソースを管理する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2bbd303df635af314cee2126a75f0569ede2f5de
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282189"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>複数の Active Directory フォレスト内のリソースを管理する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、IPAM を使用して、ドメイン コント ローラー、DHCP サーバー、および複数の Active Directory フォレスト内の DNS サーバーを管理するのに方法について説明します。  
  
IPAM を使用して、リモート Active Directory フォレスト内のリソースを管理するには、双方向の IPAM がインストールされているフォレストと信頼の各フォレストを管理する必要があります。  
  
別の Active Directory フォレストの探索プロセスを開始するには、サーバー マネージャーを開き [IPAM] をクリックします。 IPAM クライアント コンソールで、次のようにクリックします。**サーバー検出の構成**、順にクリックします**フォレストを取得**します。 これには、信頼されたフォレストとドメインを検出するバック グラウンド タスクが開始します。 検出プロセスが完了したら**サーバー検出の構成**、次のダイアログ ボックスを開きます。  
  
![サーバー検出の設定](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>グループ ポリシーの\-ベースの Active Directory のフォレスト間シナリオでは、プロビジョニング、および信頼する側のドメイン Dc ではなく、IPAM サーバーでは、次の Windows PowerShell コマンドレットを実行することを確認します。 たとえば、IPAM サーバーがフォレスト corp.contoso.com に参加していて、信頼する側のフォレストとは、fabrikam.com、行うことができます、次の Windows PowerShell コマンドレット corp.contoso.com で IPAM サーバーでグループ ポリシーの\-ベースのプロビジョニングにはfabrikam.com フォレスト。 このコマンドレットを実行するには、fabrikam.com のフォレスト内の Domain Admins グループのメンバーがあります。

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

**サーバー検出の構成**ダイアログ ボックスで、をクリックして**フォレストを選択**IPAM で管理するフォレストを選択します。 クリックして、管理するドメインを選択しても**追加**します。

**を検出するサーバーの役割の選択**、管理するドメインごとに検出するサーバーの種類を指定します。 オプションを**ドメイン コント ローラー**、 **DHCP サーバー**、および**DNS server**します。

既定では、ドメイン コント ローラー、DHCP サーバー、および DNS サーバーが検出された - 場合、これらの種類のサーバーのいずれかを検出しないようにそのオプションのチェック ボックスをオフにします。

上記の例の図に、IPAM サーバーが、contoso.com フォレストにインストールされているし、IPAM の管理、fabrikam.com のフォレストのルート ドメインが追加されます。 選択したサーバーの役割には、IPAM を検出し、ドメイン コント ローラー、DHCP サーバー、および contoso.com のルート ドメインと fabrikam.com のルート ドメインの DNS サーバーを管理ができるようにします。

フォレスト、ドメイン、およびサーバーの役割を指定した後にをクリックして**OK**します。 IPAM は、検出を実行し、検出が完了したら、ローカルおよびリモートの両方のフォレスト内のリソースを管理することができます。
