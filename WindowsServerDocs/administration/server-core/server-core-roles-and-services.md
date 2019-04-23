---
title: 役割、役割サービス、および Windows Server の Server Core に含まれる機能
description: Windows Server の Server Core インストール オプションでは、どのような役割と機能が含まれますか。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859293"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>役割、役割サービス、および Windows Server の Server Core に含まれる機能

> 適用対象:Windows Server (半期チャネル) および Windows Server 2016

について話す通常[何の*いない*Server Core で](server-core-removed-roles.md)を別のアプローチを試して、何かを指示するメッセージが表示しましょう - の*に含まれる*があるかどうかと*既定でインストールされている*します。 次の役割、役割サービス、および機能は*で*Windows Server の Server Core インストール オプションです。 環境内の Server Core オプションの動作はかどうかを把握するのにには、この情報を使用します。 これは大きなリストであるため、検討の特定のロールまたは検索では、何を探している返されない場合に該当する機能の検索は、Server Core には含まれません。

たとえば、"Remote Desktop Session Host"- 検索する場合は、このページで検出されません。 RD セッション ホストが、Server Core イメージに含まれていないためにです。

注意してください。[常に検索](server-core-removed-roles.md)どのの*いない*に含まれます。 これは、ことを確認する別の方法だけです。

## <a name="roles-included-in-server-core"></a>Server Core の役割
Server Core インストール オプションには、次のサーバーの役割が含まれています。

| ロール                                            | 名前                           | 既定でインストールされているか。 |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 証明書サービス           | 証明書の AD                 | N                     |
| Active Directory Domain Services                | AD-Domain-Services             | N                     |
| Active Directory フェデレーション サービス (AD FS)            | ADFS フェデレーション                | N                     |
| Active Directory ライトウェイト ディレクトリ サービス | ADLDS                          | N                     |
| Active Directory Rights Management サービス     | ADRMS                          | N                     |
| デバイス正常性構成証明                       | DeviceHealthAttestationService | N                     |
| DHCP サーバー                                     | DHCP                           | N                     |
| DNS サーバー                                      | DNS                            | N                     |
| ファイル サービスおよび記憶域サービス                       | FileAndStorage サービス        | Y                     |
| ホスト ガーディアン サービス                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 印刷とドキュメント サービス                     | 印刷サービス                 | N                     |
| リモート アクセス                                   | リモート アクセス                   | N                     |
| リモート デスクトップ サービス                         | リモート デスクトップのサービス        | N                     |
| ボリューム ライセンス認証サービス                      | VolumeActivation               | N                     |
| IIS web サーバー                                  | Web サーバー                     | N                     |
| Windows Server Essentials エクスペリエンス            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core に含まれる役割サービス
Server Core インストール オプションには、次の役割サービスが含まれています。

| ロール                                  | 役割サービス                                                   | 名前                    | 既定でインストールされているか。 |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 証明書サービス | 証明機関                                        | ADCS-証明書の機関     | N                     |
|                                       | 証明書の登録ポリシー Web サービス                      | ADCS-登録-Web-Pol     | N                     |
|                                       | 証明書の登録 Web サービス                             | ADCS-Enroll-Web-Svc     | N                     |
|                                       | 証明機関 Web 登録                         | ADCS Web 登録     | N                     |
|                                       | ネットワーク デバイス登録サービス                              | ADCS デバイス登録  | N                     |
|                                       | オンライン レスポンダー                                               | ADCS オンライン Cert        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management サーバー                      | ADRMS サーバー            | N                     |
|                                       | ID フェデレーション サポート                                    | Adrms-identity          | N                     |
| ファイル サービスおよび記憶域サービス             | ファイル サービスおよび iSCSI サービス                                        | ファイル サービス           | N                     |
|                                       | ファイル サーバー                                                    | FS FileServer           | N                     |
|                                       | ネットワーク ファイル用 BranchCache                                  | FS BranchCache          | N                     |
|                                       | データ重複除去                                             | FS 除去   | N                     |
|                                       | DFS 名前空間                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS レプリケーション                                                | FS DFS レプリケーション      | N                     |
|                                       | ファイル サーバー リソース マネージャー                                   | FS-Resource Manager     | N                     |
|                                       | ファイル サーバー VSS エージェント サービス                                  | FS VSS-エージェント            | N                     |
|                                       | iSCSI ターゲット サーバー                                            | iSCSITarget サーバー      | N                     |
|                                       | iSCSI ターゲット記憶域プロバイダー (VDS および VSS ハードウェア プロバイダー) | iSCSITarget-VSS の VDS     | N                     |
|                                       | NFS サーバー                                                 | FS-NFS サービス          | N                     |
|                                       | ワーク フォルダー                                                   | FS SyncShareService     | N                     |
|                                       | 記憶域サービス                                               | 記憶域サービス        | Y                     |
| 印刷とドキュメント サービス           | プリント サーバー                                                   | プリント サーバー            | N                     |
|                                       | LPD サービス                                                    | 印刷-LPD サービス       | N                     |
| リモート アクセス                         | DirectAccess と VPN (RAS)                                     | DirectAccess VPN        | N                     |
|                                       | ルーティング                                                        | ルーティング                 | N                     |
|                                       | Web アプリケーション プロキシ                                          | Web アプリケーション プロキシ   | N                     |
| リモート デスクトップ サービス               | リモート デスクトップ接続ブローカー                               | RDS-接続ブローカー   | N                     |
|                                       | リモート デスクトップ ライセンス                                       | RDS ライセンス           | N                     |
|                                       | リモート デスクトップ仮想化ホスト                             | RDS の仮想化      | N                     |
| Web サーバー (IIS)                      | Web サーバー                                                     | Web サーバーの web           | N                     |
|                                       | 一般的な HTTP 機能                                           | 一般的な Http-web         | N                     |
|                                       | 既定のドキュメント                                               | Web の既定のドキュメント         | N                     |
|                                       | ディレクトリの参照                                             | Web ディレクトリ参照        | N                     |
|                                       | HTTP エラー                                                    | Web Http-エラー         | N                     |
|                                       | 静的コンテンツ                                                 | Web 静的コンテンツ      | N                     |
|                                       | HTTP リダイレクト                                               | Web Http のリダイレクト       | N                     |
|                                       | Webdav 発行                                              | Web DAV 発行      | N                     |
|                                       | 正常性と診断                                         | Web ヘルス              | N                     |
|                                       | HTTP ログ                                                   | Web Http ログ記録        | N                     |
|                                       | カスタム ログ                                                 | Web のカスタム ログの記録      | N                     |
|                                       | ログ ツール                                                  | Web ログ-ライブラリ       | N                     |
|                                       | ODBC ログ                                                   | Web の ODBC ログの記録        | N                     |
|                                       | 要求監視                                              | Web 要求のモニター     | N                     |
|                                       | トレース                                                        | Http トレースの web        | N                     |
|                                       | パフォーマンス                                                    | Web パフォーマンス         | N                     |
|                                       | 静的コンテンツの圧縮                                     | Web の圧縮状態    | N                     |
|                                       | 動的なコンテンツの圧縮                                    | Web の圧縮 Dyn     | N                     |
|                                       | セキュリティ                                                       | Web セキュリティ            | N                     |
|                                       | Request Filtering                                              | Web フィルター処理           | N                     |
|                                       | 基本認証                                           | Web Basic-認証          | N                     |
|                                       | 一元化された SSL 証明書のサポート                            | Web CertProvider        | N                     |
|                                       | クライアント証明書マッピング認証                      | Web クライアントの認証         | N                     |
|                                       | ダイジェスト認証                                          | Web ダイジェストの認証         | N                     |
|                                       | IIS クライアント証明書マッピング認証                  | Web 証明書の認証           | N                     |
|                                       | IP およびドメインの制限                                     | Web IP セキュリティ         | N                     |
|                                       | URL 承認                                              | Web Url の認証            | N                     |
|                                       | [Windows 認証]                                         | Windows-認証 web        | N                     |
|                                       | アプリケーションの開発                                        | Web アプリの開発             | N                     |
|                                       | .NET 拡張機能 3.5                                         | Web-Net-Ext             | N                     |
|                                       | .NET 拡張機能 4.6                                         | Web-Net-Ext45           | N                     |
|                                       | Application Initialization                                     | Web AppInit             | N                     |
|                                       | ASP                                                            | Web ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Web-Asp-Net45           | N                     |
|                                       | CGI                                                            | Web CGI                 | N                     |
|                                       | ISAPI 拡張機能                                               | Web-ISAPI の拡張           | N                     |
|                                       | ISAPI Filters                                                  | ISAPI-フィルターが web        | N                     |
|                                       | サーバー側インクルードします。                                           | Web が含まれています            | N                     |
|                                       | WebSocket プロトコル                                             | Web Websocket          | N                     |
|                                       | FTP サーバー                                                     | Web から Ftp サーバー          | N                     |
|                                       | FTP サービス                                                    | Web、Ftp サービス         | N                     |
|                                       | FTP 機能拡張                                              | Web、Ftp-Ext             | N                     |
|                                       | 管理ツール                                               | Web 管理-ツール          | N                     |
|                                       | IIS 6 管理互換                                 | Web の互換性の管理         | N                     |
|                                       | IIS 6 メタベース互換                                   | Web メタベース            | N                     |
|                                       | IIS 6 スクリプト ツール                                          | Web Lgcy スクリプト      | N                     |
|                                       | IIS 6 WMI 互換                                        | Web WMI                 | N                     |
|                                       | IIS 管理スクリプトおよびツール                               | Web スクリプト ツール     | N                     |
|                                       | 管理サービス                                             | Web 管理サービス        | N                     |
| Windows Server Update Services        | WID 接続                                               | UpdateServices WidDB    | N                     |
|                                       | WSUS サービス                                                  | UpdateServices サービス | N                     |
|                                       | SQL Server 接続                                        | UpdateServices DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core に含まれる機能
Server Core インストール オプションには、次の機能が含まれています。

| 機能                                                | 名前                               | 既定でインストールされているか。 |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET framework 3.5 の機能                            | NET Framework の機能             | N                     |
| .NET framework 3.5 (.NET 2.0 および 3.0 を含む)       | NET Framework-コア                 | (削除)             |
| HTTP アクティブ化                                        | NET HTTP アクティブ化                | N                     |
| 非 HTTP アクティブ化                                    | NET-非-HTTP のアクティブな                 | N                     |
| .NET framework 4.6 の機能                            | NET Framework-45 機能          | Y                     |
| .NET Framework 4.6                                     | NET Framework-45 Core              | Y                     |
| ASP.NET 4.6                                            | NET-Framework-45-ASPNET            | N                     |
| WCF サービス                                           | NET-WCF-Services45                 | Y                     |
| HTTP アクティブ化                                        | NET WCF HTTP Activation45          | N                     |
| メッセージ キュー (MSMQ) アクティブ化                      | NET WCF MSMQ Activation45          | N                     |
| 名前付きパイプのアクティブ化                                  | NET WCF パイプ Activation45          | N                     |
| TCP のアクティブ化                                         | NET WCF TCP Activation45           | N                     |
| TCP ポート共有                                       | NET-WCF-TCP-PortSharing45          | Y                     |
| バックグラウンド インテリジェント転送サービス (BITS)         | BITS                               | N                     |
| コンパクト サーバー                                         | BITS コンパクト-サーバー                | N                     |
| 役割と機能の追加ウィザード                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS クライアント                                         | NFS クライアント                         | N                     |
| コンテナー                                             | コンテナー                         | N                     |
| データ センター ブリッジング                                   | データ センター ブリッジング               | N                     |
| 拡張記憶域                                       | EnhancedStorage                    | N                     |
| フェールオーバー クラスタリング                                    | フェールオーバー クラスタ リング                | N                     |
| グループ ポリシーの管理                                | GPMC                               | N                     |
| サービスの I/O 品質                                 | DiskIo QoS                         | N                     |
| IIS ホスト可能な Web コア                                  | Web WHC                            | N                     |
| IP アドレス管理 (IPAM) サーバー                    | IPAM                               | N                     |
| iSNS サーバー サービス                                    | ISNS                               | N                     |
| Management OData IIS 拡張機能                         | ManagementOdata                    | N                     |
| メディア ファンデーション                                       | サーバーのメディアの基盤            | N                     |
| メッセージ キューイング (Message Queuing)                                        | MSMQ (MSMQ)                               | N                     |
| メッセージ キュー サービス                               | MSMQ サービス                      | N                     |
| メッセージ キュー サーバー                                 | MSMQ サーバー                        | N                     |
| ディレクトリ サービス統合                          | MSMQ ディレクトリ                     | N                     |
| HTTP サポート                                           | MSMQ HTTP のサポート                  | N                     |
| メッセージ キュー トリガー                               | MSMQ トリガー                      | N                     |
| ルーティング サービス                                        | MSMQ ルーティング                       | N                     |
| メッセージ キュー DCOM プロキシ                             | MSMQ DCOM                          | N                     |
| マルチパス I/O                                          | マルチパス IO                       | N                     |
| MultiPoint Connector                                   | MultiPoint-Connector               | N                     |
| MultiPoint コネクタ サービス                          | Multipoint コネクタ      | N                     |
| MultiPoint マネージャーと MultiPoint ダッシュ ボード            | MultiPoint ツール                   | N                     |
| ネットワーク負荷分散                                 | NLB                                | N                     |
| ピア名解決プロトコル                          | PNRP                               | N                     |
| 高品質な Windows オーディオ ビデオ エクスペリエンス                 | qWave                              | N                     |
| Remote Differential Compression                        | RDC                                | N                     |
| リモート サーバー管理ツール                     | RSAT                               | N                     |
| 機能管理ツール                           | RSAT-機能-ツール                 | N                     |
| BitLocker ドライブ暗号化管理ユーティリティ  | RSAT 機能ツール BitLocker       | N                     |
| DataCenterBridging LLDP ツール                          | RSAT DataCenterBridging LLDP ツール | N                     |
| フェールオーバー クラスタリング ツール                              | Rsat-clustering                    | N                     |
| Windows PowerShell 用フェールオーバー クラスター モジュール         | RSAT クラスタ リング PowerShell         | N                     |
| フェールオーバー クラスター自動化サーバー                     | RSAT クラスタ リング AutomationServer   | N                     |
| フェールオーバー クラスター コマンド インターフェイス                     | RSAT クラスタ リング CmdInterface       | N                     |
| IP アドレス管理 (IPAM) クライアント                    | IPAM クライアントの機能                | N                     |
| シールドされた VM ツール                                      | RSAT の影響を受けません-VM-ツール             | N                     |
| Windows PowerShell 用記憶域レプリカ モジュール          | RSAT の記憶域レプリカ               | N                     |
| 役割管理ツール                              | RSAT のツールの役割                    | N                     |
| AD DS および AD LDS ツール                                 | RSAT AD-ツール                      | N                     |
| Windows PowerShell 用 Active Directory モジュール         | RSAT AD-PowerShell                 | N                     |
| AD DS ツール                                            | RSAT 追加                          | N                     |
| Active Directory 管理センター                 | RSAT-AD-AdminCenter                | N                     |
| AD DS スナップインおよびコマンドライン ツール                  | RSAT 追加ツール                    | N                     |
| AD LDS スナップインおよびコマンド ライン ツール                 | RSAT ADLDS                         | N                     |
| Hyper-V 管理ツール                               | RSAT ハイパー-V のツール                 | N                     |
| Windows PowerShell 用 Hyper-V モジュール                  | Hyper-V の PowerShell                 | N                     |
| Windows Server Update Services ツール                   | UpdateServices RSAT                | N                     |
| API と PowerShell コマンドレット                             | UpdateServices API                 | N                     |
| DHCP サーバー ツール                                      | RSAT DHCP                          | N                     |
| DNS サーバー ツール                                       | RSAT から DNS サーバー                    | N                     |
| リモート アクセス管理ツール                         | RSAT RemoteAccess                  | N                     |
| Windows PowerShell 用のリモート アクセス モジュール            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC over HTTP プロキシ                                    | RPC over HTTP プロキシ                | N                     |
| セットアップおよびブート イベント収集                        | セットアップ-と-ブート-イベントの収集    | N                     |
| Simple TCP/IP Services                                 | 単純な TCPIP                       | N                     |
| SMB 1.0/CIFS ファイル共有のサポート                      | FS-SMB1                            | Y                     |
| SMB 帯域幅の制限                                    | FS SMBBW                           | N                     |
| SNMP サービス                                           | SNMP サービス                       | N                     |
| WMI SNMP プロバイダー                                      | WMI SNMP-プロバイダー                  | N                     |
| Telnet クライアント                                          | Telnet クライアント                      | N                     |
| Fabric Management 用の VM シールド ツール               | FabricShieldedTools                | N                     |
| Windows Defender の機能                              | Windows Defender の機能          | Y                     |
| Windows Defender                                       | Windows Defender                   | Y                     |
| Windows Internal Database                              | Windows Internal Database          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 エンジン                          | PowerShell-V2                      | (削除)             |
| Windows PowerShell Desired State Configuration サービス | DSC サービス                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Windows プロセス アクティブ化サービス                     | が                                | N                     |
| プロセス モデル                                          | プロセス モデル                  | N                     |
| .NET 環境 3.5                                   | NET 環境                | N                     |
| 構成 API                                     | 構成 Api                    | N                     |
| Windows Server バックアップ                                  | Windows Server のバックアップ              | N                     |
| Windows Server 移行ツール                         | Migration                          | N                     |
| Windows 標準ベースの記憶域の管理             | WindowsStorageManagementService    | N                     |
| WinRM IIS 拡張機能                                    | WinRM IIS (内線)                      | N                     |
| WINS サーバー                                            | WINS                               | N                     |
| WoW64 サポート                                          | WoW64 サポート                      | Y                     |
|                                                        |                                    |                       |
