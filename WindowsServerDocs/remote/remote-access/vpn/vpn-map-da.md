---
title: Always On VPN の機能
description: このトピックでは、Always On VPN の機能について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.assetid: 8fe1c810-4599-4493-b4b8-73fa9aa18535
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 68d8561eb55b844a80c8b6a38d1255ad44457af6
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066856"
---
# Always On VPN の機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10

&#171;  [**前へ:** Windows Server および Windows 10 のための Always On VPN 展開](always-on-vpn/deploy/always-on-vpn-deploy.md)<br>
&#187; [ **次へ:** Always On VPN の機能強化の詳細](../vpn/always-on-vpn/always-on-vpn-enhancements.md)

このトピックでは、機能と Always On VPN の機能について説明します。  ただし、これには含ま一部の最も一般的な機能とリモート アクセス ソリューションで使われる機能で、次の表は、包括的なリストではありません。 

>[!TIP]
>現在 DirectAccess を使用する場合は、Always On VPN に DirectAccess を形成すべての移行する前にリモート アクセスのニーズに対応している場合を判断するには、慎重に Always On VPN の機能を調べることをお勧めします。  

| 機能領域 | Always On VPN  |
| ---- | ---- |
| 企業ネットワークへのシームレスで透過的な接続。 | Always On VPN 自動トリガー アプリケーションの起動または名前空間の解決要求に基づくをサポートするために構成できます。<p><p>使用して定義します。<br>**VPNv2/ProfileName/AlwaysOn**<br>**VPNv2/ProfileName/AppTriggerList**<br>**VPNv2/ProfileName/DomainNameInformationList/AutoTrigger** |
| 企業ネットワークにサインインしていないユーザーに接続を提供する専用インフラストラクチャ トンネルの使用。 | この機能は、VPN プロファイルのデバイス トンネル機能を使用することで有効にできます。<p><p>_**注: **_<br>デバイス トンネルは、コンピューターの証明書認証を使用する IKEv2 を使用してドメインに参加しているデバイスでのみ構成できます。<p><p>使用して定義します。<br>**VPNv2/ProfileName/DeviceTunnel** |
| 管理の使用 - 企業ネットワーク上の管理システムからクライアントにリモート接続を許可します。 | この機能は、VPN プロファイルでデバイス トンネル機能を使用し、さらに VPN インターフェイスに割り当てられている IP アドレスを内部の DNS サービスに動的に登録するように VPN 接続を構成することで実現できます。<p><p>_**注: **_<br>デバイス トンネル プロファイルでトラフィック フィルターを有効にする場合、デバイス トンネルは (クライアントに企業ネットワーク) からの着信トラフィックを拒否し、します。<p><p>使用して定義します。<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/RegisterDNS** |
| クライアントは、ファイアウォールまたはプロキシ サーバーの背後にあるときに分類されます。 | VPN プロファイル内で自動トンネル/プロトコルの種類を使用して (IKEv2 から) SSTP にフォールバックするように構成できます。<p><p>_**注: **_<br>ユーザー トンネルが SSTP および IKEv2 をサポートし、デバイス トンネル SSTP フォールバックのサポートなしでのみ IKEv2 をサポートしています。<p>使用して定義します。<br>**VPNv2/ProfileName/NativeProfile/NativeProtocolType** |
| エンド ツー エッジ アクセス モードをサポートします。 | Always On VPN では、企業リソースが VPN ゲートウェイに到達するまで認証と暗号化を要求するトンネル ポリシーを使用することで、企業リソースへの接続を提供します。 既定では、トンネル セッションは VPN ゲートウェイで終了します。VPN ゲートウェイは IKEv2 ゲートウェイとしても機能し、エンド ツー エッジのセキュリティを提供します。 |
| コンピューター証明書認証のサポート。 | Always On VPN プラットフォームの一部が VPN 認証のためのコンピューターまたはコンピューターの証明書の使用をサポートとして利用可能な IKEv2 プロトコル種類。<p><p>_**注: **_<br>IKEv2 は、デバイス トンネルのプロトコルのみがサポートして、SSTP フォールバックのサポート オプションはありません。 <p>使用して定義します。<br>**VPNv2/ProfileName/NativeProfile/Authentication/MachineMethod** |
| セキュリティ グループを使用すると、特定のクライアントへのリモート アクセス機能を制限できます。 | RADIUS の使用時に詳細な承認をサポートするように Always On VPN を構成できます。これには、VPN アクセスを制御するためのセキュリティ グループの使用が含まれます。 |
| エッジ ファイアウォール内または NAT デバイスの背後にあるサーバーをサポートします。 | Always On VPN では、NAT デバイスまたはエッジ ファイアウォールの内側にある VPN ゲートウェイの使用を完全にサポートする SSTP および IKEv2 のようなプロトコルを使用することができます。<p><p>_**注: **_<br>ユーザー トンネルが SSTP および IKEv2 をサポートし、デバイス トンネル SSTP フォールバックのサポートなしでのみ IKEv2 をサポートしています。 |
| 企業ネットワークに接続されている場合、イントラネット接続を判別することができます。 | 信頼されたネットワークの検出は、企業のネットワーク接続を検出する機能を提供し、ベースのネットワーク インターフェイスおよびネットワーク プロファイルに割り当てられた接続固有の DNS サフィックスの評価します。<p><p>使用して定義します。<br>**VPNv2/ProfileName/TrustedNetworkDetection** |
| 準拠してネットワーク アクセス保護 (NAP) を使用しています。 | Always On VPN クライアントは Azure の条件付きアクセスと統合して、MFA、デバイス コンプライアンス、または両方の組み合わせを適用します。 条件付きアクセス ポリシーに準拠している場合、Azure AD は、クライアントが VPN ゲートウェイへの認証に使用できる、有効期間が短い (既定で 60 分) IPsec 認証証明書を発行します。 デバイス コンプライアンスでは、System Center Configuration Manager/Intune のコンプライアンス ポリシーを利用します。これには、デバイスの正常性構成証明の状態が含まれます。 この時点で、Azure VPN 条件付きアクセスは、既存の NAP ソリューションに最も近い代替を提供します。ただし、修復サービスまたは検疫ネットワーク機能という形式はありません。 詳細については、 [VPN および条件付きアクセス](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-conditional-access)を参照してください。<p>使用して定義します。<br>**VPNv2/ProfileName/DeviceCompliance** |
| ユーザーがサインインする前にアクセス可能な管理サーバーを定義する機能。 | Always On VPN で、この機能を実現するには、企業ネットワーク上でどの管理システムを使用してアクセス制御トラフィック フィルターと組み合わせることにより、VPN プロファイルでデバイス トンネル機能 (バージョン 1709-の IKEv2 のみで利用可能) を使用して、デバイス トンネルします。<p><p>_**注: **_<br>デバイス トンネル プロファイルでトラフィック フィルターを有効にする場合、デバイス トンネルは (クライアントに企業ネットワーク) からの着信トラフィックを拒否し、します。<p>使用して定義します。<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/TrafficFilterList** |
---

## 追加機能

このセクションの各項目は、ユース ケース シナリオまたはよく使われるリモート アクセスの機能が Always On VPN に強化された機能、いずれかによる機能の拡張または以前の制限の排除します。


| 機能領域 | Always On VPN  |
| ---- | ---- |
| Enterprise SKU の要件を持つドメインに参加しているデバイス。 | Always On VPN は、ドメインに参加しているデバイス、ドメインに参加していない (ワークグループ) デバイス、または Azure AD に参加しているデバイスをサポートして、エンタープライズと BYOD の両方のシナリオを可能にしています。 Always On VPN はすべての Windows エディションで利用可能であり、プラットフォーム機能は UWP VPN プラグイン サポートによってサード パーティが利用可能です。<p><p>_**注: **_<br>デバイス トンネルは 1709 以降、Windows 10 Enterprise または Education バージョンを実行しているドメインに参加しているデバイスでのみ構成できます。 デバイス トンネルのサード パーティ製のコントロールのサポートされていません。 |
| IPv4 と IPv6 の両方のサポート。 | Always On VPN を使用すると、ユーザーは企業ネットワーク上の IPv4 と IPv6 の両方のリソースにアクセスできます。 Always On VPN クライアントでは、IPv6、または VPN ゲートウェイが NAT64 または DNS64 翻訳サービスを提供する必要性に明示的に依存しないデュアル スタック アプローチを使用します。 |
| 2 要素認証または OTP 認証のサポート。 |Always On VPN プラットフォームは、ネイティブで EAP をサポートしています。これにより、認証ワークフローの一部としてさまざまな Microsoft およびサード パーティの EAP の種類の使用が可能になります。 Always On VPN では特にスマート カード (物理および仮想の両方) と Windows Hello for Business の証明書をサポートし、2 要素認証の要件を満たしています。 また、Always On VPN では、EAP RADIUS 統合によって OTP を通じて MFA (サポートされていませんネイティブ、サード パーティ製プラグインでサポートされているのみ) をサポートしています。<p><p>使用して定義します。<br>**VPNv2/ProfileName/NativeProfile/Authentication** |
| 複数ドメインとフォレストのサポート。 | Always On VPN プラットフォームでは VPN クライアントが機能するためにドメインに参加している必要がないため、Active Directory Domain Services (AD DS) フォレストまたはドメイン トポロジに依存することはありません。 そのため、グループ ポリシーは、クライアントの構成時に使用しないため、VPN プロファイル設定を定義するための依存関係ではありません。 Active Directory 承認統合は必要ですが、EAP 認証および承認プロセスの一部として RADIUS によって実現できます。 |
| インターネット/イントラネットのトラフィック分離のための分割トンネルまたは強制トンネルの両方のサポート。 | 強制トンネル (既定の操作モード) および分割トンネルの両方をネイティブでサポートするように Always On VPN を構成できます。 Always On VPN では、アプリケーション固有のルーティング ポリシーのための追加の詳細情報を提供しています。<p><p>_**注: **_<br>ユーザー トンネルのみでサポートされています。<p><p>使用して定義します。<p> **VPNv2/ProfileName/NativeProfile/RoutingPolicyType**<br>**VPNv2/ProfileName/TrafficFilterList/App/RoutingPolicyType** |
| 複数のプロトコルのサポート。 | Always On VPN は、Secure Sockets Layer のフォールバック IKEv2 からが必要な場合は、SSTP をネイティブでサポートするように構成できます。<p><p>_**注: **_<br>ユーザー トンネルが SSTP および IKEv2 をサポートし、デバイス トンネル SSTP フォールバックのサポートなしでのみ IKEv2 をサポートしています。  |
| 企業の接続状態を提供するアシスタントを接続します。 | Always On VPN はネイティブの Network Connectivity Assistant と完全に統合されており、View All Networks インターフェイスから接続状態を提供します。 Windows 10 Creators Update (バージョン 1703) の登場により、VPN 接続の状態、およびユーザー トンネルの VPN 接続の制御にで (Windows 組み込み VPN クライアント用)、ネットワークのポップアップで利用できるも。 |
| 短い名前、完全修飾ドメイン名 (FQDN)、および DNS サフィックスを使用した企業リソースの名前解決。 | Always On VPN では、1 つ以上の DNS サフィックスを VPN 接続および IP アドレス割り当て処理の一部としてネイティブに定義できます (短い名前、FQDN、または DNS 名前空間全体の企業リソースの名前解決を含む)。 Always On VPN では、名前空間に固有の解決の詳細情報を提供する名前解決ポリシー テーブルの使用もサポートします。<p><p>_**注: **_<br>名前解決ポリシー テーブルを使用するときに shortname 解像度と干渉するように、グローバル サフィックスの使用を避けます。<p><p>使用して定義します。<br>**VPNv2/ProfileName/DnsSuffix**<br>**VPNv2/ProfileName/DomainNameInformationList** |
---



## 次のステップ

- [Always On VPN の機能強化について詳しく知る](always-on-vpn/always-on-vpn-enhancements.md)

- [Always On VPN の高度な機能の一部について説明します](always-on-vpn/deploy/always-on-vpn-adv-options.md)

- [Always On VPN テクノロジの詳細の確認](always-on-vpn/always-on-vpn-technology-overview.md)

- [Always On VPN 展開の計画を開始する](always-on-vpn/deploy/always-on-vpn-deploy-deployment.md)

---
