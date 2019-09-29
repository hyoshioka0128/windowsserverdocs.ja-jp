---
title: OTP 認証を使用するリモート アクセスの展開
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d0de5f459e31e1dfac40e49cd6cc83de8722df4d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404429"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>OTP 認証を使用するリモート アクセスの展開

>適用先:Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016 と Windows Server 2012 では、DirectAccess とルーティングとリモートアクセスサービス \(RRAS @ no__t VPN が1つのリモートアクセスの役割に結合されます。   

## <a name="BKMK_OVER"></a>シナリオの説明  
このシナリオでは、DirectAccess が有効になっているリモートアクセスサーバーが、標準 Active Directory の資格情報に加えて、@ no__t-0factor の1回限りのパスワード \(OTP @ no__t 認証を持つ DirectAccess クライアントユーザーを認証するように構成されています。  
  
## <a name="prerequisites"></a>前提条件  
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。  
  
-   OTP を展開する前に[、詳細設定を使用して単一の DirectAccess サーバーを](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)展開する必要があります。  
  
-   Windows 7 クライアントでは、OTP をサポートするために DCA 2.0 を使用する必要があります。  
  
-   OTP では PIN の変更はサポートされていません。  
  
-   公開キー基盤を展開する必要があります。  
  
    詳しくは、次のトピックをご覧ください。[Test Lab Guide ミニモジュール:Windows Server 2012 の基本 PKI。 ](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットの外部でのポリシーの変更はサポートされていません。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
OTP 認証シナリオには、いくつかの手順があります。  
  
1.  [詳細設定を使用して単一の DirectAccess サーバーを展開](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。 OTP を構成する前に、単一のリモートアクセスサーバーを展開する必要があります。 単一サーバーの計画と展開では、ネットワーク トポロジの設計と構成、証明書の計画と展開、DNS と Active Directory のセットアップ、リモート アクセス サーバーの設定の構成、DirectAccess クライアントの展開、およびイントラネット サーバーの準備を行います。  
  
2.  [OTP 認証を使用してリモートアクセスを計画](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication)します。 OTP では、1台のサーバーに必要な計画に加えて、Microsoft の証明機関 @no__t 0CA @ no__t と OTP 用の証明書テンプレートを計画する必要があります。RADIUS @ no__t-2enabled OTP サーバー。 また、強力な @no__t 0OTP またはスマートカード @ no__t 認証から特定のユーザーを除外するためのセキュリティグループの要件が含まれる場合もあります。 複数の @ no__t-0forest 環境における OTP の構成の詳細については、「[マルチフォレスト展開の構成](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)」を参照してください。  
  
3.  [OTP 認証を使用して DirectAccess を構成](/configure/Configure-RA-with-OTP-Authentication.md)します。 OTP の展開は、OTP 認証用のインフラストラクチャの準備、OTP サーバーの構成、リモートアクセスサーバーでの OTP 設定の構成、DirectAccess クライアントの設定の更新など、さまざまな構成手順で構成されています。  
  
4.  [OTP 展開のトラブルシューティング]((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). このトラブルシューティングのセクションでは、OTP 認証を使用してリモートアクセスを展開するときに発生する可能性のある最も一般的なエラーについて説明します。  
  
## <a name="BKMK_APP"></a>実用的なアプリケーション  
セキュリティを強化する-OTP を使用すると、DirectAccess 展開のセキュリティが向上します。 ユーザーが内部ネットワークにアクセスするには、OTP 資格情報が必要です。 ユーザーは、Windows 10 または Windows 8 クライアントコンピューターのネットワーク接続で使用できる職場の接続を介して、または Windows 7 を実行しているクライアントコンピューターで DirectAccess Connectivity Assistant \(DCA @ no__t を使用して、OTP 資格情報を提供します。 OTP 認証のプロセスは次のとおりです。  
  
1.  DirectAccess クライアントは、ドメインの資格情報を入力して、インフラストラクチャトンネル @ no__t 経由で、\(over DirectAccess インフラストラクチャサーバーにアクセスします。  特定の IKE エラーのために、内部ネットワークへの接続が使用できない場合、クライアント コンピューターの職場の接続では、資格情報が必要なことがユーザーに通知されます。 Windows 7 を実行しているクライアントコンピューターでは、スマートカードの資格情報を要求する pop @ no__t-0up が表示されます。  
  
2.  OTP 資格情報が入力されると、SSL を介してリモートアクセスサーバーに送信され、短い @ no__t-0term スマートカードログオン証明書の要求と共に送信されます。  
  
3.  リモートアクセスサーバーは、RADIUS @ no__t ベースの OTP サーバーを使用して OTP 資格情報の検証を開始します。  
  
4.  成功すると、リモート アクセス サーバーは登録機関の証明書を使用して証明書の要求に署名し、DirectAccess クライアント コンピューターに返信します。  
  
5.  DirectAccess クライアントコンピューターは、署名された証明書要求を CA に転送し、Kerberos SSP @ no__t-0AP で使用するために、登録された証明書を格納します。  
  
6.  クライアント コンピューターでは、この証明書を使用して、標準のスマート カード Kerberos 認証を透過的に実行します。  
  
## <a name="BKMK_NEW"></a>このシナリオに含まれる役割と機能  
次の表に、このシナリオに必要な役割と機能を示します。  
  
|Role @ no__t 機能|このシナリオのサポート方法|  
|---------|-----------------|  
|*リモートアクセス管理の役割*|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワークポリシーとアクセスサービス @no__t 0NPAS @ no__t サーバーロールの役割サービスであったルーティングとリモートアクセスサービスの両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />1. DirectAccess およびルーティングとリモートアクセスサービス \(RRAS @ no__t-1 VPN-DirectAccess と VPN は、リモートアクセス管理コンソールで一緒に管理されます。<br />2. RRAS ルーティング-RRAS ルーティング機能は、従来のルーティングとリモートアクセスコンソールで管理されます。<br /><br />リモート アクセスの役割は、次のサーバーの機能に依存しています。<br /><br />-インターネットインフォメーションサービス \(IIS @ no__t Web Server-この機能は、ネットワークロケーションサーバーを構成し、OTP 認証を利用し、既定の web プローブを構成するために必要です。<br />-Windows Internal Database-リモートアクセスサーバーのローカルアカウンティングに使用されます。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-リモートアクセスの役割をインストールするときに、リモートアクセスサーバーに既定でインストールされ、リモート管理コンソールのユーザーインターフェイスをサポートします。<br />-必要に応じて、リモートアクセスサーバーの役割を実行していないサーバーにインストールできます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモートアクセス GUI およびコマンドラインツール<br />-Windows PowerShell 用リモートアクセスモジュール<br /><br />次の要素と依存関係があります。<br /><br />-グループポリシー管理コンソール<br />-RAS 接続マネージャー管理キット \(CMAK @ no__t<br />-Windows PowerShell 3.0<br />-グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   Windows Server 2016 または Windows Server 2012 のハードウェア要件を満たしているコンピューター。  
  
-   このシナリオをテストするには、DirectAccess クライアントとして構成されている Windows 10、Windows 8、または Windows 7 を実行しているコンピューターが少なくとも1台は必要です。  
  
-   RADIUS 経由の PAP をサポートする OTP サーバー。  
  
-   OTP ハードウェアまたはソフトウェア トークン。  
  
## <a name="BKMK_SOFT"></a>ソフトウェア要件  
このシナリオには、さまざまな要件があります。  
  
1.  単一サーバーの展開のソフトウェア要件。 詳細については、「[単一の DirectAccess サーバーを拡張設定で展開する](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」を参照してください。  
  
2.  単一サーバーのソフトウェア要件に加えて、OTP @ no__t 固有の要件がいくつかあります。  
  
    1.  IPsec 認証用の CA-OTP 展開では、CA によって発行された IPsec コンピューター証明書を使用して DirectAccess を展開する必要があります。 OTP 展開では、リモート アクセス サーバーを Kerberos プロキシとして使用する IPsec 認証はサポートされていません。 内部 CA が必要です。  
  
    2.  OTP 認証用の CA-OTP クライアント証明書を発行するには、Windows 2003 Server 以降の @ no__t で実行されている Microsoft エンタープライズ CA \(running 必要です。 IPsec 認証用の証明書の発行に使用するのと同じ CA を使用できます。 CA サーバーは、最初のインフラストラクチャ トンネルで使用できる必要があります。  
  
    3.  セキュリティグループ-強力な認証からユーザーを除外するには、これらのユーザーを含む Active Directory セキュリティグループが必要です。  
  
    4.  クライアントの @ no__t-0side 要件-Windows 10 および Windows 8 クライアントコンピューターの場合、ネットワーク接続アシスタント \(NCA @ no__t サービスを使用して、OTP 資格情報が必要かどうかを検出します。 そのような場合は、DirectAccess メディアマネージャーによって資格情報の入力が求められます。  NCA はオペレーティングシステムに含まれており、インストールや展開は必要ありません。 Windows 7 クライアントコンピューターの場合、DirectAccess Connectivity Assistant \(DCA @ no__t-1 2.0 が必要です。 これは、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=29039)からダウンロードして入手できます。  
  
    5.  次のことを考慮してください。  
  
        1.  OTP 認証は、スマートカードおよびトラステッドプラットフォームモジュール \(TPM @ no__t @ no__t ベースの認証と並行して使用できます。 リモート アクセス管理コンソールで OTP 認証を有効にすると、スマートカード認証の使用も有効になります。  
  
        2.  リモートアクセスの構成中に、指定されたセキュリティグループのユーザーは、2つの @ no__t-0factor 認証から除外することができます。そのため、username @ no__t-1 password only を使用して認証を行います。  
  
        3.  OTP の新しい PIN モードおよび次のトークンコード モードはサポートされません。  
  
        4.  リモート アクセスのマルチサイト展開では、OTP 設定はグローバルで、すべてのエントリ ポイントに対して同一です。 OTP 用に複数の RADIUS サーバーまたは CA サーバーを構成している場合、各リモート アクセス サーバーでは、それらのサーバーを可用性と近さに基づいて並べ替えます。  
  
        5.  リモートアクセスのマルチ @ no__t-0forest 環境で OTP を構成する場合、OTP Ca はリソースフォレストのみからのものである必要があり、証明書の登録はフォレストの信頼間で構成する必要があります。 詳細については、「[AD CS:Windows Server 2008 R2 を使用したフォレスト間証明書の登録 @ no__t-0  
  
        6.  キーの FOB OTP トークンを使用するユーザーは、DirectAccess OTP ダイアログに区切り文字 @ no__t を付けずに、PIN の後に @no__t トークンコードを挿入する必要があります。 PIN PAD OTP トークンを使用するユーザーは、ダイアログで、トークンコードのみを入力する必要があります。  
  
        7.  WEBDAV が有効な場合は、OTP を有効にしないでください。  
  
## <a name="KnownIssues"></a>既知の問題  
OTP のシナリオを構成する際の既知の問題には、次のようなものがあります。  
  
-   リモートアクセスでは、プローブメカニズムを使用して、RADIUS @ no__t ベースの OTP サーバーへの接続を確認します。 場合によっては、OTP サーバーでエラーが発生されます。 この問題を回避するには、OTP サーバーで次の手順を実行します。  
  
    -   プローブ方式について、リモート アクセス サーバーで構成されているユーザー名およびパスワードと一致するユーザー アカウントを作成します。 ユーザー名に Active Directory ユーザーを定義しないでください。  
  
        既定では、リモート アクセス サーバーのユーザー名は DAProbeUser 、パスワードは DAProbePass です。 この既定の設定は、リモート アクセス サーバー上のレジストリで、次の値を使用して変更できます。  
  
        -   HKEY @ no__t-0LOCAL @ no__t-1MACHINE @ no__t-2SOFTWARE @ no__t-3Microsoft @ no__t-4DirectAccess @ no__t-5OTP @ no__t-6RadiusProbeUser  
  
        -   HKEY @ no__t-0LOCAL @ no__t-1MACHINE @ no__t-2SOFTWARE @ no__t-3Microsoft @ no__t-4DirectAccess @ no__t-5OTP @ no__t-6 RadiusProbePass  
  
-   構成済みおよび実行中の DirectAccess の展開にある IPsec ルート証明書を変更すると、OTP が動作を停止します。 この問題を解決するには、各 DirectAccess サーバーで、Windows PowerShell プロンプトで次のコマンドを実行します。 `iisreset`  
  
