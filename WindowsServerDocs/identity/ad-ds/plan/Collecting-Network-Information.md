---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: ネットワーク情報の収集
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d88cc2fafd9aa4fc221efc901c48fa41ef007a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867043"
---
# <a name="collecting-network-information"></a>ネットワーク情報の収集

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) での効果的なサイト トポロジ設計の最初の手順では、情報を収集し、物理ネットワーク トポロジについて定期的にこれらと通信する、組織のネットワークのグループを参照してください。  
  
## <a name="creating-a-location-map"></a>場所のマップを作成します。

組織の物理ネットワーク インフラストラクチャを表す場所のマップを作成します。 場所のマップでは、コンピューターのグループ 10 メガ ビット/秒 (Mbps) 以上の内部接続 (ローカル エリア ネットワーク (LAN) の速度以上) が含まれている地理的な場所を特定します。  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>通信リンクの一覧と使用可能な帯域幅

場所のマップを作成した後は、通信リンク、リンク速度、および各場所間で使用できる帯域幅の種類を文書化します。 ネットワークのグループには、ワイド エリア ネットワーク (WAN) のトポロジを取得します。 一般的な WAN 回線の種類と、帯域幅の一覧は、「コストを決定する」セクションを参照してください。[サイト リンク設計の作成](../../ad-ds/plan/Creating-a-Site-Link-Design.md)です。 この情報をサイトのトポロジ設計プロセスの後半で、サイト リンクを作成する必要があります。  
  
帯域幅は、所定の時間での通信チャネル経由で送信できるデータの量を表します。 使用できる帯域幅は、AD DS で使用するために実際に使用できる帯域幅の量を表します。 ネットワークのグループから使用可能な帯域幅の情報を入手できますか、ネットワーク モニターなどのプロトコル アナライザーを使用して各リンク上のトラフィックを分析することができます。 ネットワーク モニターをインストールする方法の詳細については、この記事を参照してください。[ネットワーク トラフィックの監視](https://go.microsoft.com/fwlink/?LinkId=107058)します。  
  
各場所とそれにリンクされている他の場所を文書化します。 さらに、レコードの通信リンクと、使用可能な帯域幅の種類。 通信リンクおよび使用できる帯域幅の一覧を支援するために、ワークシートでは、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードし、。「地理的な場所との通信リンク」(DSSTOPO_1.doc) を開きます。  
  
## <a name="listing-ip-subnets-within-each-location"></a>それぞれの場所内の IP サブネットの一覧を表示します。

通信リンクとそれぞれの場所の間で使用可能な帯域幅を文書化した後は、それぞれの場所内の IP サブネットを記録します。 既に不明な各場所内の IP アドレスとサブネット マスク場合、は、ネットワークのグループを参照してください。  
  
AD DS と各サイトに関連付けられているサブネットのワークステーションの IP アドレスを比較することで、サイトをワークステーションに関連付けます。 ドメインにドメイン コント ローラーを追加すると AD DS もの IP アドレスを検査し、最も適切なサイトで配置します。  
  
それぞれの場所内の IP サブネットの一覧を表示するためのワークシートで、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードして開きます"。場所とサブネット"(DSSTOPO_2.doc)。  
  
> [!NOTE]  
> に加えて IP バージョン 4 (IPv4) アドレス、Windows Server は、IP version 6 (IPv6) もサポートしています。 サブネットのプレフィックス。 IPv6 サブネットのプレフィックスを一覧表示を支援するために、ワークシートでは、次を参照してください[付録 a:。場所とサブネットのプレフィックス](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)します。  

## <a name="listing-domains-and-number-of-users-for-each-location"></a>ドメインと場所ごとにユーザーの数を一覧表示します。

場所で表される各地域ドメインのユーザー数は、地域別のドメイン コント ローラーの配置を決定する要因と、グローバル カタログ サーバーのいずれかのサイト トポロジの設計プロセスの次の手順であります。 たとえば、まだログオンできるドメインに WAN リンクが失敗した場合のために、100 を超える地域別のドメイン ユーザーを格納している場所に地域ドメイン コント ローラーを配置する計画します。  
  
場所ごとに、および各場所で表される各ドメインのユーザーの数で表されるドメインの場所を記録します。 ドメインとそれぞれの場所で表されるユーザーの数を一覧表示を支援するために、ワークシートでは、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_Aids_Designing_and_Deploying_Directory_and_ のダウンロード。Security_Services.zip、および「ドメインとユーザーの各場所を開く」(DSSTOPO_3.doc)。  
