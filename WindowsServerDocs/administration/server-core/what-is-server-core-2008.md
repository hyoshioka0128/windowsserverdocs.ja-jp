---
title: Server Core 2008 とは
description: Windows Server 2008 の Server Core インストールオプションについて説明します。
ms.prod: windows-server
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 0a109d0bfc4fc09b5e8097059d68b728d17752a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383385"
---
# <a name="what-is-server-core-2008"></a>Server Core 2008 とは
>適用先:Windows Server 2008

>[!NOTE]
>この情報は、Windows Server 2008 に適用されます。 Windows Server の Server Core の詳細について[は、「Windows server の Server Core インストールとは](https://docs.microsoft.com/windows-server/administration/server-core/what-is-server-core)」を参照してください。 

Server Core オプションは、Windows Server 2008 の Standard、Enterprise、または Datacenter edition を展開するときに使用できる、新しい最小インストールオプションです。 Server Core では、この章で後ほど説明するように、特定のサーバーの役割のインストールのみをサポートする Windows Server 2008 の最小限のインストールが提供されます。 これと比較して、Windows Server 2008 のフルインストールオプションでは、利用可能なすべてのサーバー役割と、Microsoft Exchange Server や SAP などの他の Microsoft またはサードパーティ製サーバーアプリケーションのインストールをサポートしています。 

さらに先に進む前に、"インストールオプション" という語句を説明する必要があります。 通常、Windows Server 2008 のコピーを購入する場合は、特定のエディションまたは在庫保持ユニット (Sku) を使用するためのライセンスを購入します。 表1-1 に、使用可能な Windows Server 2008 の各種エディションを示します。 また、各エディションで使用できるインストールオプション (Full、Server Core、またはその両方) についても示します。

**表 1-1**Windows Server 2008 のエディションとインストールオプションのサポート

| エディション       | [完全]          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (x86 および x64)       | x | x        |
| Windows Server 2008 Enterprise (x86 および x64)       | x | x        |
| Windows Server 2008 Datacenter (x86 および x64)        | x | x       |
| Windows Web Server 2008 (x86 および x64)       | x | x  |
| Itanium ベースシステム用 Windows Server 2008       | x |     |
| Windows HPC Server 2008 (x64 のみ)       | x |   |
| Windows Server 2008 Standard without Hyper-v (x86 および x64) | x | x |
| Windows Server 2008 Enterprise without Hyper-v (x86 および x64)  | x | x |
| Windows Server 2008 Standard without Hyper-v (x86 および x64) | x | x |

"インストールオプション" とは何かを理解するために、Windows Server 2008 Enterprise Edition のコピーをインストールできるボリュームライセンスを購入したとします。 ボリュームライセンスメディアをシステムに挿入し、インストールプロセスを開始すると、図1-1 に示すように、表示される画面のいずれかに、エディションとインストールオプションの選択肢が表示されます。

![インストールする Server Core インストールオプションの選択](../media/what-is-server-core-2008/FIg1-1.png)

**図 1-1**インストールする Server Core インストールオプションの選択

図1-1 では、ボリュームライセンス (製品版メディアの場合はプロダクトキー) に2つのインストールオプションが用意されています。2つ目のオプション (Windows Server 2008 Enterprise のフルインストール) と5番目のオプション (Windows の Server Core インストール) です。サーバー 2008 Enterprise) で、後者はこの例で選択されています。 

## <a name="full-vs-server-core"></a>完全比較とServer Core 
Windows server は、Microsoft Windows プラットフォームの初期段階から、すべての種類の機能を備えた "すべて" のサーバーでしたが、実際にはネットワーク環境では使用しないことがあります。 たとえば、システムに Windows Server 2003 をインストールした場合、このサービスが不要な場合でも、ルーティングとリモートアクセスサービス (RRAS) のバイナリはサーバーにインストールされています (ただし、動作する前に RRAS を構成して有効にする必要があります)。 Windows Server 2008 では、サーバー上に特定の役割をインストールすることを選択した場合にのみ、サーバーの役割に必要なバイナリをインストールすることによって、以前のバージョンが改善されています。 ただし、Windows Server 2008 のフルインストールオプションでは、特定の使用シナリオに必要ではない多くのサービスやその他のコンポーネントもインストールされます。 

その理由は、Microsoft が2番目のインストールオプションである Server Core (Windows Server 2008 用) を作成し、一般的に使用されるサーバーの役割をサポートするために不可欠ではないサービスやその他の機能を排除するためです。 たとえば、ドメインネームシステム (DNS) サーバーに Windows Internet Explorer がインストールされている必要はありません。これは、セキュリティ上の理由から、DNS サーバーから Web を参照する必要がないためです。 また、dns サーバーはグラフィカルユーザーインターフェイス (GUI) を必要としません。これは、強力な Dnscmd コマンドを使用してコマンドラインから、または DNS Microsoft 管理コンソール (MMC) スナップインを使用してリモートで、DNS のほぼすべての側面を管理できるためです。

これを回避するために、Microsoft では、Active Directory Domain Services (AD DS)、DNS、動的ホスト構成プロトコル (DHCP)、ファイルと印刷、およびなどのコアネットワークサービスを実行するために不可欠ではない Windows Server 2008 からすべてを取り除くことにしました。他のいくつかのサーバーの役割。 その結果、新しい Server Core インストールオプションが作成されます。このオプションを使用して、限られた数の役割と機能をサポートするサーバーを作成できます。 

## <a name="the-server-core-gui"></a>Server Core GUI
システムへの Server Core のインストールが完了し、初めてログオンするときは、少し驚きます。 図1-2 は、最初のログオン後の Server Core ユーザーインターフェイスを示しています。

![Server Core ユーザーインターフェイス](../media/what-is-server-core-2008/Fig1-2.png)

**図 1-2**Server Core ユーザーインターフェイス

デスクトップがありません。 つまり、[スタート] メニュー、タスクバー、および表示に使用できるその他の機能を備えた Windows Explorer シェルはありません。 すべてのコマンドプロンプトが表示されます。これは、Server Core インストールを構成するほとんどの作業を実行する必要があることを意味します。つまり、コマンドを1つずつ入力するか、スクリプトやバッチファイルを使用します。これにより、構成を高速化し、簡素化することができます。タスクを自動化することによって行います。 また、Server Core の無人インストールを実行するときに、応答ファイルを使用して初期構成タスクを実行することもできます。 

Netsh.exe、printbrm.exe、および Dnscmd などのコマンドラインツールを使用する専門家である管理者にとっては、Server Core インストールの構成と管理は簡単です。 しかし、専門家ではない人にとっては、すべてのことが失われるわけではありません。 Standard Windows Server 2008 MMC ツールを使用して、Server Core インストールを管理することもできます。 Windows Server 2008 または Windows Vista Service Pack 1 の完全インストールを実行している別のシステムで使用する必要があります。 

Server Core インストールの構成と管理の詳細については、このブックの 3 ~ 6 章を参照してください。また、後の章では、特定のサーバーの役割やその他のコンポーネントを管理する方法についても説明します。 さまざまな Windows コマンドラインツールとその使用方法の詳細については、次の2つの優れたリソースを参照してください。
* Windows Server 2008 テクニカルライブラリのコマンドリファレンスセクション () 
* *Windows コマンドライン管理者のポケットコンサルタント*(ウィリアム Stanek) (Microsoft Press、2008) 

表1-2 に、Server Core インストールで使用できるメインの GUI アプリケーションとその実行可能ファイルの一覧を示します。

**表 1-2**Server Core インストールで使用できる GUI アプリケーション

| GUI アプリケーション | 実行可能ファイルとパス |
| -------------   | -------------       | 
| コマンド プロンプト | %WINDIR%\System32\Cmd.exe |
| Microsoft サポート診断ツール | %WINDIR%\System32\MSdt.exe |
| メモ帳 | %WINDIR%\System32\Notepad.exe |
| レジストリエディター | %WINDIR%\System32\Regedt32.exe |
| システム情報 | %WINDIR%\System32\MSinfo32.exe |
| タスク マネージャー | %WINDIR%\System32\Taskmgr.exe |
| Windows インストーラー | %WINDIR%\System32\MSiexec.exe |

これはとても簡単な一覧です。 ここで、Server Core に含まれていないユーザーインターフェイス要素の一覧を示します。
* Windows Explorer デスクトップシェル (explorer.exe) と、テーマなどのサポート機能 
* すべての MMC コンソール 
* 地域と言語のオプション (国際 cpl) と日付と時刻 (Timedate. cpl) を除く、すべてのコントロールパネルユーティリティ 
* Internet Explorer と HTML ヘルプを含む、すべてのハイパーテキストマークアップ言語 (HTML) 表示エンジン 
* Windows メール 
* Windows Media Player 
* ペイント、電卓、ワードパッドなどのほとんどのアクセサリ

.NET Framework も Server Core には存在しません。つまり、Server Core インストールでのマネージコードの実行はサポートされていません。 ネイティブコードのみ (Windows アプリケーションプログラミングインターフェイス (Api) を使用して記述されたコード) は、Server Core で実行できます。 要約すると、.NET Framework または explorer.exe シェルに依存するすべての GUI アプリケーションは、Server Core では実行されません。 

>[!NOTE]
>Windows PowerShell には .NET Framework が必要なため、Windows PowerShell を Server Core にインストールすることはできません。 ただし、PowerShell WMI コマンドのみを使用している限り、Windows PowerShell を使用して Server Core インストールをリモートで管理することができます。

## <a name="supported-server-roles"></a>サポートされているサーバーの役割 
Server Core インストールには、Windows Server 2008 の完全インストールと比較した場合のサーバーの役割の数が制限されています。 表1-3 では、Windows Server 2008 Enterprise Edition のフルインストールと Server Core インストールの両方で使用できるロールを比較します。 

**表 1-3**Windows Server 2008 Enterprise Edition のフルインストールと Server Core インストールのサーバーロールの比較

| サーバーの役割  | フルインストールで利用可能  | Server Core で使用可能  |
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

Server Core で利用できるロールはアーキテクチャ (x86 または x64) と製品エディションに関係なく同じですが、いくつかの例外があります。
* Hyper-v (仮想化) の役割は、hyper-v 製品メディアを使用して Windows Server 2008 を購入した場合にのみ使用できます (Hyper-v は x64 バージョンでのみ使用できます)。 この役割が不要な場合は、代わりに Hyper-v 製品メディアを使用せずに Windows Server 2008 を購入できます。 
* Standard Edition のファイルサービスの役割は、1つのスタンドアロン分散ファイルシステム (dfs) ルートに制限されており、ファイル間のレプリケーション (DFS-R) はサポートされていません。 
* Server Core にストリーミング Media Services の役割をインストールする前に、サーバーのアーキテクチャ (x86 または x64) に適した Microsoft Update スタンドアロンパッケージ (.msu ファイル) を Microsoft ダウンロードセンターからダウンロードしてインストールする必要があります。
* Web サーバー (IIS) の役割は、ASP.NET をサポートしていません。 これは、.NET Framework が Server core でサポートされていないためです。これにより、Server Core Web サーバーでできることが制限されます。 

## <a name="supported-optional-features"></a>サポートされているオプション機能
また、Server Core インストールでは、Windows Server 2008 のフルインストールで利用できる機能の一部のみがサポートされます。 表1-4 では、Windows Server 2008 Enterprise Edition のフルインストールと Server Core インストールの両方で使用できる機能を比較します。

**表 1-4**Windows Server 2008 Enterprise Edition のフルインストールと Server Core インストールの機能の比較

| 機能  | フルインストールで利用可能  | Server Core で使用可能  |
| ------------- | :-------------: | :------------: |
| .NET Framework 3.0 の機能  | x  |  |
| 役割と機能の追加ウィザード  | x  | x |
| BITS サーバー拡張機能  | x  |  |
| 接続マネージャー管理キット  | x |  |
| デスクトップ エクスペリエンス  | x |  |
| フェールオーバー クラスタリング  | x  | x |
| グループ ポリシーの管理  | x  |  |
| インターネット印刷クライアント  | x  |  |
| インターネット記憶域ネームサーバー  | x  |  |
| LPR ポート モニター  | x  |  |
| メッセージ キューイング (Message Queuing)  | x  |  |
| マルチパス IO  | x  | x |
| ネットワーク負荷分散  | x  | x |
| ピア名解決プロトコル  | x  |  |
| 高品質な Windows オーディオ ビデオ エクスペリエンス  | x |  |
| リモート アシスタンス  | x  |  |
| Remote Differential Compression | x  |  |
| リモート サーバー管理ツール  | x  |  |
| リムーバブル記憶域マネージャー | x  | x |
| HTTP プロキシ経由の RPC | x  |  |
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

ここでも、Server Core で使用できる機能について理解しておく必要がある点がいくつかあります。
* 一部の機能では、サーバーコアで正しく機能するために特別なハードウェアが必要になる場合があります。 これらの機能には、BitLocker ドライブ暗号化、フェールオーバークラスタリング、マルチパス IO、ネットワーク負荷分散、リムーバブル記憶域などがあります。 
* フェールオーバークラスタリングは、Standard Edition では使用できません。

## <a name="server-core-architecture"></a>Server Core アーキテクチャ
Server Core の詳細については、Windows Server 2008 の Server Core インストールのアーキテクチャを、完全インストールと比較して簡単に説明します。 まず、Server Core は異なるバージョンの Windows Server 2008 ではなく、システムに Windows Server 2008 をインストールするときに選択できるインストールオプションであることに注意してください。 これは、次のことを意味します。
* Server Core インストール上のカーネルは、同じハードウェアアーキテクチャ (x86 または x64) とエディションのフルインストールで検出されたものと同じです。 
* Server Core インストールにバイナリが存在する場合、同じハードウェアアーキテクチャ (x86 または x64) とエディションの完全インストールには、その特定のバイナリと同じバージョンが使用されます (後で説明する2つの例外があります)。 
* 特定の設定 (特定のファイアウォールの例外、特定のサービスのスタートアップの種類など) が Server Core インストールで特定の既定の構成を持っている場合、その設定は同じ方法で完全にインストールされます。ハードウェアアーキテクチャ (x86 または x64) とエディション。

図1-3 に、完全インストールと Windows Server 2008 の Server Core インストールの両方のアーキテクチャの簡略化されたビューを示します。 点線は Server Core のアーキテクチャを示していますが、図全体は完全インストールのアーキテクチャを表しています。 

この図は、Windows Server 2008 のモジュール型アーキテクチャを示しています。 Server Core は、オペレーティングシステムのコア機能のサブセットに基づいて構築されています。 同じハードウェアアーキテクチャおよびエディションでは、Server Core のクリーンインストールに存在するすべてのファイルも完全インストール時に存在します。ただし、Server Core にのみ存在する2つの特別なファイル (Scregedit.exe と Oclist) は例外です。 これらの特別なファイルは Server core に含まれており、Server Core インストールの初期構成を簡略化し、役割とオプションコンポーネントを追加または削除しました。 

![Server Core とフルインストールのアーキテクチャ](../media/what-is-server-core-2008/Fig1-3.png)

**図 1-3**Server Core とフルインストールのアーキテクチャ

## <a name="driver-support"></a>ドライバーのサポート
図1-3 に示されている Server Core のアーキテクチャ図は、明らかに簡略化されています。ここでは、Server Core とフルインストールのデバイスドライバーのサポートの違いについて説明します。 Windows Server 2008 の完全インストールには、さまざまな種類のデバイス用のインボックスドライバーが多数含まれています。これにより、さまざまなハードウェア構成に製品をインストールできます。 (Windows Vista などのクライアントオペレーティングシステムには、デジタルカメラや、通常サーバーでは使用されていないスキャナーなどのデバイスをサポートするためのドライバーも多数含まれています。) 

新しいデバイスが Windows Server 2008 の完全インストールに接続されている (またはインストールされている) 場合は、プラグアンドプレイ (PnP) サブシステムによって、まず、デバイスのインボックスドライバーが存在するかどうかがチェックされます。 互換性のあるインボックスドライバーが見つかると、PnP サブシステムによってドライバーが自動的にインストールされ、デバイスが動作します。 Windows Server 2008 のフルインストールでは、ドライバーがインストールされていて、デバイスを使用する準備ができていることを示すバルーンポップアップ通知が表示される場合があります。 

Server Core インストールでは、ドライバーのインストールプロセスは同じです (PnP サブシステムが Server Core に存在します)。2つの要件があります。 まず、Server Core には、次の種類のデバイスについてのみ、インボックスドライバーの数が最小限に抑えられています。
* Standard Video Graphics Array (VGA) ビデオドライバー 
* 記憶装置のドライバー 
* ネットワークアダプターのドライバー

ここに示されている3つのデバイスカテゴリのそれぞれについて、Server Core には、対応する完全インストール (同じハードウェアアーキテクチャ用) にある、同じインボックスドライバーが含まれていることに注意してください。 

また、PnP サブシステムによって新しいデバイスのドライバーが自動的にインストールされるときに、自動的にインストールされます。バルーンポップアップ通知は表示されません。 表示されない Server Core には GUI がないため、タスクバーがないため、タスクバーに通知領域がありません。 

では、Server Core インストールに印刷サービスの役割を追加するときに、プリンターをインストールするにはどうすればよいでしょうか。 プリンタードライバーをサーバーに手動で追加します。 Server Core には、インボックス印刷ドライバーがありません。

## <a name="service-footprint"></a>サービスのフットプリント
Server Core は最小インストールであるため、同じハードウェアアーキテクチャとエディションの対応するフルインストールよりも、システムサービスのフットプリントが小さくなります。 たとえば、75のシステムサービスは、既定では、Windows Server 2008 の完全インストール時にインストールされます。この場合、約50は自動起動用に構成されます。 これに対して、Server Core では既定でインストールされるサービスの数は70であり、これらのサービスが自動的に起動するのは40未満です。 

表1-5 に、Server Core インストールで既定でインストールされるサービスと、各サービスによって使用されるアカウントのスタートアップモードを示します。

**表 1-5**Server Core に既定でインストールされるシステムサービス

| [サービス名]  | 表示名  | スタートアップモード  | アカウント  |
| ------------- | ------------- | ------------ | ------------ |
| AeLookupSvc  | アプリケーションエクスペリエンス  | Auto | LocalSystem |
| AppMgmt  | アプリケーション管理  | 手動 | LocalSystem |
| BFE | ベース フィルター エンジン  | Auto | LocalService |
| BITS | バックグラウンド インテリジェント転送サービス  | Auto | LocalSystem |
| ブラウザー | コンピューター ブラウザー  | 手動 | LocalSystem |
| CertPropSvc | 証明書伝達  | 手動 | LocalSystem |
| COMSysApp  | COM+ System Application  | 手動 | LocalSystem |
| CryptSvc  | 暗号化サービス  | Auto | ネットワークサービス |
| DcomLaunch  | DCOM Server Process Launcher  | Auto | LocalSystem |
| DHCP  | DHCP クライアント  | Auto | LocalService |
| Dnscache | DNS クライアント  | Auto | ネットワークサービス |
| DPS  | 診断ポリシー サービス  | Auto | LocalService |
| ログ | Windows イベント ログ  | Auto | LocalService |
| EventSystem  | COM+ イベント システム  | Auto | LocalService |
| FCRegSvc  | Microsoft ファイバーチャネル Platform Registration Service  | 手動 | LocalService |
| gpsvc  | グループ ポリシー クライアント  | Auto | LocalSystem |
| hidserv | ヒューマンインターフェイスデバイスアクセス  | 手動 | LocalSystem |
| hkmsvc  | 正常性キーと証明書の管理  | 手動 | LocalSystem |
| IKEEXT  | IKE および AuthIP IPsec のキー モジュール  | Auto | LocalSystem |
| iphlpsvc  | IP ヘルパー  | Auto | LocalSystem |
| KeyIso | CNG キーの分離  | 手動 | LocalSystem |
| KtmRm  | 分散トランザクション コーディネーター向け KtmRm  | Auto | ネットワークサービス |
| LanmanServer  | Server  | Auto | LocalSystem |
| LanmanWorkstation  | Workstatione  | Auto | LocalService |
| lltdsvc  | Link-Layer Topology Discovery Mapper  | 手動 | LocalService |
| lmhosts  | TCP/IP NetBIOS ヘルパー  | Auto | LocalService |
| MpsSvc  | Windows ファイアウォール  | Auto | LocalService |
| MSDTC  | 分散トランザクション コーディネーター  | Auto | ネットワークサービス |
| MSiSCSI  | Microsoft iSCSI イニシエーター サービス  | 手動 | LocalSystem |
| msiserver  | Windows インストーラー  | 手動 | LocalSystem |
| napagent  | ネットワーク アクセス保護エージェント  | 手動 | ネットワークサービス |
| Netlogon  | Netlogon  | 手動 | LocalSystem |
| netprofm  | Network List Service  | Auto | LocalService |
| NlaSvc  | Network Location Awareness  | Auto | ネットワークサービス |
| nsi  | Network Store Interface Service  | Auto | LocalService |
| pla  | パフォーマンス ログと警告  | 手動 | LocalService |
| PlugPlay  | プラグ アンド プレイ  | Auto | LocalSystem |
| PolicyAgent  | IPSec ポリシー エージェント  | Auto | ネットワークサービス |
| ProfSvc  | ユーザー プロファイル サービス  | Auto | LocalSystem |
| ProtectedStorage  | 保護された記憶域  | 手動 | LocalSystem |
| RemoteRegistry  | リモート レジストリ  | Auto | LocalService |
| RpcSs  | リモート プロシージャ コール (RPC)  | Auto | ネットワークサービス |
| RSoPProv | Resultant Set of Policy Provider  | 手動 | LocalSystem |
| sacsvr  | Special Administration Console Helper  | 手動 | LocalSystem |
| SamSs  | セキュリティ アカウント マネージャー  | Auto | LocalSystem |
| SCardSvr | スマート カード  | 手動 | LocalService |
| [スケジュール] | タスク スケジューラ  | Auto | LocalSystem |
| SCPolicySvc | スマート カードの取り出しポリシー  | 手動 | LocalSystem |
| seclogon | セカンダリ ログオン  | Auto | LocalSystem |
| SENS | システム イベント通知サービス  | Auto | LocalSystem |
| SessionEnv | ターミナル サービス構成  | 手動 | LocalSystem |
| slsvc  | ソフトウェア ライセンス | Auto | ネットワークサービス |
| SNMPTRAP  | SNMP トラップ  | 手動 | LocalService |
| swprv  | Microsoft Software Shadow Copy Provider | 手動 | LocalSystem |
| TBS | TPM 基本サービス  | 手動 | LocalService |
| TermService  | Terminal Services | Auto | ネットワークサービス |
| TrustedInstaller | Windows Modules Installer  | Auto | LocalSystem |
| UmRdpService | ターミナルサービスのモードポートリダイレクター  | 手動 | LocalSystem |
| vds | 仮想ディスク  | 手動 | LocalSystem |
| VSS | ボリューム シャドウ コピー  | 手動 | LocalSystem |
| W32Time | Windows タイム  | Auto | LocalService |
| WcsPlugInService  | Windows カラー システム  | 手動 | LocalService |
| WdiServiceHost  | Diagnostic Service Host  | 手動 | LocalService |
| WdiSystemHost  | 診断システム ホスト  | 手動 | LocalSystem |
| Wecsvc | Windows イベント コレクター  | 手動 | ネットワークサービス |
| WinHttpAuto-ProxySvc  | WinHTTP Web プロキシ自動発見サービス  | Auto | LocalService |
| Winmgmt | Windows Management Instrumentation (Windows Management Instrumentation) | Auto | LocalSystem |
| WinRM  | Windows リモート管理 (WS-Management) | Auto | ネットワークサービス |
| wmiApSrv  | WMI Performance Adapter  | 手動 | LocalSystem |
| wuauserv | Windows Update | Auto | LocalSystem |