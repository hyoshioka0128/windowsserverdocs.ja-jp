---
title: Always On VPN の高度な機能
description: この展開で提供される展開シナリオ以外にも、VPN 接続のセキュリティと可用性を向上させるために、他の高度な VPN 機能を追加することができます。
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/24/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: fd3ebf1acada5de1ed3f4b14ddeca761728ffa75
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965544"
---
# <a name="advanced-features-of-always-on-vpn"></a>Always On VPN の高度な機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** Always On VPN テクノロジについて](../always-on-vpn-technology-overview.md)
- [**次のようになります。** Always On VPN 展開の計画を開始する](always-on-vpn-deploy-planning.md)

提供される展開シナリオ以外にも、VPN 接続のセキュリティと可用性を向上させるために、他の高度な VPN 機能を追加することができます。 たとえば、VPN サーバーはこれらの機能を使用して、接続しているクライアントが正常であることを確認してから、接続を許可することができます。

## <a name="high-availability"></a>高可用性

高可用性のための追加オプションを次に示します。

|オプション  |説明  |
|---------|---------|
|サーバーの復元と負荷分散     |高可用性を必要とする環境や、大量の要求をサポートする環境では、ネットワークポリシーサーバー (NPS) を実行している複数のサーバー間で負荷分散を使用し、リモートアクセスサーバーのクラスタリングを有効にすることで、リモートアクセスのパフォーマンスと回復性を向上させることができます。<p>関連ドキュメント:<ul><li>[NPS プロキシサーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[クラスターでのリモート アクセスの展開](../../../ras/cluster/deploy-remote-access-in-cluster.md)</li></ul>        |
|地理的なサイトの復元     |IP ベースの地理位置情報の場合は、Windows Server 2016 の DNS でグローバル Traffic Manager を使用できます。 より堅牢な地理的負荷分散を行うには、Microsoft Azure Traffic Manager などのグローバルサーバー負荷分散ソリューションを使用できます。<p>関連ドキュメント:<ul><li>[Traffic Manager の概要](/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure のトラフィック マネージャー](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>高度な認証

認証に関するその他のオプションを次に示します。

|オプション  |説明  |
|---------|---------|
|Windows Hello for Business     |Windows 10 では、Pc とモバイルデバイスに強力な2要素認証を提供することで、Windows Hello for Business によってパスワードが置き換えられます。 この認証は、デバイスに関連付けられた新しい種類のユーザー資格情報で構成され、生体認証 Id または暗証番号 (PIN) を使用します。<p>Windows 10 VPN クライアントは Windows Hello for Business と互換性があります。 ユーザーがジェスチャを使用してログインすると、VPN 接続は Windows Hello for Business 証明書を使用して証明書ベースの認証を行います。<p>関連ドキュメント:<ul><li>[Windows Hello for Business](/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>技術的なケーススタディ: windows [10 で Windows Hello For Business を使用したリモートアクセスの有効化](/previous-versions//mt728163(v=technet.10))</li></ul>         |
|Azure 多要素認証 (MFA)     |Azure MFA には、Windows VPN 認証メカニズムと統合できるクラウドおよびオンプレミスのバージョンがあります。<p>このメカニズムのしくみの詳細については、「 [Azure Multi-Factor Authentication Server と RADIUS 認証を統合](/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)する」を参照してください。         |

## <a name="advanced-vpn-features"></a>高度な VPN 機能

次に、高度な機能の追加オプションを示します。

|オプション  |説明  |
|---------|---------|
|トラフィックのフィルター処理     |VPN クライアントがアクセスできるアプリケーションを選択する必要がある場合は、VPN トラフィックフィルターを有効にすることができます。<p>詳細については、「 [VPN のセキュリティ機能](/windows/access-protection/vpn/vpn-security-features)」を参照してください。         |
|アプリ トリガー VPN     |特定のアプリケーションまたはアプリケーションの種類が開始されたときに、自動的に接続するように VPN プロファイルを構成することができます。<p>このオプションおよびその他のトリガーオプションの詳細については、「 [VPN 自動トリガープロファイルのオプション](/windows/access-protection/vpn/vpn-auto-trigger-profile)」を参照してください。         |
|VPN 条件付きアクセス   |条件付きアクセスとデバイスコンプライアンスでは、管理対象デバイスが VPN に接続するには、標準に準拠している必要があります。 VPN の条件付きアクセスの高度な機能の1つとして、クライアント認証証明書に**1.3.6.1.4.1.311.87**の "AAD 条件付きアクセス" OID が含まれているもののみに vpn 接続を制限することができます。<p>VPN 接続を制限するには、次の操作を行う必要があります。<ol><li>NPS サーバーで、[**ネットワークポリシーサーバー** ] スナップインを開きます。</li><li>[**ポリシー**] [  >  **ネットワークポリシー**] の順に展開します。</li><li>[**仮想プライベートネットワーク (VPN) 接続**] ネットワークポリシーを右クリックし、[**プロパティ**] を選択します。</li><li>**[設定]** タブを選択します。</li><li>[**ベンダー固有**] を選択し、[**追加**] を選択します。</li><li>[**許可-証明書-OID** ] オプションを選択し、[**追加**] を選択します。</li><li>**1.3.6.1.4.1.311.87**の AAD 条件付きアクセス OID を属性値として貼り付け、[ **OK]** を2回選択します。</li><li>[**閉じる**] を選択し、[**適用**] を選択します。<p>これらの手順を実行した後、有効期間の短いクラウド証明書以外の証明書を使用して VPN クライアントが接続しようとすると、接続は失敗します。</li></ol>条件付きアクセスの詳細については、「 [VPN と条件付きアクセス](/windows/access-protection/vpn/vpn-conditional-access)」を参照してください。   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>失効した証明書を使用している VPN クライアントをブロックする
  
更新プログラムをインストールすると、RRAS サーバーは、デバイストンネル Always on Vpn などの認証に IKEv2 およびコンピューター証明書を使用する Vpn に証明書失効を強制できます。 つまり、このような Vpn では、RRAS サーバーは、失効した証明書を使用しようとしているクライアントへの VPN 接続を拒否できます。

**可用性**

次の表に、Windows の各バージョンの修正プログラムを含むリリースを示します。

|オペレーティング システムのバージョン |Release  |
|---------|---------|
|Windows Server バージョン 1903  |[KB4501375](https://support.microsoft.com/help/4501375/windows-10-update-kb4501375) |
|Windows Server 2019<br />Windows Server、バージョン 1809  |[KB4505658](https://support.microsoft.com/help/4505658/windows-10-update-kb4505658)  |
|Windows Server、バージョン 1803  |[KB4507466](https://support.microsoft.com/help/4507466/windows-10-update-kb4507466)  |
|Windows Server バージョン 1709  |[KB4507465](https://support.microsoft.com/help/4507465/windows-10-update-kb4507465)  |
|Windows Server 2016、バージョン1607  |[KB4503294](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) |

**前提条件の構成方法** 

1. Windows 更新プログラムが利用可能になったときにインストールします。
1. 使用するすべての VPN クライアントおよび RRAS サーバー証明書に CDP エントリがあり、RRAS サーバーがそれぞれの Crl に接続できることを確認します。
1. RRAS サーバーで、 **RootCertificateNameToAccept**パラメーターを構成するには、 **Set vpnauthprotocol** PowerShell コマンドレットを使用します。<p>
   次の例では、これを実行するコマンドを一覧表示します。 この例では、 **CN = Contoso Root 証明機関**は、ルート証明機関の識別名を表します。 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**IKEv2 コンピューター証明書に基づく VPN 接続の証明書失効を強制するように RRAS サーバーを構成する方法**

1. コマンドプロンプトウィンドウで、次のコマンドを実行します。 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. **[ルーティングとリモートアクセス**] サービスを再起動します。
  
これらの VPN 接続の証明書失効を無効にするには、 **certauthflags = 2**を設定するか、 **certauthflags**値を削除してから、**ルーティングとリモートアクセス**サービスを再起動します。 

**IKEv2 コンピューター証明書に基づく VPN 接続の VPN クライアント証明書を失効させる方法**
1. 証明機関から VPN クライアント証明書を失効させます。
1. 証明機関から新しい CRL を発行します。
1. RRAS サーバーで、管理コマンドプロンプトウィンドウを開き、次のコマンドを実行します。
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**IKEv2 コンピューター証明書ベースの VPN 接続の証明書失効が機能していることを確認する方法**  
>[!Note]  
> この手順を使用する前に、必ず CAPI2 operational イベントログを有効にしてください。
1. 前の手順に従って、VPN クライアント証明書を失効させます。
1. 証明書が失効しているクライアントを使用して、VPN への接続を試みます。 RRAS サーバーは接続を拒否し、"IKE 認証資格情報は受け入れられません" などのメッセージを表示します。
1. RRAS サーバーでイベントビューアーを開き、[**アプリケーションとサービスログ**]、[Microsoft]、[Windows]、[CAPI2] の順に移動します。 
1. 次の情報を含むイベントを検索します。
   * ログ名: **CAPI2/operational CAPI2-windows-/operational**
   * イベント ID: **41** 
   * イベントには、 **subject = "*Client fqdn*"** (*クライアント fqdn*は、失効した証明書を持つクライアントの完全修飾ドメイン名を表します) というテキストが含まれています。 

   **<Result>** イベントデータのフィールドには、**証明書が失効**していることが含まれます。 たとえば、イベントから抜粋した次の例を参照してください。
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="https://schemas.microsoft.com/win/2004/08/events/event">
    <UserData>  
     <CertVerifyRevocation>  
      <Certificate fileRef="C97AE73E9823E8179903E81107E089497C77A720.cer" subjectName="client01.corp.contoso.com" />  
      <IssuerCertificate fileRef="34B1AE2BD868FE4F8BFDCA96E47C87C12BC01E3A.cer" subjectName="Contoso Root Certification Authority" />
      ...
      <Result value="80092010">The certificate is revoked.</Result>
     </CertVerifyRevocation>
    </UserData>
   </Event>
   ```

---
## <a name="additional-protection"></a>追加の保護

### <a name="trusted-platform-module-tpm-key-attestation"></a>トラステッドプラットフォームモジュール (TPM) キーの構成証明

TPM 証明キーを持つユーザー証明書により、セキュリティが強化され、エクスポート、ハンマリング、TPM によって提供されるキーの分離によってバックアップされます。

Windows 10 での TPM キーの構成証明の詳細については、「 [Tpm キーの構成証明](../../../../../identity/ad-ds/manage/component-updates/tpm-key-attestation.md)」を参照してください。

## <a name="next-step"></a>次の手順

[ALWAYS ON vpn 展開の計画を開始](always-on-vpn-deploy-planning.md)する: vpn サーバーとして使用する予定のコンピューターにリモートアクセスサーバーの役割をインストールする前に、次のタスクを実行します。 適切な計画を立てたら Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成することができます。  

## <a name="related-topics"></a>関連トピック
- [Nps プロキシサーバーの負荷分散](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): 仮想プライベートネットワーク (VPN) サーバーやワイヤレスアクセスポイントなどのネットワークアクセスサーバーであるリモート認証ダイヤルインユーザーサービス (RADIUS) クライアントは、接続要求を作成し、NPS などの radius サーバーに送信します。 場合によっては、NPS サーバーで一度に受信する接続要求が多すぎると、パフォーマンスが低下したり、過負荷になったりすることがあります。

- [Traffic Manager の概要](/azure/traffic-manager/traffic-manager-overview): このトピックでは、Azure Traffic Manager の概要を説明します。これにより、サービスエンドポイントへのユーザートラフィックの分散を制御できます。 Traffic Manager では、ドメイン ネーム システム (DNS) を使用して、トラフィック ルーティング方法とエンドポイントの正常性に基づいて最適なエンドポイントにクライアント要求を送信します。 

- [Windows Hello For Business](/windows/access-protection/hello-for-business/hello-identity-verification): このトピックでは、クラウドのみのデプロイやハイブリッドデプロイなどの前提条件について説明します。  このトピックでは、Windows Hello for Business に関してよく寄せられる質問の一覧も示します。

- [技術的なケーススタディ: windows 10 で Windows hello For business を使用したリモートアクセスの有効化](/previous-versions//mt728163(v=technet.10)): このテクニカルケーススタディでは、Microsoft が windows Hello for business を使用してリモートアクセスを実装する方法について説明します。  Windows Hello for Business は、組織とコンシューマー向けの、パスワードを超える秘密/公開キーまたは証明書ベースの認証方式です。 この認証方法で使用されるキー ペア資格情報は、パスワードの代わりに使用でき、侵害、盗難、フィッシングに対する耐性があります。 

- [Radius 認証と azure Multi-Factor Authentication Server の統合](/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): このトピックでは、azure MULTI-FACTOR AUTHENTICATION SERVER で radius クライアント認証を追加して構成する手順について説明します。 RADIUS は、認証要求を承認してそれらの要求を処理する標準のプロトコルです。 Azure Multi-Factor Authentication Server は RADIUS サーバーとして機能します。 

- [Vpn のセキュリティ機能](/windows/access-protection/vpn/vpn-security-features): このトピックでは、Vpn のロックダウン、vpn との Windows INFORMATION PROTECTION (WIP) 統合、およびトラフィックフィルターに関する vpn セキュリティガイドラインを示します。 

- [Vpn 自動トリガープロファイルのオプション](/windows/access-protection/vpn/vpn-auto-trigger-profile): このトピックでは、アプリトリガー、名前ベースのトリガー、Always On など、vpn の自動トリガープロファイルのオプションについて説明します。

- [VPN と条件付きアクセス](/windows/access-protection/vpn/vpn-conditional-access): このトピックでは、リモートクライアントのデバイスコンプライアンスオプションを提供する、クラウドベースの条件付きアクセスプラットフォームの概要について説明します。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

- [Tpm キーの構成証明](../../../../../identity/ad-ds/manage/component-updates/tpm-key-attestation.md): このトピックでは、トラステッドプラットフォームモジュール (tpm) の概要と、tpm キーの構成証明を展開する手順について説明します。 また、トラブルシューティングの情報や問題を解決するための手順を確認することもできます。
