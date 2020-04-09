---
title: MultiPoint Services での RDP over LAN 接続ステーションのセットアップ
description: MultiPoint Services で RDP over LAN システムを設定する方法について説明します。
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 36aaa4c1571ff6dd48ae645b9c7b5746be7c1857
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853905"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>MultiPoint Services での RDP over LAN 接続ステーションのセットアップ
RDP over LAN 接続ステーションは、シンクライアント、従来のデスクトップ、またはラップトップコンピューターで、リモートデスクトッププロトコル (RDP) を使用してローカルエリアネットワーク (LAN) 上の MultiPoint Services に接続します。 これと他のステーションの種類に関する詳細については、次を参照してください。 [MultiPoint ステーション](MultiPoint-services-Stations.md)します。  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>LAN 上のコンピューターまたはシンクライアントを使用して MultiPoint ステーションを設定するには  
  
1.  MultiPoint Services を実行しているコンピューターの電源を入れます。  
  
2.  MultiPoint Server コンピューターがスイッチ、ルーター、またはその他のネットワークデバイスによって LAN に接続されており、適切な IP アドレスを持っていることを確認します。 (IP アドレスが 169.254 (APIPA アドレス) で始まる場合は、LAN 接続に問題があるか、DHCP サーバーに到達できないか、正しく機能していないことを示している可能性があります。)  
  
3.  クライアントコンピューターまたはシンクライアントを LAN に接続します。  
  
4.  クライアントコンピューターまたはシンクライアントをオンにします。  
  
5.  クライアントコンピューターまたはシンクライアントで、リモートデスクトップ接続または同等のアプリケーションを起動し、MultiPoint Services を実行しているコンピューターの名前または IP アドレスを入力します。

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>コネクタサービスを使用してリモート管理用に Windows 10 デバイスをセットアップする
Windows 10 を実行している PC またはラップトップは、次の期間だけリモートで管理できます。
- コネクタサービスが有効になっている  
- コンピューターが MultiPoint サーバーの管理されたコンピューターに追加されています。  

Windows 10 を実行している PC で、次の手順に従って MultiPoint コネクタを有効にします。

1. 検索ボックスに「Windows の機能の有効化または無効化」と入力し、適切な検索結果を選択します。 

2. 機能の一覧で**MultiPoint コネクタ**を有効にします。 これにより、デバイスを管理するために必要な MultiPoint connector サービスが有効になります。 

MultiPoint サーバーで、次のようにします。
1. MultiPoint マネージャーを開き、 **[パーソナルコンピューターの追加または削除]** を選択するか、 **Multipoint Services を追加または削除**します。

2. 管理するリモートコンピューターを選択し、[ **OK]** をクリックします。  リモートコンピューターで管理者の資格情報を入力するように求められます。  この処理が完了すると、MultiPoint マネージャーの [ホーム] タブにリモートコンピューターが表示されます。

ダッシュボードマネージャーを正常に設定すると、管理対象デバイスで作業しているユーザーを監視できます。

> [!IMPORTANT]  
> 管理対象の Windows 10 デバイスを監視するときに、サーバーの設定がそれに応じて変更されている場合を除き、administratrive ユーザーを監視することはできません。 「[サーバー設定の編集](Edit-Server-Settings.md)」を参照してください。