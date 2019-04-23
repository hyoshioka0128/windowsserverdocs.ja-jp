---
title: Windows 認証の概要
description: Windows Server のセキュリティ
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
ms.openlocfilehash: 2021ccf1e0015cc910f43966f9400e6bd56a230c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870973"
---
# <a name="windows-authentication-overview"></a>Windows 認証の概要

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT 担当者向けのこのナビゲーション トピックでは、Windows 認証およびログオン テクノロジに関するドキュメント リソースを示します。これには、製品評価、ファースト ステップ ガイド、手順、設計と展開のガイド、テクニカル リファレンス、コマンド リファレンスなどが含まれます。

## <a name="feature-description"></a>機能の説明
認証は、オブジェクト、サービス、または利用者の ID を検証するプロセスです。 オブジェクトを認証する目的は、そのオブジェクトが本物であることを確認することにあります。 サービスまたは利用者を認証する目的は、提示された資格情報が本物であることを確認することにあります。

ネットワーキングのコンテキストでの認証とは、ネットワーク アプリケーションまたはリソースに身元を証明する行為を表します。 通常、identity は、公開キーの暗号化、または共有キーと同様のユーザーのみが知っているキーを使用して暗号化操作によって証明されます。 認証交換のサーバー側は、署名されたデータを既知の暗号化キーと比較して、認証試行を検証します。

暗号化キーを安全な一元的な場所に保管すると、認証プロセスのスケーラビリティと保守性が向上します。 Active Directory Domain Services は、推奨される id 情報を格納するための既定のテクノロジと\(暗号化キー、ユーザーの資格情報を含む\)します。 既定の NTLM および Kerberos 実装には、Active Directory が必要です。

トークン、公開キー証明書のように、ユーザーが持っているものを使用するセキュリティ メカニズムをより強力なパスワードのように、ユーザーのみを認識しているものに基づいてユーザーを識別する、簡易ログオン認証技法の範囲と生体認証。 ビジネス環境のサービスまたはユーザーは、1 つまたは複数の場所に配置された複数の種類のサーバー上の複数のアプリケーションやリソースにアクセスすることがあります。 これらの理由から、認証では、他のプラットフォームや他の Windows オペレーティング システムの環境をサポートする必要があります。

Windows オペレーティング システムが Kerberos、NTLM、トランスポート層セキュリティなどの認証プロトコルの既定のセットを実装する\/Secure Sockets Layer \(TLS\/SSL\)、およびダイジェスト認証の一部として、拡張可能なアーキテクチャ。 加えて、いくつかのプロトコルは、Negotiate、Credential Security Support Provider などの認証パッケージに統合されています。 これらのプロトコルやパッケージによって、ユーザー、コンピューター、サービスの認証が可能になります。また、認証処理によって、承認されたユーザーとサービスが安全な方法でリソースにアクセスできるようになります。

Windows 認証の詳細には、次の内容も含まれます。

-   [Windows 認証の概念](windows-authentication-concepts.md)

-   [Windows ログオンのシナリオ](windows-logon-scenarios.md)

-   [Windows 認証のアーキテクチャ](windows-authentication-architecture.md)

-   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](security-support-provider-interface-architecture.md)

-   [Windows 認証で資格情報の処理](credentials-processes-in-windows-authentication.md)

-   [Windows 認証で使用されるグループ ポリシーの設定](group-policy-settings-used-in-windows-authentication.md)

参照してください、 [Windows 認証の技術概要](windows-authentication-technical-overview.md)します。

## <a name="practical-applications"></a>実際の適用例
Windows 認証は、情報が信頼できるソース (人や別のコンピューターなどのコンピューター オブジェクト) から送信されていることを確認するために使用します。 Windows には、この操作を行うためのさまざまな方法が用意されています。次の表に、これらの方法について説明します。

|宛先...|機能|説明|
|----|------|--------|
|Active Directory ドメイン内の認証|Kerberos|Microsoft Windows&nbsp;サーバー オペレーティング システムは、Kerberos version 5 認証プロトコルと公開キー認証の拡張機能を実装します。 Kerberos 認証クライアントは、セキュリティ サポート プロバイダーとして実装\(SSP\)セキュリティ サポート プロバイダー インターフェイスを介してアクセスできると\(SSPI\)します。 初期のユーザー認証は Winlogon シングル サインオンと統合\-アーキテクチャ。 Kerberos キー配布センター \(KDC\)はドメイン コント ローラーで実行されているその他の Windows Server セキュリティ サービスと統合します。 KDC では、そのセキュリティ アカウント データベースとして、ドメインの Active Directory ディレクトリ サービス データベースを使用します。 既定の Kerberos 実装には、Active Directory が必要です。<br /><br />その他のリソースについては、「[Kerberos 認証の概要](../kerberos/kerberos-authentication-overview.md)」を参照してください。|
|Web 上のセキュリティで保護された認証|TLS\/SSL、Schannel セキュリティ サポート プロバイダーに実装されています。|トランスポート層セキュリティ\(TLS\)プロトコルの version 1.0、1.1、1.2、Secure Sockets Layer \(SSL\)プロトコル、version 2.0、3.0、データグラム トランスポート層セキュリティ プロトコル バージョン 1.0、およびプライベート通信トランスポート\(PCT\) protocol、version 1.0 では公開キーの暗号化に基づきます。 セキュリティで保護されたチャネル\(Schannel\)プロバイダー認証プロトコル スイートは、これらのプロトコルを提供します。 すべての Schannel プロトコルでは、クライアント/サーバー モデルが使用されています。<br /><br />その他のリソースを参照してください。 [TLS、SSL &#40;Schannel SSP&#41;概要](../tls/tls-ssl-schannel-ssp-overview.md)します。|
|Web サービスまたはアプリケーションの認証|統合 Windows 認証<br /><br />ダイジェスト認証|その他のリソースを参照してください。[統合 Windows 認証](https://technet.microsoft.com/library/cc758557(v=WS.10).aspx)と[ダイジェスト認証](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx)、および[高度なダイジェスト認証](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx)します。|
|レガシ アプリケーションの認証|NTLM|NTLM は、チャレンジ\-応答スタイルの認証プロトコルです。認証に加えて NTLM プロトコルは、必要に応じてセッション セキュリティ具体的には、メッセージの整合性と機密性署名およびシール NTLM で関数を提供します。<br /><br />その他のリソースについては、「[NTLM の概要](../kerberos/ntlm-overview.md)」を参照してください。|
|多要素認証の利用|スマート カードのサポート<br /><br />生体認証のサポート|スマート カードは、改ざん\-クライアント認証、ドメインにログオンしているなどのタスクのセキュリティ ソリューションを提供する方法をされにくいポータブル コード署名、電子メールをセキュリティで保護する\-メール。<br /><br />生体認証は、一人一人異なる不変の身体的特徴を測定することによって個人を特定します。 生体認証に最も多く使われている身体的特徴の 1 つは指紋です。指紋を使って生体認証を行う数え切れないほどのデバイスが、パーソナル コンピューターや周辺機器に組み込まれています。<br /><br />その他のリソースを参照してください。[スマート カードのテクニカル リファレンス](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)します。 |
|資格情報のローカル管理、保管、再利用|資格情報の管理<br /><br />ローカル セキュリティ機関<br /><br />パスワード|Windows の資格情報管理を使うと、資格情報を安全に保管できます。 セキュリティで保護されたデスクトップの資格情報が収集\(ローカルまたはドメインのアクセスの\)、アプリまたは web サイトを通じて、リソースにアクセスするたびに、正しい資格情報が表示されるようにします。<br /><br />
|最新の認証保護によるレガシ システムの強化|認証の拡張保護 (Extended Protection for Authentication)|統合 Windows 認証を使用してネットワーク接続を認証するときに、保護と資格情報の処理をこの機能が強化\(IWA\)します。|

## <a name="software-requirements"></a>ソフトウェア要件
Windows 認証は、Windows オペレーティング システムの以前のバージョンとの互換性があるように設計されています。 ただし、各リリースでの改良が必ずしも以前のバージョンに適用されるとは限りません。 詳細については、特定の機能のドキュメントを参照してください。

## <a name="server-manager-information"></a>サーバー マネージャー情報
グループ ポリシーを使用して、多くの認証機能を構成できます。グループ ポリシーは、サーバー マネージャーを使用してインストールできます。 Windows 生体認証フレームワーク機能をインストールするには、サーバー マネージャーを使用します。 Web サーバーなど、認証方法に依存するその他のサーバーの役割\(IIS\) Active Directory Domain Services は、サーバー マネージャーを使用してインストールすることもできます。

## <a name="related-resources"></a>関連リソース

|認証テクノロジ|参考資料|
|----------------|-------|
|Windows 認証|[Windows 認証の技術概要](../windows-authentication/windows-authentication-technical-overview.md)<br />トピックでは、バージョン、一般的な認証の概念、ログオンのシナリオ、サポートされているバージョンは、および適用可能な設定のアーキテクチャの違いをアドレス指定します。|
|Kerberos|[Kerberos 認証の概要](../kerberos/kerberos-authentication-overview.md)<br /><br />[Kerberos の制約付き委任の概要](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Kerberos 認証のテクニカル リファレンス](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Kerberos のサバイバル ガイド](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet Wiki\)|
|TLS\/SSL および DTLS \(Schannel セキュリティ サポート プロバイダー\)|[TLS、SSL &#40;Schannel SSP&#41;の概要](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Schannel セキュリティ サポート プロバイダーのテクニカル リファレンス](../tls/schannel-security-support-provider-technical-reference.md)|
|ダイジェスト認証|[ダイジェスト認証のテクニカル リファレンス](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM の概要](../kerberos/ntlm-overview.md)<br />現在と過去のリソースへのリンクが含まれています|
|PKU2U|[Windows の PKU2U の概要](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|スマート カード|[スマート カードのテクニカル リファレンス](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|資格情報|[資格情報の保護と管理](../credentials-protection-and-management/credentials-protection-and-management.md)<br />現在と過去のリソースへのリンクが含まれています<br /><br />[パスワードの概要](../kerberos/passwords-overview.md)<br />現在と過去のリソースへのリンクが含まれています|


