---
title: OTP 認証を使用するリモート アクセスの展開
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ecb4503c6f8cbc08f2175a33a41929491e4a2b7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811993"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>OTP 認証を使用するリモート アクセスの展開

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

 Windows Server 2016 および Windows Server 2012 が DirectAccess およびルーティングとリモート アクセス サービスを組み合わせて\(RRAS\) VPN は単一のリモート アクセス役割にします。   

## <a name="BKMK_OVER"></a>シナリオの説明  
2 つ使用して DirectAccess クライアント ユーザーを認証するリモート アクセスをこのシナリオで directaccess を有効になっているサーバーが構成されている\-係数のワンタイム パスワード\(OTP\)標準アクティブだけでなく、認証ディレクトリの資格情報。  
  
## <a name="prerequisites"></a>前提条件  
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。  
  
-   [詳細設定を単一の DirectAccess サーバーをデプロイ](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)OTP を展開する前に配置する必要があります。  
  
-   Windows 7 クライアントでは、OTP をサポートするために DCA 2.0 を使用する必要があります。  
  
-   OTP では PIN の変更はサポートされていません。  
  
-   公開キー基盤を展開する必要があります。  
  
    詳しくは、次のトピックをご覧ください。[テスト ラボ ガイド ミニ モジュール:Windows Server 2012 の基本 PKI。](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットの外部でポリシーを変更することはできません。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
OTP 認証シナリオには、いくつかの手順があります。  
  
1.  [高度な設定で単一の DirectAccess サーバーをデプロイ](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。 単一のリモート アクセス サーバーは、OTP を構成する前にデプロイする必要があります。 単一サーバーの計画と展開では、ネットワーク トポロジの設計と構成、証明書の計画と展開、DNS と Active Directory のセットアップ、リモート アクセス サーバーの設定の構成、DirectAccess クライアントの展開、およびイントラネット サーバーの準備を行います。  
  
2.  [OTP 認証を使用したリモート アクセスを計画する](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication)します。 Microsoft 証明機関の計画が OTP だけでなく、単一のサーバーに必要な計画を必要\(CA\) OTP と半径のテンプレートを証明書と\-OTP サーバーを有効にします。 厳密なから特定のユーザーを除外するセキュリティ グループの要件計画も含まれます\(OTP またはスマート カード\)認証します。 マルチ OTP の構成に関する情報の\-フォレストの環境は、「[マルチ フォレスト展開構成](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)します。  
  
3.  [OTP 認証を使用して DirectAccess 構成](/configure/Configure-RA-with-OTP-Authentication.md)します。 さまざまな構成手順、OTP 認証、OTP サーバーを構成して、リモート アクセス サーバーで OTP 設定の構成、DirectAccess クライアント設定の更新のインフラストラクチャの準備などの OTP 展開で構成されます。  
  
4.  [Troubleshoot an OTP Deployment]((/troubleshoot/Troubleshoot-an-OTP-Deployment.md)。 このトラブルシューティングのセクションでは、さまざまな OTP 認証を使用したリモート アクセスを展開するときに発生する最も一般的なエラーについて説明します。  
  
## <a name="BKMK_APP"></a>実際の適用  
OTP 増加のセキュリティを使用して、DirectAccess 展開のセキュリティを強化します。 ユーザーが内部ネットワークにアクセスするには、OTP 資格情報が必要です。 ユーザーは、Windows 10 または Windows 8 クライアント コンピューターで、または DirectAccess Connectivity Assistant を使用して、ネットワーク接続で使用できる職場の接続を使用して OTP 資格情報を提供\(DCA\)を実行しているクライアント コンピューターでWindows 7。 OTP 認証のプロセスは次のとおりです。  
  
1.  DirectAccess クライアントが DirectAccess インフラストラクチャ サーバーへのアクセスにドメインの資格情報を入力\(インフラストラクチャ トンネル経由で\)します。  特定の IKE エラーのために、内部ネットワークへの接続が使用できない場合、クライアント コンピューターの職場の接続では、資格情報が必要なことがユーザーに通知されます。 Windows 7、pop を実行しているクライアント コンピューター\-をスマート カードの資格情報の表示を要求します。  
  
2.  短い要求と共に、リモート アクセス サーバーには SSL 経由で送信は、OTP 資格情報を入力したら\-スマート カード ログオン証明書の用語です。  
  
3.  リモート アクセス サーバー、RADIUS、OTP 資格情報の検証を開始する\-ベースの OTP サーバー。  
  
4.  成功すると、リモート アクセス サーバーは登録機関の証明書を使用して証明書の要求に署名し、DirectAccess クライアント コンピューターに返信します。  
  
5.  DirectAccess クライアント コンピューターが CA に署名証明書要求を転送および Kerberos SSP で使用するための登録済みの証明書を格納\/AP します。  
  
6.  クライアント コンピューターでは、この証明書を使用して、標準のスマート カード Kerberos 認証を透過的に実行します。  
  
## <a name="BKMK_NEW"></a>役割と機能がこのシナリオに含まれる  
次の表に、このシナリオに必要な役割と機能を示します。  
  
|ロール\/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|*リモート アクセス管理の役割*|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 このロールは、両方の DirectAccess 機能 Windows Server 2008 R2、およびルーティングとリモート アクセス サービスの役割サービスで、ネットワーク ポリシーとアクセス サービスを以前にあった\(NPAS\)サーバーロールです。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />1. DirectAccess およびルーティングとリモート アクセス サービス\(RRAS\) VPN DirectAccess と VPN は、リモート アクセス管理コンソールでまとめて管理します。<br />2. RRAS ルーティング RRAS ルーティング機能は、従来のルーティングとリモート アクセス コンソールで管理されます。<br /><br />リモート アクセスの役割は、次のサーバーの機能に依存しています。<br /><br />-インターネット インフォメーション サービス\(IIS\) Web サーバー - この機能は、ネットワーク ロケーション サーバーを構成、OTP 認証の場合、および既定の web プローブを構成するために必要です。<br />-リモート アクセス サーバー上のローカル アカウンティング Windows 内部 Database-Used します。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-は、リモート アクセスの役割がインストールされているし、リモート管理コンソールのユーザー インターフェイスをサポートしているときに、既定でリモート アクセス サーバーにインストールされます。<br />-は、リモート アクセス サーバーの役割が実行されていないサーバーで必要に応じてインストールすることができます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモート アクセス GUI およびコマンド ライン ツール<br />の Windows PowerShell 用リモート アクセス モジュール<br /><br />次の要素と依存関係があります。<br /><br />グループ ポリシー管理コンソール<br />RAS 接続マネージャー管理キット\(CMAK\)<br />-   Windows PowerShell 3.0<br />グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   Windows Server 2016 または Windows Server 2012 のハードウェア要件を満たすコンピューター。  
  
-   シナリオをテストするには、Windows 10、Windows 8、または DirectAccess クライアントとして構成されている Windows 7 を実行している少なくとも 1 つのコンピューターが必要です。  
  
-   RADIUS 経由の PAP をサポートする OTP サーバー。  
  
-   OTP ハードウェアまたはソフトウェア トークン。  
  
## <a name="BKMK_SOFT"></a>ソフトウェアの要件  
このシナリオには、さまざまな要件があります。  
  
1.  単一サーバーの展開のソフトウェア要件。 詳細については、次を参照してください。[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。  
  
2.  1 台のサーバーのソフトウェア要件に加えては、さまざまな OTP\-特定の要件。  
  
    1.  CA 認証での IPsec の IPsec を使用して DirectAccess を展開する必要があります OTP 展開では、CA によって発行された証明書をマシンします。 OTP 展開では、リモート アクセス サーバーを Kerberos プロキシとして使用する IPsec 認証はサポートされていません。 内部 CA が必要です。  
  
    2.  OTP 認証には、Microsoft エンタープライズ CA の CA \(Windows Server 2003 以降を実行している\)OTP クライアント証明書を発行するが必要です。 IPsec 認証用の証明書の発行に使用するのと同じ CA を使用できます。 CA サーバーは、最初のインフラストラクチャ トンネルで使用できる必要があります。  
  
    3.  セキュリティ グループにユーザーを除外強力な認証から、これらのユーザーを含む Active Directory セキュリティ グループが必要です。  
  
    4.  クライアント\-側要件-Windows 10 および Windows 8 クライアント コンピューター、Network Connectivity Assistant \(NCA\)サービスは、OTP 資格情報が必要かどうかを検出するために使用します。 場合は、DirectAccess のメディア マネージャーが資格情報を要求します。  NCA は、オペレーティング システムに含まれ、インストールまたは展開は必要ありません。 Windows 7 クライアント コンピューターで DirectAccess Connectivity Assistant の\(DCA\) 2.0 が必要です。 これは、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=29039)からダウンロードして入手できます。  
  
    5.  次のことを考慮してください。  
  
        1.  スマート カードおよびトラステッド プラットフォーム モジュールと並行して、OTP 認証を使用できます\(TPM\)\-ベースの認証。 リモート アクセス管理コンソールで OTP 認証を有効にすると、スマートカード認証の使用も有効になります。  
  
        2.  時のリモート アクセス構成のユーザーを指定したセキュリティ グループに 2 つから除外できます\-要素認証、およびユーザー名を使用して認証\/パスワードのみです。  
  
        3.  OTP の新しい PIN モードおよび次のトークンコード モードはサポートされません。  
  
        4.  リモート アクセスのマルチサイト展開では、OTP 設定はグローバルで、すべてのエントリ ポイントに対して同一です。 OTP 用に複数の RADIUS サーバーまたは CA サーバーを構成している場合、各リモート アクセス サーバーでは、それらのサーバーを可用性と近さに基づいて並べ替えます。  
  
        5.  リモート アクセス マルチで OTP を構成するときに\-フォレスト環境では、OTP Ca をリソース フォレスト専用にする必要があり、フォレストの信頼間で証明書の登録を構成する必要があります。 詳細については、次を参照してください[AD CS:。Windows Server 2008 R2 のフォレスト間証明書の登録](https://technet.microsoft.com/library/ff955842.aspx)します。  
  
        6.  KEY FOB OTP トークンを使用しているユーザーは PIN の後にトークン コードを挿入する必要があります\(区切り記号なし\)DirectAccess OTP ダイアログ ボックス。 PIN PAD OTP トークンを使用するユーザーは、ダイアログで、トークンコードのみを入力する必要があります。  
  
        7.  WEBDAV が有効な場合は、OTP を有効にしないでください。  
  
## <a name="KnownIssues"></a>既知の問題  
OTP のシナリオを構成する際の既知の問題には、次のようなものがあります。  
  
-   リモート アクセスでは、プローブ メカニズムを使用して、RADIUS への接続確認\-ベースの OTP サーバー。 場合によっては、OTP サーバーでエラーが発生されます。 この問題を回避するには、OTP サーバーで次の手順を実行します。  
  
    -   プローブ方式について、リモート アクセス サーバーで構成されているユーザー名およびパスワードと一致するユーザー アカウントを作成します。 ユーザー名に Active Directory ユーザーを定義しないでください。  
  
        既定では、リモート アクセス サーバーのユーザー名は DAProbeUser 、パスワードは DAProbePass です。 この既定の設定は、リモート アクセス サーバー上のレジストリで、次の値を使用して変更できます。  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\RadiusProbeUser  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\ RadiusProbePass  
  
-   構成済みおよび実行中の DirectAccess の展開にある IPsec ルート証明書を変更すると、OTP が動作を停止します。 Windows PowerShell プロンプトで、各 DirectAccess サーバーでこの問題を解決するには、コマンドを実行します。 `iisreset`  
  
