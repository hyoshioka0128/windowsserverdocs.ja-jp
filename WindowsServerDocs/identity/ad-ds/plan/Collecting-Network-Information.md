---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: ネットワーク情報の収集
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6792d565e08a188e1957c67ce419676d4a044d82
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624390"
---
# <a name="collecting-network-information"></a>ネットワーク情報の収集

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) で効果的なサイトトポロジを設計するための最初の手順は、組織のネットワークグループを参照して情報を収集し、物理ネットワークトポロジに関する情報を定期的に伝達することです。

## <a name="creating-a-location-map"></a>場所マップの作成

組織の物理ネットワークインフラストラクチャを表す場所マップを作成します。 [場所] マップで、内部接続が 10 mbps 以上 (ローカルエリアネットワーク (LAN) の速度以上) のコンピューターのグループを含む地理的な場所を特定します。

## <a name="listing-communication-links-and-available-bandwidth"></a>通信リンクと使用可能な帯域幅の一覧表示

ロケーションマップを作成した後、通信リンクの種類、リンク速度、および各場所間の使用可能な帯域幅を文書化します。 ネットワークグループからワイドエリアネットワーク (WAN) トポロジを取得します。 一般的な WAN 回線の種類とその帯域幅の一覧については、「[サイトリンクの設計を作成](../../ad-ds/plan/Creating-a-Site-Link-Design.md)する」の「コストの決定」セクションを参照してください。 サイトトポロジの設計プロセスで、後でサイトリンクを作成するには、この情報が必要になります。

帯域幅とは、一定の時間内に通信チャネル経由で送信できるデータの量のことです。 使用可能な帯域幅は、AD DS で実際に使用できる帯域幅の量を示します。 使用可能な帯域幅情報はネットワークグループから取得できます。また、ネットワークモニターなどのプロトコルアナライザーを使用して、各リンクのトラフィックを分析することもできます。 ネットワークモニターのインストールの詳細については、「[ネットワークトラフィックの監視](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc783075(v=ws.10))」を参照してください。

各場所とそれにリンクされているその他の場所を文書化します。 さらに、通信リンクの種類と使用可能な帯域幅を記録します。 通信リンクと使用可能な帯域幅を一覧表示するためのワークシートについては、「 [Windows Server 2003 展開キット用のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」を参照し、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip をダウンロードして、「地理的な場所と通信リンク」 (DSSTOPO_1) を開きます。

## <a name="listing-ip-subnets-within-each-location"></a>各場所内の IP サブネットの一覧表示

各場所の間で通信リンクと使用可能な帯域幅を文書化したら、各場所に IP サブネットを記録します。 各場所でサブネットマスクと IP アドレスがわかっていない場合は、ネットワークグループを参照してください。

AD DS は、ワークステーションの IP アドレスと各サイトに関連付けられているサブネットを比較することによって、ワークステーションをサイトに関連付けます。 ドメインコントローラーをドメインに追加すると、AD DS も IP アドレスを調べて、最適なサイトに配置します。

各場所に IP サブネットの一覧を表示するためのワークシートについては、「 [Windows Server 2003 Deployment Kit のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」を参照し、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip をダウンロードして、「場所とサブネット」 (DSSTOPO_2) を開きます。

> [!NOTE]
> Windows Server では、IP version 4 (IPv4) アドレスに加えて、IP version 6 (IPv6) のサブネットプレフィックスもサポートしています。 IPv6 サブネットプレフィックスの一覧表示に役立つワークシートについては、「[付録 a: 場所とサブネットプレフィックス](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)」を参照してください。

## <a name="listing-domains-and-number-of-users-for-each-location"></a>各場所のドメインとユーザー数を一覧表示する

場所で表される各地域ドメインのユーザー数は、サイトトポロジの設計プロセスの次の手順である、地域のドメインコントローラーとグローバルカタログサーバーの配置を決定する要因の1つです。 たとえば、リージョンドメインコントローラーを100を超える地域ドメインユーザーが含まれる場所に配置し、WAN リンクに障害が発生した場合でもドメインにログオンできるように計画します。

場所、各場所で表されるドメイン、および各場所で表される各ドメインのユーザー数を記録します。 各場所で表されるドメインとユーザーの数を一覧表示するためのワークシートについては、「 [Windows Server 2003 Deployment Kit のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」を参照し、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services をダウンロードして、「各場所のドメインとユーザー (DSSTOPO_3 .doc)」を参照してください。
