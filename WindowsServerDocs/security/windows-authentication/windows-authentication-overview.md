---
title: "Windows 認証の概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 485a0774-0785-457f-a964-0e9403c12bb1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: c2ec55ed6b09628d1d80a24be766259980e84d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="windows-authentication-overview"></a>Windows 認証の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのナビゲーション トピックでは、製品評価、ガイド、手順、設計と展開のガイド、テクニカル リファレンス、およびコマンドの参照を取得するが含まれる Windows 認証およびログオン テクノロジに関するドキュメント リソースを示します。

## <a name="feature-description"></a>機能の説明
認証は、オブジェクト、サービスまたは個人の身元を確認するプロセスです。 オブジェクトを認証する目的は、オブジェクトが正規のものであることを確認します。 サービスまたは利用者を認証する目的は提示された資格情報が本物であることを確認します。

ネットワー キングのコンテキストでは、認証は、ネットワーク アプリケーションまたはリソースに身元を証明する行為です。 通常、身元は公開キーの暗号化、または共有キーと同様のユーザーのみが知っているキーを使用して暗号化操作で実証されています。 認証交換のサーバー側では、認証の試行を検証する既知の暗号化キーで署名されたデータを比較します。

スケーラブルで完成度の高い認証プロセスでは、セキュリティで保護された一元化された場所に暗号化キーを保存すます。 Active Directory ドメイン サービスは、推奨される ID 情報を格納するための既定のテクノロジと \ (ユーザーの credentials\ される暗号化キーを含む)。 Active Directory は、既定の NTLM および Kerberos 実装に必要です。

認証の手法範囲のみユーザーが知っている -、パスワードのようなトークン、公開キー証明書、生体認証などのユーザーが持っているものを使用するより強力なセキュリティ メカニズムに何かに基づいてユーザーを識別する単純なログオンからです。 ビジネス環境において、サービスまたはユーザー可能性があります複数アプリケーションやリソースにアクセスでさまざまな種類のサーバー、1 つまたは複数の場所に配置します。 これらの理由から、認証は、環境の他のプラットフォームと他の Windows オペレーティング システムをサポートする必要があります。

Windows オペレーティング システムが Kerberos、NTLM などの認証プロトコルの既定のセットを実装して、トランスポート層 Security\/secure Sockets Layer \(TLS\/SSL\) と拡張性に優れたアーキテクチャの一部として、ダイジェスト認証です。 さらに、一部のプロトコルは、Negotiate、Credential Security Support Provider などの認証パッケージに統合されています。 これらのプロトコルやパッケージは、ユーザー、コンピューター、およびサービスの認証を有効にします。さらに、有効安全な方法でリソースにアクセスするには、承認されたユーザーとサービスに認証処理します。

詳細については、Windows 認証を含む

-   [Windows 認証の概念](windows-authentication-concepts.md)

-   [Windows ログオンのシナリオ](windows-logon-scenarios.md)

-   [Windows 認証のアーキテクチャ](windows-authentication-architecture.md)

-   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](security-support-provider-interface-architecture.md)

-   [Windows 認証で資格情報の処理](credentials-processes-in-windows-authentication.md)

-   [Windows 認証で使用されるグループ ポリシーの設定](group-policy-settings-used-in-windows-authentication.md)

参照してください、[Windows 認証の技術概要](windows-authentication-technical-overview.md)します。

## <a name="practical-applications"></a>実際の適用
Windows 認証を使用して、別のコンピューターなど、ユーザーまたはコンピューター オブジェクトからかどうかについては、信頼されたソースからものであることを確認します。 Windows では、以下に示すように、この目標を達成する多くのさまざまな方法を提供します。

|宛先。。。|機能|説明|
|----|------|--------|
|Active Directory ドメイン内の認証します。|Kerberos|Microsoft Windows&nbsp;Server オペレーティング システムが Kerberos version 5 認証プロトコルと公開キーの認証拡張機能を実装します。 Kerberos 認証クライアントはセキュリティ サポート プロバイダーとして実装 \(SSP\) され、セキュリティ サポート プロバイダー インターフェイス \(SSPI\) を通じてアクセスできます。 初回ユーザー認証は Winlogon シングル sign\ のアーキテクチャと統合されています。 Kerberos Key Distribution Center \(KDC\) はドメイン コントローラーで実行されているその他の Windows Server セキュリティ サービスと統合されています。 KDC では、そのセキュリティ アカウント データベースとして、ドメインの Active Directory ディレクトリ サービス データベースを使用します。 Active Directory は、既定の Kerberos 実装に必要です。<br /><br />その他のリソースを参照してください。[Kerberos 認証の概要](../kerberos/kerberos-authentication-overview.md)します。|
|Web 上の安全な認証|TLS\/SSL、Schannel セキュリティ サポート プロバイダーに実装されています。|トランスポート層セキュリティ \(TLS\) プロトコル version 1.0、1.1、1.2、Secure Sockets Layer \(SSL\) プロトコルの version 2.0、3.0、データグラム トランスポート層セキュリティ プロトコルの version 1.0、および、プライベート通信トランスポート \(PCT\) プロトコル バージョン 1.0 は、公開キーの暗号化に基づいています。 セキュリティで保護されたチャネル \(Schannel\) プロバイダー認証プロトコル スイートは、これらのプロトコルを提供します。 すべての Schannel プロトコルでは、クライアント/サーバー モデルを使用します。<br /><br />その他のリソースを参照してください。[TLS、SSL & #40 です。Schannel SSP & #41 です。概要](../tls/tls-ssl-schannel-ssp-overview.md)します。|
|Web サービスまたはアプリケーションへの認証します。|統合 Windows 認証<br /><br />ダイジェスト認証|For additional resources, see [Integrated Windows Authentication](https://technet.microsoft.com/library/cc758557(v=WS.10.aspx and [Digest Authentication](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx), and [Advanced Digest Authentication](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx).|
|レガシ アプリケーションへの認証します。|NTLM|NTLM は、認証 challenge\ 応答スタイル認証 protocol.In に加えて、NTLM プロトコル必要に応じて、セッション セキュリティ--具体的には、メッセージの整合性および署名機能およびシーリング機能では、NTLM による機密性します。<br /><br />その他のリソースを参照してください。[NTLM の概要](../kerberos/ntlm-overview.md)します。|
|多要素認証の活用|スマート カードのサポート<br /><br />生体認証のサポート|スマート カードは、クライアント認証、ドメインにログオンしているなどのタスクのセキュリティ ソリューション コード署名、e\ メールのセキュリティ保護を提供するされ tamper\ にくいポータブル方法です。<br /><br />生体認証は、そのユーザーを一意に識別する人物の不変の身体的特徴を測定することに依存しています。 指紋は何百万ものパーソナル コンピューターや周辺機器に埋め込まれている指紋生体認証デバイスでは、最もよく使われる生体認証特性の 1 つです。<br /><br />その他のリソースを参照してください。[スマート カードのテクニカル リファレンス](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)します。 |
|ローカル管理、保管、再利用の資格情報を提供します。|資格情報の管理<br /><br />ローカル セキュリティ機関<br /><br />パスワード|Windows での資格情報の管理により、資格情報を安全に保管します。 セキュリティで保護されたデスクトップの資格情報が収集 \ (ローカルまたはドメイン access\)、用アプリまたは Web サイトを通じて、適切な資格情報は毎回を表示できるように、リソースにアクセスします。<br /><br />
|最新の認証保護によるレガシ システムを拡張します。|認証に対する保護の強化|この機能では、統合 Windows 認証 \(IWA\) を使用してネットワーク接続を認証するときに、保護と資格情報の処理を向上させます。|

## <a name="software-requirements"></a>ソフトウェアの要件
Windows 認証は、Windows オペレーティング システムの以前のバージョンに対応するよう設計されています。 ただし、各リリースでの機能強化では、以前のバージョンに必ずしも適用されません。 詳細については、特定の機能に関するドキュメントを参照してください。

## <a name="server-manager-information"></a>サーバー マネージャー情報
多くの認証機能を構成するには、サーバー マネージャーを使用してインストールできるグループ ポリシーを使用します。 Windows 生体認証フレームワーク機能は、サーバー マネージャーを使用してインストールされます。 サーバー マネージャーを使用しても、Web サーバー \(IIS\) や Active Directory ドメイン サービスなどの認証方法に依存する他のサーバーの役割をインストールできます。

## <a name="related-resources"></a>関連リソース

|認証テクノロジ|リソース|
|----------------|-------|
|Windows 認証|[Windows 認証の技術概要](../windows-authentication/windows-authentication-technical-overview.md)<br />バージョン、全般的な認証の概念、ログオンのシナリオ、サポートされているバージョン、および該当する設定のアーキテクチャ間の違いのトピックが含まれます。|
|Kerberos|[Kerberos 認証の概要](../kerberos/kerberos-authentication-overview.md)<br /><br />[Kerberos の制約付き委任の概要](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Kerberos Authentication Technical Reference](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Kerberos Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet Wiki\)|
|TLS\/SSL および DTLS \ (Schannel セキュリティ サポート プロバイダー)|[TLS、SSL & #40 です。Schannel SSP & #41 です。概要](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Schannel セキュリティ サポート プロバイダーのテクニカル リファレンス](../tls/schannel-security-support-provider-technical-reference.md)|
|ダイジェスト認証|[Digest Authentication Technical Reference](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM の概要](../kerberos/ntlm-overview.md)<br />現在および過去のリソースへのリンクが含まれています|
|PKU2U|[Windows の PKU2U の概要](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|スマート カード|[スマート カードのテクニカル リファレンス](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|資格情報|[資格情報の保護と管理](../credentials-protection-and-management/credentials-protection-and-management.md)<br />現在および過去のリソースへのリンクが含まれています<br /><br />[パスワードの概要](../kerberos/passwords-overview.md)<br />現在および過去のリソースへのリンクが含まれています|


