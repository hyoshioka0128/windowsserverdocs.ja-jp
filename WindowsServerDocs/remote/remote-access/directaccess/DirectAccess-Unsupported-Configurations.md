---
title: DirectAccess には、構成がサポートされていません
description: このトピックでは、Windows Server 2016 でサポートされていない DirectAccess 構成の一覧を示します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e652083d4accf90b542a16d51e314299303954f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388841"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess には、構成がサポートされていません

>適用先:Windows Server (半期チャネル)、Windows Server 2016

展開を開始する前に、次のサポートされていない DirectAccess 構成の一覧を確認して、展開を再度開始する必要がないようにしてください。  

## <a name="bkmk_frs"></a>グループポリシーオブジェクトのファイルレプリケーションサービス (FRS) 配布 (SYSVOL レプリケーション)  
ドメインコントローラーがグループポリシーオブジェクト (SYSVOL レプリケーション) を配布するためにファイルレプリケーションサービス (FRS) を実行している環境では、DirectAccess を展開しないでください。 FRS を使用する場合、DirectAccess の展開はサポートされません。  
  
Windows Server 2003 または Windows Server 2003 R2 を実行しているドメインコントローラーがある場合は、FRS を使用します。 また、以前に Windows 2000 Server または Windows Server 2003 のドメインコントローラーを使用していて、FRS から分散ファイルシステムレプリケーション (DFS-R) に SYSVOL レプリケーションを移行したことがない場合は、FRS を使用している可能性があります。  
  
FRS SYSVOL レプリケーションを使用して DirectAccess を展開する場合、directaccess サーバーとクライアントの構成情報を含む DirectAccess グループポリシーオブジェクトを誤って削除する危険性があります。 これらのオブジェクトが削除されると、DirectAccess の展開が停止し、DirectAccess を使用するクライアントコンピューターがネットワークに接続できなくなります。  
  
DirectAccess の展開を計画している場合は、Windows Server 2003 R2 以降のオペレーティングシステムを実行しているドメインコントローラーを使用する必要があります。また、DFS-R を使用する必要があります。  
  
FRS から DFS-R への移行の詳細については、[SYSVOL レプリケーション移行ガイドを参照してください。FRS を DFS レプリケーション](https://technet.microsoft.com/library/dd640019(v=ws.10).aspx)します。  
  
## <a name="bkmk_nap"></a>DirectAccess クライアントのネットワークアクセス保護  
ネットワークアクセス保護 (NAP) を使用して、企業ネットワークへのアクセスが許可される前に、リモートクライアントコンピューターが IT ポリシーを満たしているかどうかを判断します。 NAP は Windows Server 2012 R2 で非推奨とされており、Windows Server 2016 には含まれていません。 このため、NAP を使用した DirectAccess の新しい展開を開始することはお勧めしません。 DirectAccess クライアントのセキュリティをエンドポイントで制御する別の方法をお勧めします。  
  
## <a name="bkmk_multi"></a>Windows 7 クライアントのマルチサイトサポート  
DirectAccess がマルチサイト展開で構成されている場合、Windows 10 @ no__t-0、Windows @ no__t 8.1、および Windows @ no__t 8 クライアントは、最も近いサイトに接続することができます。  Windows 7 @ no__t クライアントコンピューターには、同じ機能がありません。 Windows 7 クライアントのサイト選択は、ポリシーの構成時に特定のサイトに設定されます。これらのクライアントは、場所に関係なく、常に指定されたサイトに接続します。  
  
## <a name="bkmk_user"></a>ユーザーベースのアクセス制御  
DirectAccess ポリシーは、ユーザーベースではなく、コンピューターベースです。 企業ネットワークへのアクセスを制御する DirectAccess ユーザーポリシーを指定することはサポートされていません。  
  
## <a name="bkmk_policy"></a>DirectAccess ポリシーのカスタマイズ  
Directaccess は、DirectAccess セットアップウィザード、リモートアクセス管理コンソール、またはリモートアクセス Windows PowerShell コマンドレットを使用して構成できます。 Directaccess セットアップウィザード以外の任意の方法を使用して directaccess を構成する (DirectAccess グループポリシーオブジェクトを直接変更する、サーバーまたはクライアントの既定のポリシー設定を手動で変更するなど) ことはサポートされていません。 これらの変更により、構成が使用できなくなる可能性があります。  
  
## <a name="bkmk_kerb"></a>KerbProxy 認証  
はじめにウィザードを使用して DirectAccess サーバーを構成すると、コンピューターとユーザーの認証に KerbProxy 認証を使用するように DirectAccess サーバーが自動的に構成されます。 このため、はじめにウィザードは、Windows 10 の @ no__t-0、Windows 8.1、または Windows 8 クライアントのみが展開されている単一サイトの展開にのみ使用してください。  
  
また、次の機能は、KerbProxy 認証では使用しないでください。  
  
-   外部ロードバランサーまたは Windows 負荷を使用した負荷分散   
    分散  
  
-   スマートカードまたはワンタイムパスワード (OTP) が必要な2要素認証  
  
KerbProxy 認証を有効にした場合、次のデプロイ計画はサポートされません。  
  
-   サイト.  
  
-   Windows 7 クライアントの DirectAccess サポート。  
  
-   強制トンネリング。 強制トンネリングを使用するときに KerbProxy 認証が有効になっていないことを確認するには、ウィザードの実行中に次の項目を構成します。  
  
    -   強制トンネリングを有効にする  
  
    -   Windows 7 クライアントの DirectAccess を有効にする  
  
> [!NOTE]  
> 以前の展開では、詳細構成ウィザードを使用する必要があります。このウィザードでは、証明書ベースのコンピューターとユーザー認証の2つのトンネル構成を使用します。 詳細については、「[単一の DirectAccess サーバーを拡張設定で展開する](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」を参照してください。  
  
## <a name="bkmk_isa"></a>ISATAP の使用  
ISATAP は、IPv4 専用企業ネットワークに IPv6 接続を提供する移行テクノロジです。 Directaccess サーバーの展開が1つの小規模および中規模の組織に限定されており、DirectAccess クライアントのリモート管理を可能にします。 ISATAP がマルチサイト、負荷分散、またはマルチドメイン環境に展開されている場合は、DirectAccess を構成する前に、それを削除するか、ネイティブ IPv6 展開に移動する必要があります。  
  
## <a name="bkmk_iphttps"></a>IPHTTPS とワンタイムパスワード (OTP) エンドポイントの構成  
IPHTTPS を使用する場合、IPHTTPS 接続は、他のデバイス (ロードバランサーなど) ではなく、DirectAccess サーバー上で終了する必要があります。 同様に、ワンタイムパスワード (OTP) 認証中に作成される帯域外 Secure Sockets Layer (SSL) 接続は、DirectAccess サーバー上で終了する必要があります。 これらの接続のエンドポイント間のすべてのデバイスは、パススルーモードで構成する必要があります。  
  
## <a name="bkmk_ft"></a>OTP 認証を使用してトンネルを強制する  
OTP と強制トンネリングを使用して2要素認証を使用して DirectAccess サーバーを展開しないでください。そうしないと、OTP 認証は失敗します。 DirectAccess サーバーと DirectAccess クライアントの間に帯域外 Secure Sockets Layer (SSL) 接続が必要です。 この接続には、DirectAccess トンネルの外部にトラフィックを送信するための除外が必要です。 強制トンネル構成では、すべてのトラフィックが DirectAccess トンネルを通過する必要があり、トンネルが確立された後に除外することはできません。 このため、強制トンネル構成では OTP 認証がサポートされていません。  
  
## <a name="bkmk_rodc"></a>読み取り専用ドメインコントローラーを使用した DirectAccess の展開  
DirectAccess サーバーは読み取り/書き込みドメインコントローラーにアクセスできる必要があり、読み取り専用ドメインコントローラー (RODC) では正常に機能しません。  
  
読み取り/書き込みドメインコントローラーは、次のようなさまざまな理由で必要になります。  
  
-   DirectAccess サーバーで、リモートアクセス Microsoft 管理コンソール (MMC) を開くには、読み取り/書き込みドメインコントローラーが必要です。  
  
-   Directaccess サーバーは、DirectAccess クライアントと DirectAccess サーバーグループポリシーオブジェクト (Gpo) に対して読み取りと書き込みの両方を行う必要があります。  
  
-   DirectAccess サーバーは、プライマリドメインコントローラーエミュレーター (PDCe) から特別にクライアント GPO を読み取り、書き込みます。  
  
これらの要件のため、RODC を使用して DirectAccess を展開しないでください。  
  


