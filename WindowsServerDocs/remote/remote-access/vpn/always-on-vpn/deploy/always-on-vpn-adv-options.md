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
ms.openlocfilehash: 5f43d64dc7642ef67da03fec989909bc4f2f14ae
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263030"
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


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>失効した証明書を使用して VPN クライアントのブロック
  
更新プログラムをインストールした後、RRAS サーバーは IKEv2 を使用する Vpn の証明書の失効を適用することができ、デバイスなどの認証の証明書をマシン always-on Vpn のトンネリングします。 これは、このような vpn では、RRAS サーバーことができますが拒否される VPN 接続、失効した証明書を使用しようとするクライアントに意味します。

**可用性**

次の表では、Windows のバージョンごとに、修正プログラムのおおよそのリリース日を示します。

|オペレーティング システムのバージョン |リリース日 * |
|---------|---------|
|Windows Server バージョンが 1903  |2019、第 2 四半期  |
|Windows Server 2019<br />Windows Server、バージョン 1809  |2019 年第 3 四半期  |
|Windows Server Version 1803  |2019 年第 3 四半期  |
|Windows Server バージョン 1709  |2019 年第 3 四半期  |
|Windows Server 2016 バージョン 1607  |2019、第 2 四半期  |
  
\* リリースのすべての日付はカレンダー四半期に表示されます。 日付は概算であり予告なく変更可能性があります。

**前提条件を構成する方法** 

1. 利用可能になった Windows 更新プログラムをインストールします。
1. すべての VPN クライアントとを使用する RRAS サーバーの証明書に CDP のエントリがあることと、それぞれの Crl の RRAS サーバーに到達できることを確認してください。
1. 使用して、RRAS サーバーで、**セット VpnAuthProtocol**を構成する PowerShell コマンドレット、 **RootCertificateNameToAccept**パラメーター。<br /><br />
   次の例は、これを行うためのコマンドを一覧表示します。 例では、 **CN = Contoso ルート証明機関**ルート証明機関の識別名を表します。 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority,*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**IKEv2 コンピューター証明書に基づく VPN 接続用の証明書の失効を強制する RRAS サーバーを構成する方法**

1. コマンド プロンプト ウィンドウで、次のコマンドを実行します。 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. 再起動、**ルーティングとリモート アクセス**サービス。
  
これらの VPN 接続の証明書の失効を無効にするには設定**CertAuthFlags = 2**または削除、 **CertAuthFlags**値に設定して、再起動、**ルーティングとリモート アクセス**サービス。 

**IKEv2 コンピューターの証明書に基づく VPN 接続用の VPN クライアント証明書を失効させる方法**
1. 証明機関から VPN クライアント証明書の失効します。
1. 証明機関から新しい CRL を公開します。
1. RRAS サーバーで管理コマンド プロンプト ウィンドウを開くし、次のコマンドを実行します。
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**機能は、IKEv2 マシン証明書ベースの VPN 接続の場合は、その証明書失効を確認する方法**  
>[!Note]  
> この手順を使用する前に、CAPI2 操作イベント ログを有効にすることを確認します。
1. VPN クライアント証明書の失効前の手順に従います。
1. 失効した証明書を持つクライアントを使用して、VPN に接続しようとしてください。 RRAS サーバーの接続を拒否して「IKE 認証資格情報が許容可能です」など、メッセージを表示する必要があります。
1. RRAS サーバーでイベント ビューアーを開きに移動します**アプリケーションとサービス ログ/Microsoft/Windows/CAPI2**します。 
1. 次の情報を持つイベントを検索します。
   * ログ名:**Microsoft Windows の CAPI2/運用 Microsoft Windows の CAPI2/運用**
   * イベントID:**41** 
   * イベントには、次のテキストが含まれています:**サブジェクト ="*クライアント FQDN*"** (*クライアント FQDN*を持つ、失効したクライアントの完全修飾ドメイン名を表します証明書です。) 

   **<Result>** のイベント データ フィールドを含める必要があります **、証明書が失効**します。 たとえば、イベントから次の抜粋を参照してください。
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
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
