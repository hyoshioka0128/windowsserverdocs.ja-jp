---
title: リモート アクセス Always On VPN 移行の概要
description: Always On VPN では、Windows Vpn や DirectAccess は、DirectAccess から Always On VPN に移行する方法と、前のギャップを説明します。
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 402d8ff72fe869572c9e6129cdf1aa7e755c354a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845983"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess から Always On VPN への移行の概要 

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#187;[ **[次へ]。** DirectAccess Always On VPN への移行からを計画します。](da-always-on-migration-planning.md)

プラットフォームの制限事項は Windows VPN アーキテクチャの以前のバージョンで行ったユーザーがサインインする前に開始された自動接続など、DirectAccess を置き換えるために必要重要な機能を提供するが困難。 ただし、Always On VPN ではこれらのほとんどの制限を軽減し、DirectAccess の機能を越えて VPN 機能を拡張しました。 Always On VPN では、Windows Vpn や DirectAccess の以前のギャップを説明します。

VPN の移行プロセスで DirectAccess – に – Always は、次の 4 つの主要なコンポーネントと高度なプロセスで構成されます。


1.  **Always On VPN 移行を計画します。** 計画には、ユーザーのフェーズの分離だけでなくインフラストラクチャと機能の対象となるクライアントを識別するのに役立ちます。

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **サイド バイ サイドでの VPN インフラストラクチャをデプロイします。** 移行のフェーズと展開に追加する機能を確認した後は、既存の DirectAccess のインフラストラクチャと並行 Always On VPN インフラストラクチャを展開します。  

3.  **証明書と構成をクライアントに展開します。**  VPN インフラストラクチャ準備ができたら、作成し、クライアントに必要な証明書を発行します。 クライアントが証明書を受信したときに、VPN_Profile.ps1 構成スクリプトを配置します。 または、Intune を使用して、VPN クライアントを構成することができます。 正常な VPN 構成の展開を監視するには、Microsoft System Center Configuration Manager または Microsoft Intune を使用します。

4.  **削除し、使用を停止します。** DirectAccess からのすべてのユーザーを移行した後、環境の使用を正しく停止します。

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>DirectAccess の展開シナリオ

この展開シナリオではこのガイドでは、移行の開始点として、単純な DirectAccess 展開シナリオを使用します。 Always On VPN に移行する前にこの展開シナリオに一致する必要はありませんが、多くの組織でこの簡単なセットアップは正確に表す、現在の DirectAccess の展開。 次の表は、このセットアップの基本的な機能の一覧を示します。

DirectAccess の展開シナリオとオプションの多くがあるため、実装は、ここで説明したものと異なるする可能性があります。 そうである場合を参照してください[DirectAccess と Always On VPN の機能のマッピング](../vpn/vpn-map-da.md)を Always On VPN 機能は、最新のパッチのマッピングを設定するかを判断し、構成にこれらの機能を追加します。 またを参照することができます、 [Always On VPN の機能強化](../vpn/always-on-vpn/always-on-vpn-enhancements.md)Always On VPN 展開にオプションを追加します。

>[!NOTE] 
>非ドメイン参加済みデバイスでは、証明書の登録など、追加の考慮事項があります。 詳細については、次を参照してください。 [Always On VPN 展開の Windows Server および Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)します。

### <a name="deployment-scenario-feature-list"></a>展開シナリオの機能の一覧

| DirectAccess 機能 | 一般的なシナリオ |
|-----|----|
| 展開方法                   | クライアント アクセスとリモート管理の完全な DirectAccess を展開します。                                               |
| ネットワーク アダプター                      | 2                                                                                                              |
| ユーザー認証                   | Active Directory の資格情報                                                                                   |
| コンピューターの証明書の使用             | 〇                                                                                                            |
| セキュリティ グループ                       | 〇                                                                                                            |
| 単一の DirectAccess サーバー            | 〇                                                                                                            |
| ネットワーク トポロジ                      | ネットワーク アドレス変換 (NAT)、エッジ ファイアウォールの背後にある 2 つのネットワーク アダプター                            |
| アクセス モード                           | Edge を終了します。                                                                                                    |
| トンネリング:                             | 分割トンネル                                                                                                   |
| 認証                        | コンピューターの証明書と Kerberos (KerbProxy ではない) 標準の公開キー基盤 (PKI) 認証 |
| プロトコル                             | HTTPS (IP-HTTPS) 経由で IP                                                                                       |
| ネットワーク ロケーション サーバー (NLS) のボックスをオフ | 〇                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always On VPN 展開シナリオ

この展開シナリオでは、DirectAccess の移行ソリューションでは単純な Always On VPN 環境への単純な環境が DirectAccess の移行に専念します。 次の表では、この単純なソリューションで使用する機能を提供します。 Always On VPN クライアントに追加の機能強化について詳細を参照してください。 [Always On VPN の機能強化](../vpn/always-on-vpn/always-on-vpn-enhancements.md)します。

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>単純な環境で使用される always On VPN 機能

| VPN 機能 | 展開シナリオの構成 |
|-----|-----|
| 接続の種類 | ネイティブのインターネット キー交換バージョン 2 (IKEv2) |
| ネットワーク アダプター   | 2        |
| ユーザー認証  | Active Directory の資格情報            |
| コンピューターの証明書の使用        | 〇                          |
| ルーティング | 分割トンネリング |
| 名前解決 | ドメイン名情報一覧とドメイン ネーム システム (DNS) サフィックス |
| トリガーします。 | 常にオンおよび信頼されたネットワーク検出 |
| 認証  | 保護された拡張認証プロトコル-トランスポート層セキュリティ (PEAP-TLS) トラステッド プラットフォーム モジュールで保護されたユーザー証明書の使用 |

## <a name="next-step"></a>次の手順

[DirectAccess Always On VPN への移行からを計画](da-always-on-migration-planning.md)します。 移行の主な目的は、ユーザーがプロセス全体を通じてオフィスへのリモート接続を維持できるようにすることです。

---