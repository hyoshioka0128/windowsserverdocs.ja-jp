---
title: Server Core 2008 とは何ですか。
description: Windows Server 2008 の Server Core インストール オプションについて説明します
ms.prod: windows-server-threshold
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 8d1aaf8b61142155ea7b2a5391367cc677596ebe
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435603"
---
# <a name="what-is-server-core-2008"></a>Server Core 2008 とは何ですか。
>適用先:Windows Server 2008

>[!NOTE]
>この情報は、Windows Server 2008 に適用されます。 Windows Server の Server Core については、次を参照してください。[新機能 Windows Server の Server Core インストール](https://docs.microsoft.com/windows-server/administration/server-core/what-is-server-core)します。 

Server Core オプションは、Windows Server 2008 の Standard、Enterprise、または Datacenter edition を展開する場合に使用できる新しい最小限のインストール オプションです。 Server Core では、特定のサーバー ロールのみのインストールをサポートする Windows Server 2008 の最小限のインストール後、この章で説明。 すべての利用可能なサーバー ロールともその他の Microsoft または Microsoft Exchange Server や SAP などのサード パーティのサーバー アプリケーションのインストールをサポートする Windows Server 2008 のフル インストール オプションとは対照的です。 

入る前にさらに、「インストール オプション」という語句を説明する必要があります。 通常、Windows Server 2008 のコピーを購入すると、特定のエディションや在庫管理単位 (Sku) を使用するライセンスを購入します。 表 1-1 には、使用可能な Windows Server 2008 のさまざまなエディションが一覧表示します。 また、各エディションのインストール オプション (フル、Server Core、またはその両方) が利用も示します。

**表 1-1** Windows Server 2008 のエディションとインストール オプションのサポート

| エディション       | 完全          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (x86 および x64)       | x | x        |
| Windows Server 2008 Enterprise (x86 および x64)       | x | x        |
| Windows Server 2008 Datacenter (x86 および x64)        | x | x       |
| Windows Web Server 2008 (x86 および x64)       | x | x  |
| Windows Server 2008 For Itanium ベース システム       | x |     |
| Windows HPC Server 2008 (x64 のみ)       | x |   |
| Windows Server 2008 Standard without HYPER-V (x86 および x64) | x | x |
| Windows Server 2008 Enterprise without HYPER-V (x86 および x64)  | x | x |
| Windows Server 2008 Standard without HYPER-V (x86 および x64) | x | x |

内容を理解するには、「インストール オプション」は、Windows Server 2008 Enterprise Edition のコピーをインストールすることができます、ボリューム ライセンスを購入したとしましょう。 システムに、ボリューム ライセンス メディアを挿入し、図 1-1 に示すように、画面のいずれかのインストール プロセスを開始の各エディションとインストール オプションの選択肢が表示されます。

![インストールする Server Core インストール オプションを選択します。](../media/what-is-server-core-2008/FIg1-1.png)

**図 1-1**をインストールする Server Core インストール オプションを選択します。

図 1-1 では、ボリューム ライセンス (または製品版メディア用のプロダクト キー) の方が 2 つのインストール オプションから選択できます 2 番目のオプション (、完全なインストールの Windows Server 2008 Enterprise) と 5 番目のオプション (、Server Core インストールの Windows。Server 2008 Enterprise の場合)、この例で選択されている後者でします。 

## <a name="full-vs-server-core"></a>完全な vs します。Server Core 
Microsoft Windows プラットフォームの初期の段階から、Windows を使用していた基本的に「すべて」、うちいくつか使用する機能が実際には、ネットワーク環境でのすべての種類が含まれているサーバー。 たとえば、システムで Windows Server 2003 をインストールしたときにルーティングとリモート アクセス サービス (RRAS) のバイナリ インストールされたサーバー上でもがあるない場合にこのサービスが必要 (ただし、まだ構成して、その前に、RRAS を有効にする必要がある)。 Windows Server 2008 では、以前のバージョンがサーバーでその特定のロールをインストールする場合にのみ、サーバーの役割で必要なバイナリをインストールすることで向上します。 ただし、Windows Server 2008 のフル インストール オプションは、多くのサービスおよび特定の使用シナリオのために必要な多くの場合、その他のコンポーネントをまだインストールされます。 

Microsoft は、2 番目のインストール オプションを作成する理由です: Server Core-Windows Server 2008: すべてのサービスと不要な特定のサポートが一般的にサーバーの役割を使用するその他の機能を排除します。 たとえば、ドメイン ネーム システム (DNS) サーバーを本当に必要はありませんはセキュリティ上の理由から、DNS サーバーから Web を閲覧するためにインストールされている Windows Internet Explorer。 DNS サーバーは、グラフィカル ユーザー インターフェイス (GUI) を必要もありません、DNS のほぼすべての側面を管理するため、強力な Dnscmd.exe コマンドを使用またはリモートで DNS Microsoft 管理コンソール (MMC) を使用して、コマンドラインからいずれかのスナップインです。

これを回避するには、Microsoft の決定が Active Directory Domain Services (AD DS)、DNS、動的ホスト構成プロトコル (DHCP)、ファイルおよび印刷などのコア ネットワークのサービスを実行するため絶対に不可欠な Windows Server 2008 からのすべてのものを削除して、他のいくつかのサーバー ロール。 役割と機能の限られた数のみをサポートするサーバーを作成するために使用できる新しい Server Core インストール オプションになります。 

## <a name="the-server-core-gui"></a>Server Core GUI
最初にシステムとのログで Server Core のインストールが完了したら、あなた少し驚きでした。 図 1-2 では、最初のログオン後、Server Core のユーザー インターフェイスを示しています。

![Server Core のユーザー インターフェイス](../media/what-is-server-core-2008/Fig1-2.png)

**図 1-2**サーバー コア ユーザー インターフェイス

デスクトップはありません。 これは、[スタート] メニュー、タスク バーで、表示されるその他の機能と、Windows エクスプ ローラー シェルではありません。 必要なは、コマンド プロンプト、高速化し、configurati を簡略化は低速で、時間、またはスクリプトとすることができます、バッチ ファイルを使用して 1 つのコマンドを入力するか、Server Core インストールを構成する作業の大部分を実行する必要があります。それらを自動化することによってタスク。 Server Core の無人インストールを実行すると、応答ファイルを使用していくつかの初期構成タスクを実行することもできます。 

Netsh.exe、Dfscmd.exe、Dnscmd.exe などのコマンド ライン ツールを使用してに精通した管理者の場合は、構成と Server Core インストールを管理できる、楽しく簡単。 専門家でない方、ただし、すべては失われません。 Server Core インストールを管理するため、標準の Windows Server 2008 の MMC ツールを引き続き使用できます。 Service Pack 1 のいずれかの Windows Server 2008 の完全インストールまたは Windows Vista を実行している別のシステムでこれらを使用する必要があります。 

構成して、以降の章が特定のサーバーの役割とその他のコンポーネントを管理する方法を扱うときに、Server Core インストールで章 3 ~ 6 の本を管理する詳細については説明します。 さまざまな Windows コマンド ライン ツールとその使用方法の詳細についてを参照する 2 つの優れたリソースがあります。
* Windows Server 2008 テクニカル ライブラリ () のコマンドのリファレンス セクション 
* *Windows コマンド ライン Administrator's Pocket consultant 』* William R. Stanek (Microsoft Press、2008 年) 

表 1-2 には、その実行可能ファイル、Server Core インストールで利用できると共に、メインの GUI アプリケーションが一覧表示します。

**表 1-2** Server Core インストールで使用可能な GUI アプリケーション

| GUI アプリケーション | パスの実行可能ファイル |
| -------------   | -------------       | 
| コマンド プロンプト | %WINDIR%\System32\Cmd.exe |
| Microsoft サポート診断ツール | %WINDIR%\System32\MSdt.exe |
| メモ帳 | %WINDIR%\System32\Notepad.exe |
| レジストリ エディター | %WINDIR%\System32\Regedt32.exe |
| システム情報 | %WINDIR%\System32\MSinfo32.exe |
| タスク マネージャー | %WINDIR%\System32\Taskmgr.exe |
| Windows インストーラー | %WINDIR%\System32\MSiexec.exe |

とても簡単な一覧です。 ここでは、Server Core には含まれていないユーザー インターフェイス要素の一覧を示します。
* Windows エクスプ ローラー デスクトップ シェル (Explorer.exe) とテーマなどの任意のサポート機能 
* すべての MMC コンソール 
* 地域と言語のオプション (Intl.cpl) および日付と時刻 (Timedate.cpl) を除き、すべてのコントロール パネルの ユーティリティ 
* Internet Explorer、HTML ヘルプなど、すべてのハイパー テキスト マークアップ言語 (HTML) レンダリング エンジン 
* Windows メール 
* Windows Media Player 
* ペイント、電卓、ワードパッドなどのほとんどのアクセサリ

.NET Framework も Server Core インストールでマネージ コードの実行はサポートされていませんが、Server Core に存在できません。 ネイティブ コードのみ-Windows アプリケーション プログラミング インターフェイス (Api) を使用して記述されたコード、Server Core で実行できます。 要約すると、.NET Framework のいずれかに依存しているすべての GUI アプリケーションで、または、Explorer.exe のシェルは Server Core で実行されません。 

>[!NOTE]
>Windows PowerShell には、.NET Framework が必要であるために、Server Core 上に Windows PowerShell をインストールすることはできません。 ただし、PowerShell WMI コマンドのみを使用するように Windows PowerShell を使用してリモートで Server Core インストールを管理することができます。

## <a name="supported-server-roles"></a>サポートされているサーバーの役割 
Server Core インストールには、Windows Server 2008 のフル インストールと比較して、サーバーの役割の制限の数のみが含まれています。 表 1-3 は、Windows Server 2008 Enterprise Edition の完全と Server Core の両方がインストールされて利用可能な役割を比較します。 

**表 1-3**の Windows Server 2008 Enterprise Edition のインストールをフル インストール オプションと Server Core サーバーの役割の比較

| サーバーの役割  | フル インストールで利用可能  | Server Core で使用できます。  |
| ------------- | :-------------: | :------------: |
| Active Directory 証明書サービス (AD CS)  | x |  |
| Active Directory ドメイン サービス (AD DS)  | x  | x |
| Active Directory フェデレーション サービス (AD FS)  | x  |  |
| Active Directory ライトウェイト ディレクトリ サービス (AD LDS)  | x  | x |
| Active Directory Rights Management サービス (AD RMS)  | x  |  |
| アプリケーション サーバー  | x  |  |
| DHCP サーバー  | x  | x |
| DNS サーバー  | x  | x |
| FAX サーバー  | x  |  |
| ファイル サービス  | x  | x |
| Hyper-V  | x | x |
| ネットワーク ポリシーとアクセス サービス  | x  |  |
| 印刷サービス  | x  | x |
| ストリーミング メディア サービス  | x  | x |
| Terminal Services  | x  |  |
| UDDI サービス  | x  |  |
| Web サーバー (IIS) | x | x |
| Windows 展開サービス  | x |  |

Server Core の使用可能な役割は、アーキテクチャ (x86 または x64) と製品のエディションに関係なく同じでは一般に、いくつかの例外もあります。
* (仮想化)、HYPER-V ロールは、HYPER-V の製品メディアを使用した Windows Server 2008 を購入した場合にのみ使用できます (HYPER-V は x64 でのみ使用できますのバージョン)。 このロールが必要ない場合は場合、代わりに、HYPER-V の製品メディアのない Windows Server 2008 を購入できます。 
* Standard Edition でファイル サービスの役割は、1 つのスタンドアロンの分散ファイル システム (DFS) ルートに制限され、ファイル間レプリケーション (DFS-R) をサポートしていません。 
* Server Core でストリーミング メディア サービスの役割をインストールすることができます、前にする必要がありますをダウンロードして、適切な Microsoft 更新プログラム スタンドアロン パッケージ (.msu ファイル)、サーバーのアーキテクチャ (x86 または x64) をインストール、Microsoft ダウンロード センターから。
* Web サーバー (IIS) ロールは、ASP.NET をサポートしていません。 これは、.NET Framework が Server Core の Web サーバーで行うことができますを制限する Server Core でサポートされていないためにです。 

## <a name="supported-optional-features"></a>サポートされているオプション機能
Server Core インストールは、Windows Server 2008 のフル インストールにも使用できる機能の一部のサブセットのみをサポートします。 表 1-4 は、Windows Server 2008 Enterprise Edition の完全と Server Core の両方がインストールされて利用可能な機能を比較します。

**表 1-4**の Windows Server 2008 Enterprise Edition のインストールをフル インストール オプションと Server Core の機能の比較

| 機能  | フル インストールで利用可能  | Server Core で使用できます。  |
| ------------- | :-------------: | :------------: |
| .NET framework 3.0 の機能  | x  |  |
| 役割と機能の追加ウィザード  | x  | x |
| BITS サーバー拡張  | x  |  |
| 接続マネージャー管理キット  | x |  |
| デスクトップ エクスペリエンス  | x |  |
| フェールオーバー クラスタリング  | x  | x |
| グループ ポリシーの管理  | x  |  |
| インターネット印刷クライアント  | x  |  |
| インターネット ストレージ ネーム サーバー  | x  |  |
| LPR ポート モニター  | x  |  |
| メッセージ キューイング (Message Queuing)  | x  |  |
| マルチパス I/O  | x  | x |
| ネットワーク負荷分散  | x  | x |
| ピア名解決プロトコル  | x  |  |
| 高品質な Windows オーディオ ビデオ エクスペリエンス  | x |  |
| リモート アシスタンス  | x  |  |
| Remote Differential Compression | x  |  |
| リモート サーバー管理ツール  | x  |  |
| リムーバブル記憶域マネージャー | x  | x |
| RPC Over HTTP プロキシ | x  |  |
| Simple TCP/IP Services  | x  |  |
| SMTP サーバー  | x  |  |
| SMNP サービス  | x  | x  |
| SAN 用記憶域マネージャー  | x  |  |
| UNIX ベース アプリケーション用サブシステム | x | x  |
| Telnet クライアント  | x | x  |
| Telnet サーバー  | x   |  |
| TFTP クライアント  | x   |  |
| Windows Internal Database  | x  |  |
| Windows PowerShell  | x  |  |
| Windows 製品ライセンス認証サービス  | x   |  |
| Windows Server バックアップ機能  | x  | x  |
| Windows システム リソース マネージャー  | x  |  |
| WINS サーバー  | x | x |
| ワイヤレス LAN サービス | x  |  |

ここでもは、Server Core で使用できる機能について把握する必要があるいくつかの点があります。
* 一部の機能は、Server Core で正しく (またはまったく) に機能する特殊なハードウェアを必要があります。 これらの機能には、BitLocker ドライブ暗号化、フェールオーバー クラスタ リング、マルチパス IO、ネットワーク負荷分散、およびリムーバブル記憶域が含まれます。 
* フェールオーバー クラスタ リングでは、Standard Edition では使用できません。

## <a name="server-core-architecture"></a>Server Core のアーキテクチャ
Server Core に詳細を理解、について簡単に見てみましょう Windows Server 2008 の Server Core インストールのアーキテクチャのフル インストールと比較しています。 最初に、Server Core は、異なるバージョンの Windows Server 2008 が、システムに Windows Server 2008 をインストールするときに選択可能なインストール オプションだけではないことに注意してください。 これは、次を意味します。
* Server Core インストールでのカーネルとは、同じハードウェア アーキテクチャ (x86 または x64) とエディションのフル インストールで検出されたものと同じです。 
* バイナリが Server Core インストール上に存在する場合は、同じハードウェア アーキテクチャ (x86 または x64) とエディションのフル インストールでは (後で説明する 2 つの例外) をその特定のバイナリの同じバージョンがあります。 
* その設定で同じのフル インストールにまったく同じ方法が構成されている場合 (特定のファイアウォールの例外や、特定のサービスのスタートアップの種類など) の特定の設定は、特定の既定の構成を Server Core インストールでは、ハードウェアのアーキテクチャ (x86 または x64) とエディション。

図 1-3 は、フル インストールと Windows Server 2008 の Server Core インストールの両方のアーキテクチャの概略を示します。 ダイアグラム全体が完全なインストールのアーキテクチャを表して、点線は、Server Core のアーキテクチャを示します。 

図では、コア オペレーティング システムの機能のサブセットに構築される、Server Core での Windows Server 2008 のモジュール アーキテクチャを示します。 同じのハードウェア アーキテクチャとエディションの Server Core のクリーン インストールですべてのファイルに存在もと 2 つ特殊なファイル (ある Scregedit.wsf Oclist.exe)、Server Core 上にのみ存在である例外のフル インストール上に存在できます。 これらの特殊なファイルを Server Core インストールと追加の初期構成またはロールおよび省略可能なコンポーネントの削除を簡略化の Server Core に含まれていた。 

![Server Core とフル インストールのアーキテクチャ](../media/what-is-server-core-2008/Fig1-3.png)

**図 1-3** Server Core とフル インストールのアーキテクチャ

## <a name="driver-support"></a>ドライバーのサポート
図 1-3 に示すように、Server Core のアーキテクチャの図は明らかに簡略化されます。表示されないことの 1 つは、Server Core とフル インストールの間でデバイス ドライバーのサポート差です。 Windows Server 2008 のフル インストールには、何千も異なるハードウェア構成のさまざまな製品をインストールすることを可能にするには、デバイスのさまざまな種類のインボックス ドライバーにはが含まれています。 (など、Windows Vista クライアント オペレーティング システムはデジタル カメラやスキャナーは、通常はサーバーで使用されるなどのデバイスをサポートするためにさらに多くのドライバーを含む)。 

新しいデバイスに接続されている (またはにインストールされている) Windows Server 2008 のフル インストールは、プラグ アンド プレイ (PnP) サブシステムはまずデバイス用のインボックス ドライバーが存在するかどうか。 互換性のあるインボックス ドライバーが見つかると、PnP サブシステムが、自動的とデバイスのドライバーをインストールし、動作します。 Windows Server 2008 のフル インストールで、ドライバーがインストールされて、デバイスが使用できることを示す、ポップアップ通知のバルーンを表示可能性があります。 

Server Core インストールでは、ドライバーのインストール プロセスは、同じ (PnP サブシステムは Server Core 上に存在する) 2 つの条件を満たすです。 最初に、Server Core には、最小限に抑えるインボックス ドライバー、およびデバイスの次の型に対してのみにはが含まれています。
* 標準のビデオ グラフィックス配列 (VGA) ビデオ ドライバー 
* 記憶装置のドライバー 
* ネットワーク アダプターのドライバー

ここに示す 3 つのデバイス カテゴリごとに、Server Core が含まれること (同じハードウェア アーキテクチャ) に対応するフル インストール上にある同じのインボックス ドライバーに注意してください。 

また、PnP サブシステムは、新しいデバイスのドライバーをインストールする自動的に、これはサイレント モードで、ポップアップ通知のバルーンは表示されません。 表示されない Server Core で GUI がないためにがありませんタスク バーで、タスクバーの通知領域はありません。 

そこで皆さんは、印刷サービスの役割を Server Core インストールに追加して、プリンターをインストールするときにでしょうか。 サーバーにプリンター ドライバーを手動で追加する、Server Core には、ボックスの印刷ドライバーがありません。

## <a name="service-footprint"></a>サービスのフット プリント
Server Core は、最小限のインストールであるため、同じハードウェア アーキテクチャとエディションの場合は、対応する完全インストールよりもには、小規模なシステム サービス フット プリントがあります。 たとえば、約 75 台のシステム サービスが自動的に開始する約 50 が構成されている、Windows Server 2008 のフル インストールに既定でインストールされます。 これに対し、Server Core のみ約 70 サービスがインストールされて、これらの開始よりも少ない 40、既定で自動的にします。 

表 1. ~ 5. のスタートアップ モードの Server Core インストールで既定でインストールされているサービスの一覧し、アカウントは、各サービスで使用されます。

**表 1-5**システム サービスが既定では、Server Core インストール

| サービス名  | 表示名  | スタートアップ モード  | アカウント  |
| ------------- | ------------- | ------------ | ------------ |
| AeLookupSvc  | アプリケーション エクスペリエンス  | Auto | LocalSystem |
| AppMgmt  | アプリケーション管理  | Manual | LocalSystem |
| BFE | ベース フィルター エンジン  | Auto | LocalService |
| BITS | バックグラウンド インテリジェント転送サービス  | Auto | LocalSystem |
| ブラウザー | コンピューター ブラウザー  | Manual | LocalSystem |
| CertPropSvc | 証明書伝達  | Manual | LocalSystem |
| COMSysApp  | COM+ System Application  | Manual | LocalSystem |
| 証明書サービス  | 暗号化サービス  | Auto | ネットワーク サービス |
| DcomLaunch  | DCOM サーバー プロセス ランチャー  | Auto | LocalSystem |
| Dhcp  | DHCP クライアント  | Auto | LocalService |
| 改名 | DNS クライアント  | Auto | ネットワーク サービス |
| DPS  | 診断ポリシー サービス  | Auto | LocalService |
| イベント ログ | Windows イベント ログ  | Auto | LocalService |
| EventSystem  | COM + イベント システム  | Auto | LocalService |
| FCRegSvc  | ファイバー チャネルの Microsoft プラットフォームの登録サービス  | Manual | LocalService |
| gpsvc  | グループ ポリシー クライアント  | Auto | LocalSystem |
| hidserv | ヒューマン インターフェイス デバイスへのアクセス  | Manual | LocalSystem |
| hkmsvc  | 正常性のキーと証明書の管理  | Manual | LocalSystem |
| IKEEXT  | IKE および AuthIP IPsec のキー モジュール  | Auto | LocalSystem |
| iphlpsvc  | IP ヘルパー  | Auto | LocalSystem |
| KeyIso | CNG キー分離  | Manual | LocalSystem |
| KtmRm  | 分散トランザクション コーディネーター向け KtmRm  | Auto | ネットワーク サービス |
| LanmanServer  | Server  | Auto | LocalSystem |
| LanmanWorkstation  | Workstatione  | Auto | LocalService |
| lltdsvc  | リンク層トポロジ検出マッパー  | Manual | LocalService |
| lmhosts  | TCP/IP NetBIOS Helper  | Auto | LocalService |
| MpsSvc  | Windows ファイアウォール  | Auto | LocalService |
| MSDTC  | 分散トランザクション コーディネーター  | Auto | ネットワーク サービス |
| MSiSCSI  | Microsoft iSCSI イニシエーター サービス  | Manual | LocalSystem |
| msiserver  | Windows インストーラー  | Manual | LocalSystem |
| napagent  | ネットワーク アクセス保護エージェント  | Manual | ネットワーク サービス |
| Netlogon  | Netlogon  | Manual | LocalSystem |
| netprofm  | ネットワーク一覧サービス  | Auto | LocalService |
| NlaSvc  | Network Location Awareness  | Auto | ネットワーク サービス |
| nsi  | ネットワーク ストア インターフェイス サービス  | Auto | LocalService |
| pla  | パフォーマンス ログとアラート  | Manual | LocalService |
| PlugPlay  | プラグ アンド プレイ  | Auto | LocalSystem |
| ポリシー エージェント  | IPSec ポリシー エージェント  | Auto | ネットワーク サービス |
| ProfSvc  | ユーザー プロファイル サービス  | Auto | LocalSystem |
| ProtectedStorage  | 保護されたストレージ  | Manual | LocalSystem |
| RemoteRegistry  | リモート レジストリ  | Auto | LocalService |
| RpcSs  | リモート プロシージャ コール (RPC)  | Auto | ネットワーク サービス |
| RSoPProv | ポリシー プロバイダの結果セット  | Manual | LocalSystem |
| sacsvr  | 特別な管理コンソールのヘルパー  | Manual | LocalSystem |
| SamSs  | セキュリティ アカウント マネージャー  | Auto | LocalSystem |
| SCardSvr | スマート カード  | Manual | LocalService |
| [スケジュール] | タスク スケジューラ  | Auto | LocalSystem |
| SCPolicySvc | スマート カードの削除ポリシー  | Manual | LocalSystem |
| seclogon | セカンダリ ログオン  | Auto | LocalSystem |
| SENS | システム イベント通知サービス  | Auto | LocalSystem |
| SessionEnv | ターミナル サービス構成  | Manual | LocalSystem |
| slsvc  | ソフトウェア ライセンス | Auto | ネットワーク サービス |
| SNMPTRAP  | SNMP トラップ  | Manual | LocalService |
| swprv  | Microsoft ソフトウェア シャドウ コピー プロバイダー | Manual | LocalSystem |
| TB | TPM ベースのサービス  | Manual | LocalService |
| TermService  | Terminal Services | Auto | ネットワーク サービス |
| TrustedInstaller | Windows モジュール インストーラー  | Auto | LocalSystem |
| UmRdpService | Terminal Services UserMode Port リダイレクター  | Manual | LocalSystem |
| vds | 仮想ディスク  | Manual | LocalSystem |
| VSS | ボリューム シャドウ コピー  | Manual | LocalSystem |
| W32Time | Windows タイム  | Auto | LocalService |
| WcsPlugInService  | Windows カラー システム  | Manual | LocalService |
| WdiServiceHost  | 診断サービス ホスト  | Manual | LocalService |
| WdiSystemHost  | 診断システムでのホスト  | Manual | LocalSystem |
| Wecsvc | Windows イベント コレクター  | Manual | ネットワーク サービス |
| WinHttpAuto ProxySvc  | WinHTTP の Web プロキシ自動検出サービス  | Auto | LocalService |
| Winmgmt | Windows Management Instrumentation (Windows Management Instrumentation) | Auto | LocalSystem |
| WinRM  | Windows リモート管理 (Ws-management) | Auto | ネットワーク サービス |
| wmiApSrv  | WMI Performance Adapter  | Manual | LocalSystem |
| wuauserv | Windows Update | Auto | LocalSystem |