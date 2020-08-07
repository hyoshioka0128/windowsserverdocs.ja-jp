---
title: リモートアクセス Always On VPN の移行の概要
description: Always On VPN は、Windows Vpn と DirectAccess の間の以前のギャップ、および DirectAccess から Always On VPN に移行する方法を解決します。
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: fcc04dcb9c76a2e25d768de18738078f425f2c76
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953748"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess から Always On VPN への移行の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#187; [**次へ]:** VPN 移行を Always On するように DirectAccess を計画します。](da-always-on-migration-planning.md)

以前のバージョンの Windows VPN アーキテクチャでは、プラットフォームの制限により、ユーザーがサインインする前に自動的に開始される自動接続など、DirectAccess を置き換えるために必要な重要な機能を提供することが難しくなっていました。 ただし、Always On VPN ではこれらのほとんどの制限を軽減し、DirectAccess の機能を越えて VPN 機能を拡張しました。 Always On VPN は、Windows Vpn と DirectAccess の間の以前のギャップを解決します。

DirectAccess – Always On VPN の移行プロセスは、次の4つの主要なコンポーネントと高レベルのプロセスで構成されています。


1.  **Always On VPN 移行を計画します。** 計画によって、ユーザーフェーズの分離の対象クライアントと、インフラストラクチャと機能を識別できます。

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)]

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)]

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **サイドバイサイド VPN インフラストラクチャを展開します。** 移行フェーズと、展開に含める機能を決定したら、既存の DirectAccess インフラストラクチャと共に Always On VPN インフラストラクチャをサイドバイサイドで展開します。

3.  **証明書と構成をクライアントに展開します。**  VPN インフラストラクチャの準備ができたら、必要な証明書を作成してクライアントに発行します。 クライアントが証明書を受信したら、VPN_Profile.ps1 構成スクリプトを展開します。 または、Intune を使用して VPN クライアントを構成することもできます。 Microsoft Endpoint Configuration Manager または Microsoft Intune を使用して、VPN 構成の展開が成功したかを監視します。

4.  **削除して使用を停止します。** DirectAccess からすべてのユーザーを移行した後に、環境を適切に使用停止します。

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>DirectAccess 展開シナリオ

この展開シナリオでは、このガイドで紹介する移行の出発点として、単純な DirectAccess 展開シナリオを使用します。 Always On VPN に移行する前に、この展開シナリオを一致させる必要はありませんが、多くの組織では、この簡易セットアップは、現在の DirectAccess 展開を正確に表現したものです。 次の表に、このセットアップの基本的な機能の一覧を示します。

多くの DirectAccess 展開シナリオとオプションが存在するので、実装はここで説明したものとは異なる可能性があります。 その場合は、「 [DirectAccess と ALWAYS ON vpn の間の機能マッピング](../vpn/vpn-map-da.md)」を参照して、現在の追加に対する Always On vpn 機能セットのマッピングを決定してから、これらの機能を構成に追加します。 また、vpn の[Always On 拡張機能](../vpn/always-on-vpn/always-on-vpn-enhancements.md)を参照して、Always On vpn 展開にオプションを追加することもできます。

>[!NOTE]
>ドメインに参加していないデバイスについては、証明書の登録など、追加の考慮事項があります。 詳細については、「 [Windows Server および windows 10 用の VPN 展開の Always On](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)」を参照してください。

### <a name="deployment-scenario-feature-list"></a>展開シナリオの機能一覧

| DirectAccess 機能 | 一般的なシナリオ |
|-----|----|
| デプロイ シナリオ                   | クライアントアクセスとリモート管理のための完全な DirectAccess を展開する                                               |
| ネットワーク アダプター                      | 2                                                                                                              |
| ユーザー認証                   | Active Directory の資格情報                                                                                   |
| コンピューター証明書を使用する             | はい                                                                                                            |
| セキュリティ グループ                       | はい                                                                                                            |
| 単一の DirectAccess サーバー            | はい                                                                                                            |
| ネットワーク トポロジ                      | 2つのネットワークアダプターを持つエッジファイアウォールの背後にあるネットワークアドレス変換 (NAT)                            |
| アクセス モード                           | 端から端まで                                                                                                    |
| トンネリング                             | 分割トンネル                                                                                                   |
| 認証                        | コンピューター証明書と Kerberos (KerbProxy 以外) を使用した標準の公開キー基盤 (PKI) 認証 |
| プロトコル                             | IP-HTTPS (ip-https)                                                                                       |
| ネットワークロケーションサーバー (NLS) オフボックス | はい                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always On VPN 展開シナリオ

この展開シナリオでは、単純な DirectAccess 環境を単純な Always On VPN 環境 (DirectAccess 置換ソリューション) に移行することに重点を置いて説明します。 次の表は、この簡単なソリューションで使用される機能を示しています。 Always On VPN クライアントのその他の機能強化の詳細については、「 [ALWAYS ON vpn の機能強化](../vpn/always-on-vpn/always-on-vpn-enhancements.md)」を参照してください。

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>単純な環境で使用される VPN 機能の Always On

| VPN 機能 | 展開シナリオの構成 |
|-----|-----|
| 接続の種類 | ネイティブインターネットキー交換バージョン 2 (IKEv2) |
| ネットワーク アダプター   | 2        |
| ユーザー認証  | Active Directory の資格情報            |
| コンピューター証明書を使用する        | はい                          |
| ルーティング | 分割トンネリング |
| 名前解決 | ドメイン名情報の一覧とドメインネームシステム (DNS) サフィックス |
| トリガ | Always on と信頼されたネットワーク検出 |
| 認証  | 保護された拡張認証プロトコル-トラステッドプラットフォームモジュールで保護されたユーザー証明書を使用したトランスポート層セキュリティ (PEAP-TLS) |

## <a name="next-step"></a>次のステップ

[VPN 移行を Always On するように DirectAccess を計画](da-always-on-migration-planning.md)します。 移行の主な目的は、ユーザーがプロセス全体を通じてオフィスへのリモート接続を維持できるようにすることです。

---