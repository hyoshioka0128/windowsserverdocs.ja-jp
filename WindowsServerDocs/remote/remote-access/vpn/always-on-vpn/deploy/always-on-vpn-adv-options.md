---
title: Always On VPN の高度な機能
description: この展開で提供されている、展開シナリオ以外は、セキュリティと VPN 接続の可用性を向上させるために他の高度な VPN 機能を追加できます。
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: a544ac3c1a121874170a2fc78a34bd401b8bebe1
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067432"
---
# Always On VPN の高度な機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** Always On VPN テクノロジについて説明します](../always-on-vpn-technology-overview.md)<br>
& #187 です。[ **[次へ]:** Always On VPN 展開の計画開始](always-on-vpn-deploy-planning.md)

提供されている、展開シナリオ以外は、セキュリティと VPN 接続の可用性を向上させるために他の高度な VPN 機能を追加できます。 たとえば、このようなコンポーネントに役立つ接続を許可する前に、接続しているクライアントが正常な状態であることを確認します。


## 高可用性

高可用性の追加のオプションを次に示します。


|オプション  |説明  |
|---------|---------|
|サーバーの回復性と負荷分散     |高可用性やサポート大量の要求を必要とする環境では、向上することがリモート アクセスの回復性とパフォーマンスを使って、ネットワーク ポリシー サーバー (NPS) を実行していると、リモートを有効化する複数のサーバー間の負荷分散アクセス サーバーのクラスター化します。<p>関連するドキュメントは:<ul><li>[NPS プロキシ サーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[クラスターでのリモート アクセスの展開](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|地理的なサイトの回復性     |地理位置情報の IP ベースの Windows Server 2016 での DNS のグローバル Traffic Manager を使用できます。 強力な地理的な負荷分散のためには、Microsoft Azure Traffic Manager など、グローバル サーバー負荷分散ソリューションを使用できます。<p>関連するドキュメントは:<ul><li>[トラフィック マネージャーの概要](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

---

## 高度な認証

認証の追加のオプションを次に示します。


|オプション  |説明  |
|---------|---------|
|Windows Hello for Business     |Windows 10 の PC とモバイル デバイスでは、Windows Hello for Business により、パスワードが強固な 2 要素認証に置き換えられます。 この認証は、新しい種類は、デバイスに関連付けられて、生体認証を使用して、ユーザーの資格情報や暗証番号 (PIN) で構成されます。<p>Windows 10 VPN クライアントは、Windows こんにちは for Business との互換性。 ジェスチャを使用して、ユーザーがログに記録した後、VPN 接続を使用して、Windows こんにちは for Business の証明書認証の証明書ベースのします。<p>関連するドキュメントは:<ul><li>[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>技術的なケース スタディ: [Windows こんにちは for Business は Windows 10 でのリモート アクセスを有効にします。](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure の多要素認証 (MFA)     |Azure MFA がクラウドとオンプレミスのバージョンを Windows VPN 認証メカニズムと統合することができます。<p>このメカニズムのしくみについて詳しくは、 [Azure Multi-factor Authentication Server を使用して RADIUS の統合認証](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)を参照してください。         |

---

## VPN の高度な機能

高度な機能の追加のオプションを次に示します。


|オプション  |説明  |
|---------|---------|
|トラフィック フィルター     |クライアントがアクセス可能なアプリケーションの VPN を適用する必要がある場合は、VPN トラフィック フィルターを有効にできます。<p>詳細については、 [VPN セキュリティ機能](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)を参照してください。         |
|アプリ トリガー VPN     |特定のアプリケーションや種類のアプリケーションを起動するときに自動的に接続する VPN プロファイルを構成することができます。<p>これとその他のトリガーのオプションについて詳しくは、 [VPN 自動トリガー プロファイル オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)を参照してください。         |
|VPN の条件付きアクセス   |条件付きアクセスとデバイスのコンプライアンス標準を満たすため、VPN に接続する前に、管理対象デバイスを要求できます。 VPN の条件付きアクセス用の高度な機能の 1 つ使用すると、クライアント認証証明書が 'AAD の条件付きアクセスの OID 1.3.6.1.4.1.311.87 の '' を含むものだけに VPN 接続を制限することができます。<p>VPN 接続を制限する必要があります。<ol><li>NPS サーバー、**ネットワーク ポリシー サーバー**の管理スナップインを開きます。</li><li>**ポリシー**を展開 > **ネットワーク ポリシー**。</li><li>**仮想プライベート ネットワーク (VPN) 接続**のネットワーク ポリシーを右クリックし、[**プロパティ**] を選択します。</li><li>**[設定**] タブを選択します。</li><li>**ベンダー固有**の選択し、**追加**] をクリックします。</li><li>**許可されている-証明書の OID**オプションを選択し、[**追加**] をクリックします。</li><li>属性値として**1.3.6.1.4.1.311.87**の AAD の条件付きアクセス OID を貼り付けるし、 **[ok]** を 2 回クリックします。</li><li>**Close**し、[**適用**] をクリックします。<p>ここで VPN クライアントは、クラウドの有効期間が短い証明書以外のすべての証明書を使用して接続するときに、接続は失敗します。</li></ol>条件付きアクセスの詳細については、 [VPN および条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)を参照してください。   |

---


## 追加の保護

**トラステッド プラットフォーム モジュール (TPM) キーの構成証明**<p>
TPM の構成証明されたキーを持つユーザー証明書より高いセキュリティ保証、以外のエクスポート、ハンマリング対策のキーは TPM によって提供される分離、バックアップを提供します。

Windows 10 では、TPM キーの構成証明について詳しくは、 [TPM キーの構成証明](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)を参照してください。

## 次の手順
[Always On VPN 展開の計画開始](always-on-vpn-deploy-planning.md): VPN サーバーとして使用を計画しているコンピューターで、リモート アクセス サーバーの役割をインストールする前に、次のタスクを実行します。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。  

---

## 関連トピック
- [NPS プロキシ サーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): 仮想プライベート ネットワーク (VPN) サーバーとワイヤレス アクセス ポイントなどのネットワーク アクセスのサーバーであり、リモート認証ダイヤルイン ユーザー サービス (RADIUS) クライアントが接続要求を作成し、radius 送信NPS などのサーバー。 場合によっては、NPS サーバー可能性がありますが多すぎる接続要求を受信同時に、パフォーマンスの低下またはオーバー ロードです。

- [Traffic Manager の概要](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): このトピックでは、概要の Azure Traffic Manager、サービス エンドポイントのユーザーへのトラフィックの配布を制御できます。 トラフィックのマネージャーは、最も適切なエンドポイントへのトラフィックをルーティング メソッドと、エンドポイントの正常性に基づくをクライアントに要求を送信するのにドメイン ネーム システム (DNS) を使用します。 

- [Windows こんにちは for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): このトピックで説明など、クラウドのみの展開とハイブリッド展開の前提条件です。  また、このトピックでは、Windows こんにちは for Business に関してよく寄せられる質問を示します。

- [技術的なケース スタディ: を有効にするリモート アクセスと Windows こんにちは for Business は Windows 10 で](https://msdn.microsoft.com/library/mt728163.aspx): このテクニカル ケース スタディでは Microsoft が Windows hello for Business のリモート アクセスを実装するか説明します。  Windows こんにちは for Business は、プライベート/公開キーまたはパスワードを超える企業とコンシューマーの証明書ベースの認証方法。 この形式の認証は、パスワードを置き換えることができますし、侵害、盗用、およびフィッシングに抵抗力がキーのペアの資格情報に依存しています。 

- [Azure Multi-factor Authentication Server との統合 RADIUS 認証](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): このトピックでは追加すると、Azure Multi-factor Authentication server RADIUS クライアントの認証を構成します。 半径は、認証要求を承認して、それらの要求を処理する標準的なプロトコルです。 Azure Multi-factor Authentication Server は、RADIUS サーバーとして使用できます。 

- [VPN セキュリティ機能](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): このトピックでは、VPN のセキュリティ ガイドライン ロックダウン vpn は、VPN では、Windows 情報保護 (WIP) の統合とトラフィック フィルター処理します。 

- [VPN 自動トリガー プロファイル オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): このトピックでは、アプリのトリガーなどの名前に基づくトリガー、Always On VPN 自動トリガー プロファイル オプションを提供します。

- [VPN および条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): このトピックでは、リモート クライアント用のデバイス コンプライアンス オプションを提供するための条件付きアクセス プラットフォームのクラウド ベースの概要を示します。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

- [TPM キーの構成証明](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): このトピックでは、トラステッド プラットフォーム モジュール (TPM) の概要を提供し、キーの構成証明の TPM を展開する手順を実行します。 トラブルシューティングの情報および問題を解決する手順を検索することもできます。 

---