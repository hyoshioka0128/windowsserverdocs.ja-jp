---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: "ネットワーク情報の収集"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 174f11ca85a659f9d0c52e220d5ce37b1804f39b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="collecting-network-information"></a>ネットワーク情報の収集

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory ドメイン サービス (AD DS) で、有効なサイト トポロジの設計の最初の手順に情報を収集し、物理ネットワーク トポロジについて定期的にすると通信する、組織のネットワークのグループを参照してください。  
  
## <a name="creating-a-location-map"></a>位置情報のマップを作成します。  
組織の物理ネットワーク インフラストラクチャを表す場所、マップを作成します。 場所の地図、コンピューターのグループに 10 メガ ビット/秒 (Mbps)、またはそれ以上の内部接続 (ローカル エリア ネットワーク (LAN) の速度またはそれ以上) が含まれている地理的な場所を識別します。  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>通信リンクと使用可能な帯域幅を一覧表示します。  
場所の地図を作成した後は、通信リンク、そのリンク速度、および各場所の間で利用可能な帯域幅の種類を文書化します。 ネットワーク グループから、ワイド エリア ネットワーク (WAN) のトポロジを取得します。 一般的な WAN 接続の種類と、帯域幅の一覧は、「コストを決定する」セクションを参照して[サイト リンク設計を作成する](../../ad-ds/plan/Creating-a-Site-Link-Design.md)します。 この情報をサイト トポロジの設計プロセスの後でサイト リンクを作成する必要があります。  
  
帯域幅は、指定された時間内の通信チャネルの間で送信できるデータの量を指します。 利用可能な帯域幅は、AD DS で使用するため、実際に使用できる帯域幅の量を指します。 利用可能な帯域幅の情報を取得するには、ネットワーク グループから、または Windows Server 2008 に付属しているコンポーネントである、ネットワーク モニターなどのプロトコル アナライザを使用して各リンク上のトラフィックを分析することができます。 ネットワーク モニターをインストールする方法については、ネットワーク トラフィックの監視を参照してください ([https://go.microsoft.com/fwlink/?LinkId=107058](https://go.microsoft.com/fwlink/?LinkId=107058))。  
  
それぞれの場所とそれにリンクされている他の場所を文書化します。 さらに、通信リンクとその利用可能な帯域幅の種類を記録します。 通信リンクと使用可能な帯域幅を一覧表示するためのワークシートで、ジョブ エイドの Windows Server 2003 導入ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))、ダウンロード。Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip、および「地理的な場所との通信リンク」(DSSTOPO_1.doc) を開きます。  
  
## <a name="listing-ip-subnets-within-each-location"></a>各場所での IP サブネットを一覧表示します。  
通信リンクと各場所の間で利用可能な帯域幅を文書化した後は、各場所で、IP サブネットを記録します。 既に把握していない各場所内の IP アドレスとサブネット マスク場合、は、ネットワークのグループを参照してください。  
  
AD DS では、各サイトに関連付けられているサブネットを含む、ワークステーションの IP アドレスを比較することによって、サイトにワークステーションを関連付けます。 ドメインにドメイン コントローラーを追加すると、AD DS も、IP アドレスを調べてし、最も適切なサイトに配置します。  
  
各場所で、IP サブネットを一覧表示するためのワークシートで、ジョブ エイドの Windows Server 2003 導入ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip と開いている「場所とサブネット」(DSSTOPO_2.doc).  
  
> [!NOTE]  
> に加えて IP バージョン 4 (IPv4) アドレス、Windows Server 2008 もサポートしています IP version 6 (IPv6) のサブネット プレフィックスです。 IPv6 サブネット プレフィックスの一覧を表示するためのワークシートで、次を参照してください。[付録 a: 場所とサブネットのプレフィックス](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)します。  
  
## <a name="listing-domains-and-number-of-users-for-each-location"></a>ドメインとユーザーの各場所の数を一覧表示します。  
各場所で表される地域ドメインのユーザーの数は 1 つ地域ドメイン コントローラーの配置を決定する要因とグローバル カタログ サーバーのサイト トポロジの設計プロセスの次の手順であります。 たとえば、100 を超える地域別のドメイン ユーザーを含むことができますまだにログオンする、ドメイン、WAN リンクが失敗した場合の場所に地域ドメイン コントローラーを配置する予定です。  
  
場所ごとに、および各場所で表されるドメインごとにユーザーの数で表されているドメインの場所を記録します。 各場所で表されているユーザーの数とドメインの一覧を表示するためのワークシートで、ジョブ エイドの Windows Server 2003 導入ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))、ダウンロード < DICT__Job_Aids_Designing_and_Deploying_。Directory_and_Security_Services.zip>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip >、"ドメインとユーザーの各場所] を開きます(DSSTOPO_3.doc) します。  
  


