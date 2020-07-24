---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: サイト設計の作成
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: fb37fe72c69fb0055632e09b7a6c51ce9f5cb561
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962314"
---
# <a name="creating-a-site-design"></a>サイト設計の作成

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイトの設計を作成するには、サイトにする場所の決定、サイトオブジェクトの作成、サブネットオブジェクトの作成、およびサブネットのサイトへの関連付けを行います。

## <a name="deciding-which-locations-will-become-sites"></a>サイトになる場所の決定

次のように、サイトを作成する場所を決定します。

- ドメインコントローラーを配置するすべての場所のサイトを作成します。 ドメインコントローラーを含む場所を特定するには、「ドメインコントローラーの配置」 (DSSTOPO_4.doc) ワークシートに記載されている情報を参照してください。
- サイトを作成する必要があるアプリケーションを実行しているサーバーを含む場所のサイトを作成します。 分散ファイルシステム名前空間 (DFSN) などの特定のアプリケーションでは、サイトオブジェクトを使用して、クライアントに最も近いサーバーを検索します。

> [!NOTE]
> 組織に、高速で信頼性の高い接続と近接した複数のネットワークがある場合は、それらのネットワークのすべてのサブネットを1つの Active Directory サイトに含めることができます。 たとえば、異なるサブネットにある2つのサーバー間のラウンドトリップがネットワーク待機時間を返す場合、同じ Active Directory サイトに両方のサブネットを含めることができます。 2つの場所の間のネットワーク待機時間が10ミリ秒を超える場合は、サブネットを1つの Active Directory サイトに含めないでください。 待機時間が10ミリ秒以下の場合でも、サイト間のトラフィックを Active Directory ベースのアプリケーション用に分割する場合は、個別のサイトを展開することを選択できます。

- ある場所にサイトが必要ない場合は、場所のサブネットをサイトに追加して、その場所のワイドエリアネットワーク (WAN) の最大速度と使用可能な帯域幅を指定します。

サイトになるドキュメントの場所と、各場所内のネットワークアドレスとサブネットマスク。 サイトの文書化に役立つワークシートについては、「 [Windows Server 2003 展開キット用のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」、「Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードする」、および「サブネットとサイトの関連付け」 (DSSTOPO_6.doc) を参照してください。

## <a name="creating-a-site-object-design"></a>サイトオブジェクトの設計を作成する

サイトの作成を決定した場所ごとに、Active Directory Domain Services (AD DS) でサイトオブジェクトの作成を計画します。 "サブネットとサイトの関連付け" ワークシート内のサイトになるドキュメントの場所。

サイトオブジェクトの作成方法の詳細については、「[サイトを作成](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc772304(v=ws.11))する」を参照してください。

## <a name="creating-a-subnet-object-design"></a>サブネットオブジェクトの設計を作成する

各場所に関連付けられているすべての IP サブネットとサブネットマスクについて、サイト内のすべての IP アドレスを表す AD DS でサブネットオブジェクトを作成することを計画します。

Active Directory サブネットオブジェクトを作成すると、ネットワーク IP サブネットとサブネットマスクに関する情報が、ネットワークプレフィックス長表記形式に自動的に変換され <IP address> / <prefix length> ます。 たとえば、サブネットマスク255.255.252.0 を持つネットワーク IP version 4 (IPv4) アドレス172.16.4.0 は、172.16.4.0/22 として表示されます。 IPv4 アドレスに加えて、Windows Server 2008 では IP version 6 (IPv6) のサブネットプレフィックスもサポートされています。たとえば、3FFE: FFFF: 0: C000::/64 のようになります。 各場所の IP サブネットの詳細については、「[ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md)」および「[付録 a: 場所とサブネットプレフィックス](Appendix-A--Locations-and-Subnet-Prefixes.md)」の「場所とサブネット」 (DSSTOPO_2.doc) ワークシートを参照してください。

各サブネットオブジェクトをサイトオブジェクトに関連付けるには、「サイトになる場所を決定する」の「サブネットをサイトに関連付ける」 (DSSTOPO_6.doc) ワークシートを参照して、どのサブネットをどのサイトに関連付けるかを決定します。 「サブネットとサイトの関連付け」 (DSSTOPO_6.doc) ワークシートの各場所に関連付けられている Active Directory サブネットオブジェクトを文書化します。

サブネットオブジェクトを作成する方法の詳細については、「[サブネットの作成](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc770372(v=ws.11))」を参照してください。
