---
title: MultiPoint Services で、RDP over LAN 接続ステーションのセットアップします。
description: MultiPoint Services で、RDP over LAN システムを設定する方法について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 8d2f1644918f1a581c1bcab181cd084e12c6b576
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843703"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>MultiPoint Services で、RDP over LAN 接続ステーションのセットアップします。
RDP over LAN 接続ステーションとは、シン クライアント、従来のデスクトップまたはリモート デスクトップ プロトコル (RDP) を使用して、ローカル エリア ネットワーク (LAN) 上の MultiPoint Services に接続するラップトップ コンピューターです。 これと他のステーションの種類に関する詳細については、次を参照してください。 [MultiPoint ステーション](MultiPoint-services-Stations.md)します。  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>LAN では、コンピューターまたはシン クライアントを使用して MultiPoint ステーションを設定するには  
  
1.  MultiPoint Services を実行しているコンピューターを起動します。  
  
2.  MultiPoint Server コンピューターが、スイッチ、ルーター、またはその他のネットワーク デバイスが LAN に接続されているし、適切な IP アドレスを持っていることを確認してください。 (169.254.*.* (APIPA アドレス) で始まる IP アドレスは LAN 接続に問題があるか、DHCP サーバーに到達できないまたは正しく機能していないことを示す可能性があります)  
  
3.  シン クライアント、クライアント コンピューターを LAN に接続します。  
  
4.  クライアント コンピューターまたはシン クライアントで有効にします。  
  
5.  クライアント コンピューターまたはシン クライアント、リモート デスクトップ接続または同等のアプリケーションを起動し、名前または MultiPoint Services を実行しているコンピューターの IP アドレスを入力します。

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>コネクタ サービスを使用してリモート管理のための Windows 10 デバイスを設定します。
PC または Windows 10 を実行しているラップトップをリモートで管理することができる限り。
- コネクタ サービスを有効になっています。  
- MultiPoint サーバー上の管理対象のコンピューターに、マシンが追加されました。  

Windows 10 を実行している PC で MultiPoint コネクタを有効にするこれらの手順に従います。

1. 検索ボックスには、「有効にする Windows 機能を切り替えます」を入力し、適切な検索結果を選択します。 

2. 機能の一覧でを有効にする**MultiPoint コネクタ**します。 これは、デバイスの管理に必要な MultiPoint コネクタ サービスを有効になります。 

MultiPoint server:
1. MultiPoint マネージャーを開き、いずれかを選択します。**パーソナル コンピューターを追加または削除する**または**追加または削除する MultiPoint Services**します。

2. 管理し、をクリックするリモート コンピューターを選択して**OK**します。  リモート コンピューターの管理者の資格情報を求めるメッセージが表示されます。  これが完了すると、MultiPoint マネージャー ホーム タブでは、リモート コンピューターが表示されます。

ときに正常に設定ダッシュ ボード マネージャーを監視できます管理されたデバイスで作業しているユーザー。

> [!IMPORTANT]  
> 監視を管理するときは、設定が適切に変更されているサーバーを除く Windows 10 デバイス administratrive ユーザーを監視できません。 参照してください[サーバー設定の編集](Edit-Server-Settings.md)