---
title: リモート アクセス Always On VPN 移行の計画
description: DirectAccess から Always On VPN に移行するには、適切な計画を移行のフェーズの判断により、組織全体に影響が及ぶ前に、問題を特定する必要があります。
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 494dc7916b505991c22b07bec738c2300d660ec1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835673"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess から Always On VPN への移行の計画

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#171;[**前。** DirectAccess Always On VPN への移行からの概要](da-always-on-migration-overview.md)<br>
&#187;[ **[次へ]。** Always On VPN に移行し、DirectAccess を使用停止](da-always-on-migration-deploy.md)


DirectAccess から Always On VPN に移行するには、適切な計画を移行のフェーズの判断により、組織全体に影響が及ぶ前に、問題を特定する必要があります。 移行の主な目的は、ユーザーがプロセス全体を通じてオフィスへのリモート接続を維持できるようにすることです。 不適切な順序でタスクを実行すると、競合状態が発生し、リモート ユーザーが会社のリソースにアクセスできなくなります。 そのため、Microsoft では、DirectAccess から計画済み、サイド バイ サイド移行を実行する Always On VPN をお勧めします。 詳細については、次を参照してください。、 [Always On VPN 展開の移行](da-always-on-migration-deploy.md)セクション。

ユーザーの移行、標準の構成に関する考慮事項、および Always On VPN の機能強化を分離することの利点について説明します。 移行計画のフェーズは次のとおりです。

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>移行のリングをビルドします。
移行のリングを使用して、Always On VPN クライアントの移行作業を複数のフェーズに分割します。 最後のフェーズを取得するまでに、プロセスはもテストと一貫性のあるをする必要があります。

このセクションでは、移行のフェーズにユーザーを分離し、し、これらのフェーズを管理するための 1 つの方法を提供します。 選択したユーザーのフェーズの分離方法に関係なく、移行が完了したら、管理を容易に 1 つの VPN ユーザー グループを維持します。

>[!NOTE] 
>単語_フェーズ_長いプロセスであることを示すものではありません。 各フェーズでは、数日または数か月間を移動するかどうかは、サイド バイ サイド移行を活用し、段階的なアプローチを使用するをお勧めします。

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>移行作業を複数のフェーズに分割するメリット

-   **大容量の障害保護します。** フェーズに移行を除算すると、ユーザーに影響する可能性の移行によって生成された問題の数がはるかに小さいです。

-   **プロセスまたはフィードバックからの通信の機能強化。** 理想的には、ユーザーが付かない場合も、移行が発生したことです。 ただし、経験最適ではない場合は、これらの使用からのフィードバックでは、計画を改善し、今後の問題を回避します。

### <a name="tips-for-building-your-migration-ring"></a>移行のリングを構築するためのヒント

-   **リモート ユーザーを特定します。** 2 つのバケットにユーザーを分離することで開始: 多くの場合、office としないユーザーに、人。 移行プロセスは両方のグループに対して同じですが、するよりも頻繁に接続しているユーザーにとって、更新を受信するリモート クライアントの時間がかかる可能性があります。 理想的には、移行の各フェーズは、各バケットからメンバーを含める必要があります。

-  **ユーザーを優先します。** リーダーシップと影響の大きいの他のユーザーは通常最後のユーザー間で移行します。 ユーザーの優先順位付け、ときに、自身のクライアント コンピューターの移行が失敗する場合、ビジネスの生産性への影響をただし、検討します。 たとえば、1 ~ 3 の評価がある場合 1 の意味を持つ従業員ができない作業、つまり作業を即時中断することなく、が 3 内部の基幹業務 (LOB) アプリのみをリモートで使用するビジネス アナリストがある、1 には、クラウドを使用して販売員 アプリは、3 になります。

-   **複数のフェーズでは、各部門や部署を移行します。** 一度に部門全体を移行しないことを強くお勧めします。 問題が発生した場合たくない全体の部門のリモートの作業を妨げること。 代わりに、各部門またはビジネス ユニットを少なくとも 2 つのフェーズで移行します。

-   **ユーザー数が徐々 に増やします。** 最も一般的な移行シナリオでは、IT 組織のメンバーと起動し、ビジネス ユーザーが後にリーダーシップと影響の大きいの他のユーザーに、移動します。 通常、移行の各フェーズには、段階的により多くの人が含まれます。 たとえば、最初のフェーズが 10 人のユーザーを含めることができ、最後のグループは、5,000 人のユーザーを含めることができます。 展開を簡素化するには、1 つの VPN ユーザーのセキュリティ グループを作成し、ユーザーを追加、フェーズが到着するとします。 これにより、最終的に 1 つの VPN ユーザー グループにメンバーを追加できますが後でします。

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>次の手順

|目的の処理  |参照先  |
|---------|---------|
|Always On VPN への移行を開始します。     |[Always On VPN に移行し、DirectAccess を使用停止](da-always-on-migration-deploy.md)します。 DirectAccess から Always On VPN への移行には、特定のプロセスに役立ちますが順不同の移行手順の実行に起因する競合状態を最小限に抑えるクライアントを移行する必要があります。         |
|Always On VPN と DirectAccess の両方の機能について説明します    |[機能の Always On VPN と DirectAccess の比較](../vpn/vpn-map-da.md)します。 以前のバージョンの Windows VPN アーキテクチャでは、プラットフォームの制限のために、(ユーザーのサインインの前に開始される自動接続のような) DirectAccess を置き換えるために必要とされる重要な機能を提供することは困難でした。 ただし、Always On VPN ではこれらのほとんどの制限を軽減し、DirectAccess の機能を越えて VPN 機能を拡張しました。         |



---