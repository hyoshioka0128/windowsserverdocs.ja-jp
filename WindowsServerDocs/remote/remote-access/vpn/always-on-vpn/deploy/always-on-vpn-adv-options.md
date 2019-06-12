---
title: Always On VPN の高度な機能
description: この展開で提供される展開シナリオ、以外は、セキュリティと、VPN 接続の可用性を向上させるその他の高度な VPN 機能を追加できます。
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 7534f631cf0ac3f8230ea12e790dcd946da0ffbd
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749519"
---
# <a name="advanced-features-of-always-on-vpn"></a>Always On VPN の高度な機能

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** Always On VPN テクノロジについて説明します](../always-on-vpn-technology-overview.md)
- [**次に：** Always On VPN 展開の計画を開始します。](always-on-vpn-deploy-planning.md)

提供される展開シナリオ、セキュリティと、VPN 接続の可用性を向上させるその他の高度な VPN 機能を追加できます。 たとえば、このようなコンポーネントでは、接続を許可する前に接続するクライアントが正常であるが役立ちます。

## <a name="high-availability"></a>高可用性

高可用性のための追加のオプションを次に示します。

|オプション  |説明  |
|---------|---------|
|サーバーの回復性と負荷分散     |高可用性とサポート大量の要求を必要とする環境を向上することが、パフォーマンスとリモート アクセスの回復性は、ネットワーク ポリシー サーバー (NPS) を実行して、リモートの有効化する複数のサーバー間の負荷分散を使用して、アクセス サーバーのクラスター化します。<p>関連ドキュメント:<ul><li>[NPS プロキシ サーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[クラスターでのリモート アクセスの展開](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|地理的なサイトの回復性     |IP ベースの位置情報では、Windows Server 2016 で DNS に Global Traffic Manager を使用できます。 堅牢な地理的な負荷分散で、グローバル サーバー負荷分散ソリューション、Microsoft Azure Traffic Manager などを使用することができます。<p>関連ドキュメント:<ul><li>[Traffic Manager の概要](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>高度な認証

認証の追加オプションを次に示します。

|オプション  |説明  |
|---------|---------|
|Windows Hello for Business     |Windows Hello for Business は、Windows 10 の PC とモバイル デバイスで、パスワードに替わる強固な 2 要素認証機能を提供します。 この認証は、新しい種類のデバイスに関連付けられているし、生体認証を使用しているユーザーの資格情報や暗証番号 (PIN) で構成されます。<p>Windows 10 の VPN クライアントは、Windows こんにちは for Business との互換性。 ユーザーがログインのジェスチャを使用して、VPN 接続を使用して、Windows こんにちは for Business の証明書の証明書ベースの認証。<p>関連ドキュメント:<ul><li>[Windows こんにちは for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>技術的なケース スタディ:[Windows 10 でビジネス向け Windows こんにちはを使用したリモート アクセスを有効にします。](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-factor Authentication (MFA)     |Azure MFA がクラウドとオンプレミス バージョンの Windows VPN 認証メカニズムと統合することができます。<p>このメカニズムの動作方法の詳細については、次を参照してください。[と Azure Multi-factor Authentication Server の統合の RADIUS 認証](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)します。         |

## <a name="advanced-vpn-features"></a>高度な VPN 機能

高度な機能の追加オプションを次に示します。

|オプション  |説明  |
|---------|---------|
|トラフィックのフィルター処理     |クライアントがアクセス可能なアプリケーションの VPN を強制する必要がある場合は、VPN トラフィックのフィルターを有効にすることができます。<p>詳細については、次を参照してください。 [VPN セキュリティ機能](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)します。         |
|アプリ トリガー VPN     |特定のアプリケーションやアプリケーションの種類の開始時に自動的に接続する VPN プロファイルを構成することができます。<p>これと他のトリガーを起動するオプションの詳細については、次を参照してください。 [VPN プロファイルの自動トリガー オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)します。         |
|VPN の条件付きアクセス   |条件付きアクセスとデバイスのコンプライアンス標準を満たす VPN に接続する管理対象デバイスを要求できます。 条件付きアクセスの VPN の高度な機能の 1 つ使用すると、クライアント認証証明書が 'AAD の条件付きアクセスの OID 1.3.6.1.4.1.311.87 の '' が含まれているもののみに VPN 接続を制限することができます。<p>VPN 接続を制限するには、する必要があります。<ol><li>NPS サーバーで開く、**ネットワーク ポリシー サーバー**スナップイン。</li><li>展開**ポリシー** > **ネットワーク ポリシー**します。</li><li>右クリックし、**仮想プライベート ネットワーク (VPN) 接続**ネットワーク ポリシーと選択**プロパティ**します。</li><li>選択、**設定**タブ。</li><li>選択**ベンダー固有**選択**追加**します。</li><li>選択、**許可されている証明書の OID**オプションを選択して**追加**します。</li><li>条件付きアクセス AAD OID を貼り付けます**1.3.6.1.4.1.311.87**として選択し、属性の値を**OK** 2 回です。</li><li>選択**閉じる**し**適用**します。<p>これで VPN クライアントは、有効期間が短いクラウド証明書以外の任意の証明書を使用して接続するときに、接続は失敗します。</li></ol>条件付きアクセスの詳細については、次を参照してください。 [VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)します。   |

## <a name="additional-protection"></a>追加の保護

### <a name="trusted-platform-module-tpm-key-attestation"></a>トラステッド プラットフォーム モジュール (TPM) キーの構成証明

TPM 証明キーを持つユーザーの証明書は、非エクスポート可能性、ハンマリング対策および TPM によって提供されるキーの分離によってバックアップより高いセキュリティ保証を提供します。

Windows 10 での TPM キー認証の詳細については、次を参照してください。 [TPM キーの構成証明](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)します。

## <a name="next-step"></a>次の手順

[Always On VPN 展開の計画を開始する](always-on-vpn-deploy-planning.md):VPN サーバーとして使用してを予定しているコンピューターのリモート アクセス サーバーの役割をインストールする前に、次のタスクを実行します。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。  

## <a name="related-topics"></a>関連トピック
- [NPS プロキシ サーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md):仮想プライベート ネットワーク (VPN) サーバーやワイヤレス アクセス ポイントなどのネットワーク アクセス サーバーとは、リモート認証ダイヤルイン ユーザー サービス (RADIUS) クライアントでは、接続要求を作成し、NPS などの RADIUS サーバーに送信します。 場合によっては、NPS サーバー可能性がありますが多すぎる接続要求を受信同時に、パフォーマンスの低下やオーバー ロードします。

- [Traffic Manager の概要](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview):このトピックでは、Azure Traffic Manager の概要、サービス エンドポイントに対するユーザー トラフィックの分散を制御することができますを提供します。 Traffic Manager では、ドメイン ネーム システム (DNS) を使用して、トラフィック ルーティング方法と、エンドポイントの正常性に基づいて最適なエンドポイントにクライアント要求を送信します。 

- [Windows こんにちは for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification):このトピックでは、クラウドのみのデプロイとハイブリッド デプロイなど、前提条件を提供します。  このトピックでは、Windows こんにちは for Business についてよく寄せられる質問も一覧表示します。

- [技術的なケース スタディ:Windows 10 でビジネス向け Windows こんにちはを使用したリモート アクセスを有効にする](https://msdn.microsoft.com/library/mt728163.aspx):この技術的なケース スタディでは、マイクロソフトで Windows こんにちは for Business のリモート アクセスを実装する方法を説明します。  Windows こんにちは for Business は、秘密/公開キーまたはパスワードを超える組織とコンシューマー向けの証明書ベースの認証方式。 この形式の認証は、パスワードに置き換えることができますし、侵害、耐性、フィッシングに対するがキーのペアの資格情報に依存します。 

- [Azure Multi-factor Authentication Server と RADIUS 認証を統合](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius):このトピックでは、追加して、Azure Multi-factor Authentication Server を RADIUS クライアントの認証を構成するについて説明します。 RADIUS は、認証要求を受け入れ、それらの要求を処理する標準のプロトコルです。 Azure Multi-factor Authentication Server は、RADIUS サーバーとして機能できます。 

- [VPN セキュリティ機能](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features):このトピックでは、VPN のロックダウン、VPN、およびトラフィックのフィルターと Windows 情報保護 (WIP) の統合の VPN セキュリティ ガイドラインを提供します。 

- [VPN プロファイルの自動トリガー オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile):このトピックでは、アプリのトリガー、名前に基づくトリガー、および Always On などの VPN プロファイルの自動トリガー オプションを提供します。

- [VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):このトピックでは、リモート クライアントのデバイス コンプライアンスのオプションを提供する条件付きアクセスのプラットフォームをクラウド ベースの概要を示します。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

- [TPM キー認証](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation):このトピックでは、TPM キー認証をデプロイするには、トラステッド プラットフォーム モジュール (TPM) と手順の概要を示します。 トラブルシューティングの情報と問題を解決する手順を検索することもできます。