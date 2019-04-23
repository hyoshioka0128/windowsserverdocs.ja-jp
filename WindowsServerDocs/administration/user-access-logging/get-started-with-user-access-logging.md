---
title: ユーザーの概要ログにアクセス
desctription: Describes the User Access Logging feature and how to start using it.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-user-access-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c395b8b-3b35-4042-b9cc-07e438f86d50
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8656bf278519b48f8d26008fd98e46428106e511
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861503"
---
# <a name="get-started-with-user-access-logging"></a>ユーザーの概要ログにアクセス

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ユーザー アクセス ログ (UAL) には、Windows Server およびロールのローカル サーバー上の製品のクライアント使用状況データを集約する機能です。 Windows サーバーの管理者がローカル サーバーで役割とサービスのクライアント コンピューターからの要求を定量化することができます。  
  
UAL がインストールされでデータを収集、既定で有効になっているほぼリアルタイムです。 UAL は無効にすることも有効にすることもできますが、管理者構成は必要ありません。 詳細については、「 [Manage User Access Logging](Manage-User-Access-Logging.md)」を参照してください。 ユーザー アクセス ログ サービスは、ローカル データベース ファイルにロールと製品ごとにクライアント使用状況データを集計します。  IT 管理者は後で Windows Management Instrumentation (WMI) または Windows PowerShell コマンドレットを使用し、サーバー ロール (またはソフトウェア製品) 別、ユーザー別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。  
  
> [!NOTE]  
> UAL は [Microsoft Assessment and Planning Toolkit](https://go.microsoft.com/fwlink/?LinkID=111000)をサポートします。  
  
## <a name="BKMK_APP"></a>実際の適用  
UAL は、一意のクライアント デバイスとユーザー要求イベントをローカル データベースにログに記録されるを集計します。 サーバー管理者は、クエリによってこれらの記録を使用し、サーバー ロール別、ユーザー別、デバイス別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。  さらに、UAL は、Microsoft 以外のソフトウェア開発者は Windows Server で集計される UAL イベントを有効にする拡張されています。  
  
UAL は、次のタスクを実行できます。  
  
-   ローカルの物理サーバーまたは仮想サーバーに対するクライアント ユーザーの要求を定量化します。  
  
-   ローカルの物理または仮想マシンにインストールされているソフトウェア製品に対するクライアント ユーザーの要求を定量化します。  
  
-   Hyper-V を実行するローカル サーバーでデータを取得し、Hyper-V 仮想コンピューターに対する要求が多い期間と少ない期間を明らかにします。  
  
-   複数のリモート サーバーから UAL データを取得します。  
  
さらに、ソフトウェア開発者は、集計して WMI および Windows PowerShell インターフェイスを使用して取得できる、UAL イベントをインストルメント化できます。  
  
次のサーバーの役割とサービスが UAL でサポートされます。  
  
-   Active Directory 証明書サービス (AD CS)  
  
-   Active Directory Rights Management サービス (AD RMS)  
  
-   BranchCache  
  
-   ドメイン ネーム システム (DNS)  
  
    > [!NOTE]  
    > UAL は 24 時間ごとに DNS データを収集します。このシナリオのために個別の UAL コマンドレットがあります。  
  
-   動的ホスト構成プロトコル (DHCP)  
  
-   FAX サーバー  
  
-   ファイル サービス  
  
-   ファイル転送プロトコル (FTP) サーバー  
  
-   Hyper-V  
  
    > [!NOTE]  
    > UAL は 24 時間ごとに Hyper-V データを収集します。このシナリオのために個別の UAL コマンドレットがあります。  
  
-   Web サーバー (IIS)  
  
    > [!WARNING]  
    > IIS で UAL を使用するには、iisual.exe を実行する必要があります。 詳細については、「 [Analyzing Client Usage Data with IIS User Access Logging (IIS ユーザー アクセス ログでのクライアント使用状況データの分析)](http://www.iis.net/learn/manage/configuring-security/analyzing-client-usage-data-with-iis-user-access-logging)」を参照してください。  
  
-   Microsoft メッセージ キュー (MSMQ) サービス  
  
-   ネットワーク ポリシーとアクセス サービス  
  
-   印刷とドキュメント サービス  
  
-   ルーティングとリモート アクセス サービス (RRAS)  
  
-   Windows 展開サービス (WDS)  
  
-   Windows Server Update Services (WSUS)  
  
> [!IMPORTANT]  
> UAL は、インターネットに直接接続されているサーバー (インターネットでアクセスできるアドレス空間にある Web サーバーなど) やサーバーの主な機能が非常に高パフォーマンスであるシナリオ (HPC ワークロード環境など) での使用はお勧めできません。 UAL は主に、small、medium、および高ボリュームが必要な場合、企業イントラネットのシナリオの目的を定期的にインターネットに接続するトラフィック ボリュームを処理するデプロイしないの最高です。  
  
## <a name="BKMK_NEW"></a>重要な機能  
次の表は、UAL の主な機能とその値についてまとめたものです。  
  
|機能|値|  
|-----------------|---------|  
|ほぼリアルタイムでクライアント要求イベント データを収集し、集計します。|最大 3 年分のデータを保存できます。 概要管理者は、組織のプライバシー ポリシーとローカル規制に基づき、収集されたデータの整合性とデータの保持期間を強制する必要があります。|  
|WMI または Windows PowerShell インターフェイスを利用して UAL に問い合わせ、ローカルまたはリモート サーバーのクライアント要求データを取得します。|UAL では、1 つのビューで進行中の使用状況データを参照できます。 サーバー管理者とエンタープライズ管理者は、このデータを取得し、ビジネス管理者と連携し、ボリューム ソフトウェア ライセンスを最適な方法で利用できます。|  
|既定で有効になっています。|サーバー管理者がこの機能を構成しなくても、すべてのコア機能は利用できるし、動作します。|  
  
## <a name="data-logged-with-ual"></a>UAL で記録されたデータ  
UAL では次のユーザー関連データが記録されます。  
  
|データ|説明|  
|--------|---------------|  
|**UserName**|インストールされている役割と製品からの UAL エントリを伴うクライアントでのユーザー名 (該当する場合)。|  
|**ActivityCount**|特定のユーザーが役割またはサービスにアクセスした回数。|  
|**FirstSeen**|ユーザーが役割またはサービスに最初にアクセスした日時。|  
|**lastSeen**|ユーザーが役割またはサービスに最後にアクセスした日時。|  
|**ProductName**|UAL データを提供しているソフトウェアの親製品 (Windows など) の名前。|  
|**RoleGUID**|サーバーの役割またはインストールされている製品を表す UAL 割り当てまたは登録 GUID。|  
|**RoleName**|UAL データを提供している役割、コンポーネント、またはサブ製品の名前。 これは ProductName および RoleGUID と関連付けられてもいます。|  
|**TenantIdentifier**|UAL データを伴う、インストールされている役割または製品のテナント クライアントの一意の GUID (該当する場合)。|  
  
UAL では次のデバイス関連データが記録されます。  
  
|データ|説明|  
|--------|---------------|  
|**IPAddress**|役割またはサービスにアクセスするために使用されるクライアント デバイスの IP アドレス。|  
|**ActivityCount**|特定のデバイスが役割またはサービスにアクセスした回数。|  
|**FirstSeen**|役割またはサービスにアクセスするために IP アドレスが初めて使用された日時。|  
|**lastSeen**|役割またはサービスにアクセスするために IP アドレスが最後に使用された日時。|  
|**ProductName**|UAL データを提供しているソフトウェアの親製品 (Windows など) の名前。|  
|**RoleGUID**|サーバーの役割またはインストールされている製品を表す UAL 割り当てまたは登録 GUID。|  
|**RoleName**|UAL データを提供している役割、コンポーネント、またはサブ製品の名前。 これは ProductName および RoleGUID と関連付けられてもいます。|  
|**TenantIdentifier**|UAL データを伴う、インストールされている役割または製品のテナント クライアントの一意の GUID (該当する場合)。|  
  
## <a name="BKMK_SOFT"></a>ソフトウェアの要件  
UAL は、Windows Server 2012 以降後のバージョンの Windows Server を実行するコンピューターで使用できます。  
  
## <a name="see-also"></a>関連項目  
[User Access Logging (ユーザー アクセス ログ)](https://msdn.microsoft.com/library/windows/desktop/hh437528(v=vs.85).aspx) (MSDN)  
[ユーザーを管理するアクセス ログ](Manage-User-Access-Logging.md)  
  

