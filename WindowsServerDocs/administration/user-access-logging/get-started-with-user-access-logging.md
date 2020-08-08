---
title: ユーザーアクセスログを使ってみる
desctription: Describes the User Access Logging feature and how to start using it.
ms.topic: article
ms.assetid: 5c395b8b-3b35-4042-b9cc-07e438f86d50
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da8bb60ea455578eff96aed6173e4662fffd6ade
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991757"
---
# <a name="get-started-with-user-access-logging"></a>ユーザーアクセスログを使ってみる

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ユーザーアクセスログ (UAL) は、ローカルサーバー上の役割と製品ごとにクライアント使用状況データを集計する Windows Server の機能です。 Windows server 管理者は、ローカルサーバー上の役割とサービスについて、クライアントコンピューターからの要求を定量化するのに役立ちます。

UAL は既定でインストールされ、有効になっており、ほぼリアルタイムでデータを収集します。 UAL は無効にすることも有効にすることもできますが、管理者構成は必要ありません。 詳細については、「[ユーザー アクセス ログの管理](Manage-User-Access-Logging.md)」を参照してください。 ユーザーアクセスログサービスは、ロールと製品ごとのクライアント使用状況データをローカルデータベースファイルに集計します。  IT 管理者は後で Windows Management Instrumentation (WMI) または Windows PowerShell コマンドレットを使用し、サーバー ロール (またはソフトウェア製品) 別、ユーザー別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。

> [!NOTE]
> UAL は [Microsoft Assessment and Planning Toolkit](https://go.microsoft.com/fwlink/?LinkID=111000) をサポートします。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例
UAL は、ローカルデータベースに記録される一意のクライアントデバイスイベントとユーザー要求イベントを集計します。 サーバー管理者は、クエリによってこれらの記録を使用し、サーバーの役割別、ユーザー別、デバイス別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。  さらに、UAL は、Microsoft 以外のソフトウェア開発者が Windows Server によって集計される UAL イベントを利用できるように拡張されています。

UAL では、次のタスクを実行できます。

-   ローカルの物理サーバーまたは仮想サーバーに対するクライアント ユーザーの要求を定量化します。

-   ローカルの物理または仮想マシンにインストールされているソフトウェア製品に対するクライアント ユーザーの要求を定量化します。

-   Hyper-V を実行するローカル サーバーでデータを取得し、Hyper-V 仮想コンピューターに対する要求が多い期間と少ない期間を明らかにします。

-   複数のリモート サーバーから UAL データを取得します。

さらに、ソフトウェア開発者は、WMI および Windows PowerShell インターフェイスを使用して集計および取得できる UAL イベントをインストルメント化することができます。

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
    > IIS で UAL を使用するには、iisual.exe を実行する必要があります。 詳細については、「[Analyzing Client Usage Data with IIS User Access Logging (IIS ユーザー アクセス ログでのクライアント使用状況データの分析)](https://www.iis.net/learn/manage/configuring-security/analyzing-client-usage-data-with-iis-user-access-logging)」を参照してください。

-   Microsoft メッセージ キュー (MSMQ) サービス

-   Network Policy and Access Services

-   印刷とドキュメント サービス

-   ルーティングとリモート アクセス サービス (RRAS)

-   Windows 展開サービス (WDS)

-   Windows Server Update Services (WSUS)

> [!IMPORTANT]
> UAL は、インターネットに直接接続されているサーバー (インターネットでアクセスできるアドレス空間にある Web サーバーなど) やサーバーの主な機能が非常に高パフォーマンスであるシナリオ (HPC ワークロード環境など) での使用はお勧めできません。 UAL は主に、大容量が想定されているが、インターネットに接続するトラフィックボリュームを定期的に処理する展開ほど高くない、小規模、中、およびエンタープライズのイントラネットのシナリオを対象としています。

## <a name="important-functionality"></a><a name="BKMK_NEW"></a>重要な機能
次の表は、UAL の主な機能とその値についてまとめたものです。

|機能|値|
|-----------------|---------|
|ほぼリアルタイムでクライアント要求イベント データを収集し、集計します。|最大 3 年分のデータを保存できます。 **重要:** 管理者は、組織のプライバシーポリシーとローカル規制に従って、収集されたデータとデータ保有期間のコンプライアンスを強制する必要があります。|
|WMI または Windows PowerShell インターフェイスを利用して UAL に問い合わせ、ローカルまたはリモート サーバーのクライアント要求データを取得します。|UAL では、1 つのビューで進行中の使用状況データを参照できます。 サーバー管理者とエンタープライズ管理者は、このデータを取得し、ビジネス管理者と連携し、ボリューム ソフトウェア ライセンスを最適な方法で利用できます。|
|既定で有効です。|サーバー管理者がこの機能を構成しなくても、すべてのコア機能は利用できるし、動作します。|

## <a name="data-logged-with-ual"></a>UAL で記録されたデータ
UAL では次のユーザー関連データが記録されます。

|Data|説明|
|--------|---------------|
|**UserName**|インストールされている役割と製品からの UAL エントリを伴うクライアントでのユーザー名 (該当する場合)。|
|**ActivityCount**|特定のユーザーが役割またはサービスにアクセスした回数。|
|**FirstSeen**|ユーザーが役割またはサービスに最初にアクセスした日時。|
|**LastSeen**|ユーザーが役割またはサービスに最後にアクセスした日時。|
|**同様**|UAL データを提供しているソフトウェアの親製品 (Windows など) の名前。|
|**RoleGUID**|サーバーの役割またはインストールされている製品を表す UAL 割り当てまたは登録 GUID。|
|**RoleName**|UAL データを提供している役割、コンポーネント、またはサブ製品の名前。 これは ProductName および RoleGUID と関連付けられてもいます。|
|**TenantIdentifier**|UAL データを伴う、インストールされている役割または製品のテナント クライアントの一意の GUID (該当する場合)。|

UAL では次のデバイス関連データが記録されます。

|Data|説明|
|--------|---------------|
|**IPAddress**|役割またはサービスにアクセスするために使用されるクライアント デバイスの IP アドレス。|
|**ActivityCount**|特定のデバイスが役割またはサービスにアクセスした回数。|
|**FirstSeen**|役割またはサービスにアクセスするために IP アドレスが初めて使用された日時。|
|**LastSeen**|役割またはサービスにアクセスするために IP アドレスが最後に使用された日時。|
|**同様**|UAL データを提供しているソフトウェアの親製品 (Windows など) の名前。|
|**RoleGUID**|サーバーの役割またはインストールされている製品を表す UAL 割り当てまたは登録 GUID。|
|**RoleName**|UAL データを提供している役割、コンポーネント、またはサブ製品の名前。 これは ProductName および RoleGUID と関連付けられてもいます。|
|**TenantIdentifier**|UAL データを伴う、インストールされている役割または製品のテナント クライアントの一意の GUID (該当する場合)。|

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件
UAL は、Windows Server 2012 以降のバージョンの Windows Server を実行しているすべてのコンピューターで使用できます。

## <a name="additional-references"></a>その他の参照情報
[User Access Logging (ユーザー アクセス ログ)](/previous-versions/windows/desktop/ual/user-access-logging) (MSDN)
[ユーザー アクセス ログの管理](Manage-User-Access-Logging.md)