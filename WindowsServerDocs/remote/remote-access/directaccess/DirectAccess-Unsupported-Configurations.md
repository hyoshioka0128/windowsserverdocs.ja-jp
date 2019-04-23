---
title: DirectAccess には、構成がサポートされていません
description: このトピックでは、Windows Server 2016 でサポートされていない DirectAccess の構成の一覧を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49fa86883e6a590ac8f7dcf0c724f87af419f88e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828853"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess には、構成がサポートされていません

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

もう一度配置を開始することを回避するために、デプロイを開始する前に、次のサポートされていない DirectAccess の構成の一覧を確認します。  

## <a name="bkmk_frs"></a>グループ ポリシー オブジェクト (SYSVOL レプリケーション) のファイル レプリケーション サービス (FRS) の配布  
ドメイン コント ローラーに配布するためのグループ ポリシー オブジェクト (SYSVOL レプリケーション) ファイル レプリケーション サービス (FRS) が実行されている環境で DirectAccess を展開しないでください。 FRS. を使用すると、DirectAccess の展開がサポートされていません  
  
Windows Server 2003 または Windows Server 2003 R2 を実行しているドメイン コント ローラーがある場合は、FRS を使用しています。 さらを使用している FRS Windows 2000 Server または Windows Server 2003 ドメイン コント ローラーを以前使用していて決してから移行した SYSVOL レプリケーション FRS 分散ファイル システム レプリケーション (DFS-R) にします。  
  
FRS SYSVOL レプリケーションで DirectAccess を展開する場合、意図しない削除 DirectAccess グループ ポリシーのリスクは、DirectAccess サーバーとクライアントの構成情報が含まれているオブジェクトします。 これらのオブジェクトが削除された場合は、DirectAccess の展開には、障害発生が低下し、DirectAccess を使用するクライアント コンピューターでは、ネットワークに接続できません。  
  
DirectAccess を展開する場合は、Windows Server 2003 R2 より新しいオペレーティング システムを実行するドメイン コント ローラーを使用する必要があり。、DFS-R: を使用する必要があります。  
  
FRS から DFS R への移行方法の詳細については、次を参照してください。、 [SYSVOL レプリケーション移行ガイド。FRS DFS レプリケーションから](https://technet.microsoft.com/library/dd640019(v=ws.10).aspx)します。  
  
## <a name="bkmk_nap"></a>DirectAccess クライアントのネットワーク アクセス保護  
ネットワーク アクセス保護 (NAP) を使用して、リモート クライアント コンピューターが企業ネットワークへのアクセスが許可されるまでに、IT ポリシーを満たすかどうかを決定します。 NAP は、Windows Server 2012 R2 で非推奨とされ、は、Windows Server 2016 では含まれていません。 このため、NAP と DirectAccess の新しい展開を開始することはお勧めしません。 DirectAccess クライアントのセキュリティの終了点のコントロールの別の方法をお勧めします。  
  
## <a name="bkmk_multi"></a>Windows 7 クライアントのマルチサイトのサポート  
Windows 10、マルチサイト展開で DirectAccess を構成するとき&reg;、Windows&reg; 8.1、および Windows&reg; 8 のクライアントに最も近いサイトに接続する機能があります。  Windows 7&reg;クライアント コンピューターと同じ機能がありません。 Windows 7 クライアントのサイトの選択は、ポリシーの構成時に特定のサイトに設定し、これらのクライアントは常にその場所に関係なく、指定されたサイトに接続します。  
  
## <a name="bkmk_user"></a>ユーザーに基づくアクセス制御  
DirectAccess ポリシーは、コンピューター、ユーザー ベースではなくです。 企業ネットワークへのアクセスを制御する DirectAccess ユーザー ポリシーを指定することはサポートされていません。  
  
## <a name="bkmk_policy"></a>DirectAccess ポリシーをカスタマイズします。  
DirectAccess のセットアップ ウィザードで、リモート アクセス管理コンソールまたはリモート アクセスの Windows PowerShell コマンドレットを使用して DirectAccess を構成できます。 DirectAccess のセットアップ ウィザード以外の方法を使用して、DirectAccess グループ ポリシー オブジェクトを直接変更することや、サーバーまたはクライアントの既定のポリシー設定を手動で変更するなど、DirectAccess を構成することはサポートされていません。 これらの変更の構成を使用できなくなる可能性があります。  
  
## <a name="bkmk_kerb"></a>KerbProxy 認証  
作業の開始ウィザードで DirectAccess サーバーを構成するときに、DirectAccess サーバーは自動的にコンピューターの KerbProxy 認証とユーザー認証を使用する構成します。 このため、する必要がありますのみを使用して、作業の開始ウィザードの単一サイト展開のみ Windows 10&reg;、Windows 8.1、または Windows 8 クライアントをデプロイします。  
  
さらに、次の機能は、いない KerbProxy 認証で使用する必要があります。  
  
-   によって外部ロード バランサーまたは Windows ロードのいずれかを使用して負荷分散   
    バランサー  
  
-   スマート カードやワンタイム パスワード (OTP) が必要な 2 要素認証  
  
KerbProxy 認証を有効にした場合は、次の展開の計画はサポートされていません。  
  
-   マルチサイトします。  
  
-   DirectAccess は、Windows 7 クライアントをサポートします。  
  
-   強制トンネリングします。 強制トンネリングを使用すると、KerbProxy 認証が無効になっていることを確認するには、ウィザードの実行中に、次の項目を構成します。  
  
    -   強制トンネリングを有効にします。  
  
    -   Windows 7 の DirectAccess クライアントを有効にします。  
  
> [!NOTE]  
> 以前のデプロイでは、高度な構成ウィザードの 2 つのトンネルの構成を使用して、証明書ベースのコンピューターとユーザー認証を使用したを使用する必要があります。 詳細については、次を参照してください。[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。  
  
## <a name="bkmk_isa"></a>ISATAP を使用します。  
ISATAP とは、IPv4 専用の企業ネットワークで IPv6 接続を提供する移行テクノロジです。 単一の DirectAccess サーバー展開での小規模および中規模の組織に限定し、DirectAccess クライアントのリモート管理できます。 ISATAP が deployedin multisite、負荷分散、またはマルチ ドメイン環境の場合は、削除するか、DirectAccess を構成する前に、ネイティブ IPv6 の展開に移動する必要があります。  
  
## <a name="bkmk_iphttps"></a>IPHTTPS とワンタイム パスワード (OTP) エンドポイントの構成  
IPHTTPS を使用して、IPHTTPS 接続をロード バランサーなど、他の任意のデバイスではなく、DirectAccess サーバーで終了する必要があります。 同様に、ワンタイム パスワード (OTP) 認証中に作成された帯域外の Secure Sockets Layer (SSL) 接続は、DirectAccess サーバーで終了する必要があります。 これらの接続のエンドポイント間のすべてのデバイスは、パススルー モードで構成する必要があります。  
  
## <a name="bkmk_ft"></a>OTP 認証を使用した強制トンネリング  
OTP と強制トンネリングで 2 要素認証を使用した DirectAccess サーバーを展開しないと、OTP 認証は失敗します。 帯域外の Secure Sockets Layer (SSL) 接続が DirectAccess サーバーと DirectAccess クライアントの間に必要です。 この接続には、DirectAccess トンネルの外部トラフィックを送信する除外が必要です。 強制トンネル構成では、すべてのトラフィックは、DirectAccess トンネルを通過する必要があるされ、トンネルが確立されると適用除外は許可されません。 このために、OTP 認証を強制トンネル構成であることはできません。  
  
## <a name="bkmk_rodc"></a>読み取り専用ドメイン コント ローラーと DirectAccess を展開します。  
DirectAccess サーバーは、読み取り/書き込みドメイン コント ローラーへのアクセスが必要し、正しくの読み取り専用ドメイン コント ローラー (RODC) では機能しています。  
  
読み取り/書き込みドメイン コント ローラーは、次を含む、さまざまな理由が必要です。  
  
-   DirectAccess サーバーでリモート アクセス Microsoft 管理コンソール (MMC) を開く、読み取り/書き込みドメイン コント ローラーが必要です。  
  
-   DirectAccess サーバーする必要があります読み取りおよび書き込み DirectAccess クライアントと DirectAccess サーバーのグループ ポリシー オブジェクト (Gpo) にします。  
  
-   DirectAccess サーバーを読み取って、プライマリ ドメイン コント ローラー エミュレーター (PDCe) から具体的には、クライアント GPO に書き込みます。  
  
これらの要件により、RODC で DirectAccess を展開しません。  
  


