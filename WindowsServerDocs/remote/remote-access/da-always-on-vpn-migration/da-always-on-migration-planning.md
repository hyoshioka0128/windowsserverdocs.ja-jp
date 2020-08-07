---
title: リモートアクセス Always On VPN 移行計画
description: DirectAccess から Always On VPN に移行するには、移行フェーズを決定するための適切な計画が必要です。これは、組織全体に影響を与える前に問題を特定するのに役立ちます。
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: 57b44b90213ca756666b83aa934bc6fd42fa609b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951427"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess から Always On VPN への移行の計画

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

[**前**の &#171;: VPN 移行を Always On する DirectAccess の概要](da-always-on-migration-overview.md)<br>
&#187; [**次:** Always On VPN に移行して DirectAccess を使用停止にする](da-always-on-migration-deploy.md)


DirectAccess から Always On VPN に移行するには、移行フェーズを決定するための適切な計画が必要です。これは、組織全体に影響を与える前に問題を特定するのに役立ちます。 移行の主な目的は、ユーザーがプロセス全体を通じてオフィスへのリモート接続を維持できるようにすることです。 不適切な順序でタスクを実行すると、競合状態が発生し、リモート ユーザーが会社のリソースにアクセスできなくなります。 そのため、DirectAccess から Always On VPN への計画されたサイドバイサイド移行を実行することをお勧めします。 詳細については、「 [ALWAYS ON VPN migration deployment](da-always-on-migration-deploy.md) 」セクションを参照してください。

このセクションでは、移行のためにユーザーを分離する利点、標準的な構成に関する考慮事項、および Always On VPN 機能の強化について説明します。 移行計画フェーズには次のものが含まれます。

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)]

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)]

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>ビルド移行リング
移行リングは、Always On VPN クライアントの移行作業を複数のフェーズに分割するために使用されます。 最後のフェーズに達すると、プロセスは十分にテストされ、一貫した状態になります。

このセクションでは、ユーザーを移行フェーズに分割してから、それらのフェーズを管理する方法の1つを紹介します。 選択したユーザーフェーズの分離方法に関係なく、1つの VPN ユーザーグループを管理して、移行が完了したときの管理を容易にします。

>[!NOTE]
>単語_フェーズ_は、これが長いプロセスであることを示すためのものではありません。 各フェーズを数日間、または数か月で移動する場合でも、サイドバイサイド移行を利用し、段階的なアプローチを使用することをお勧めします。

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>移行作業を複数のフェーズに分割する利点

-   **一括停止の保護。** 移行を段階的に分割することによって、移行によって生成される問題が影響を受ける可能性があります。

-   **フィードバックによって処理またはコミュニケーションが向上します。** ユーザーは、移行が行われたことに気付かない場合があります。 しかし、経験が最適ではない場合、これらの使用からのフィードバックにより、計画を改善し、将来の問題を回避する機会が得られます。

### <a name="tips-for-building-your-migration-ring"></a>移行リングを構築するためのヒント

-   **リモートユーザーを識別します。** まず、ユーザーを2つのバケットに分割します。つまり、オフィスに頻繁にアクセスするユーザーと、そうでないユーザーを分けます。 移行プロセスは両方のグループで同じですが、より頻繁に接続する場合よりも、リモートクライアントが更新を受信するのに時間がかかることがあります。 各移行フェーズ (理想的) には、各バケットのメンバーが含まれている必要があります。

-  **ユーザーの優先順位を設定します。** リーダーシップとその他の影響の大きいユーザーは、通常、最後に移行されたユーザーの間にあります。 ただし、ユーザーに優先順位を付けた場合は、クライアントコンピューターの移行が失敗した場合に、ビジネスの生産性に与える影響を考慮してください。 たとえば、1 ~ 3 の評価があったとします。1は従業員が仕事をできないことを意味し、3はすぐに作業が中断されないことを意味します。一方、内部の基幹業務 (LOB) アプリのみを使用しているビジネスアナリストは、1になります。

-   **各部門または事業単位を複数のフェーズで移行します。** Microsoft では、部門全体を同時に移行しないことを強くお勧めします。 問題が発生した場合、部門全体のリモート作業が妨げられないようにする必要があります。 代わりに、少なくとも2つのフェーズで各部門または事業単位を移行します。

-   **ユーザーカウントを徐々に増やします。** ほとんどの一般的な移行シナリオでは、IT 組織のメンバーから始めて、ビジネスユーザーに移行し、その後、リーダーシップやその他の影響の大きいユーザーを選択します。 各移行フェーズには、通常、徐々に多くのスタッフが関与します。 たとえば、1番目のフェーズには10人のユーザーが含まれ、最後のグループには5000ユーザーが含まれる場合があります。 デプロイを簡略化するには、1つの VPN ユーザーセキュリティグループを作成し、そのフェーズが到着したときにユーザーを追加します。 このようにして、後でメンバーを追加できる単一の VPN ユーザーグループが作成されます。

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>次のステップ

|目的  |参照先  |
|---------|---------|
|Always On VPN への移行を開始する     |[ALWAYS ON VPN に移行し、DirectAccess を使用停止に](da-always-on-migration-deploy.md)します。 DirectAccess から Always On VPN に移行するには、クライアントを移行するための特定のプロセスが必要です。これにより、移行手順を順番に実行することによって発生する競合状態を最小限に抑えることができます。         |
|Always On VPN と DirectAccess の両方の機能について説明します。    |[ALWAYS ON VPN と DirectAccess の機能の比較](../vpn/vpn-map-da.md)。 以前のバージョンの Windows VPN アーキテクチャでは、プラットフォームの制限のために、(ユーザーのサインインの前に開始される自動接続のような) DirectAccess を置き換えるために必要とされる重要な機能を提供することは困難でした。 ただし、Always On VPN ではこれらのほとんどの制限を軽減し、DirectAccess の機能を越えて VPN 機能を拡張しました。         |



---