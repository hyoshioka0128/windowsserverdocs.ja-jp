---
title: Windows Server-Server Core に含まれる役割、役割サービス、および機能
description: Windows Server の Server Core インストールオプションにはどのような役割と機能が含まれていますか。
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 7b5d5d5ad38b1b03e409c26485860f43799f1322
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383330"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Windows Server-Server Core に含まれる役割、役割サービス、および機能

> 適用対象:Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

通常、 [Server Core では*ないこと*](server-core-removed-roles.md)について説明します。ここでは、別のアプローチを試して、*含まれ*ているものと、既定で何かが*インストールさ*れているかどうかを確認します。 次の役割、役割サービス、および機能は、Windows Server の Server Core インストールオプション*に含ま*れています。 この情報は、お使いの環境で Server Core オプションが機能するかどうかを判断するのに役立ちます。 これは大きなリストなので、関心のある特定の役割または機能を検索することを検討してください。探しているものが見つからない場合、Server Core には含まれていません。

たとえば、"リモートデスクトップセッションホスト" を検索すると、このページには見つかりません。 これは、RD セッションホストが Server Core イメージに含まれていないためです。

何も含まれて*いない*ことを[常に確認](server-core-removed-roles.md)できることに注意してください。 これは、何かを確認するための別の方法にすぎません。

## <a name="roles-included-in-server-core"></a>Server Core に含まれる役割
Server Core インストールオプションには、次のサーバーの役割があります。

| ロール                                            | 名前                           | 既定でインストールされますか? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 証明書サービス           | 証明書の AD                 | N                     |
| Active Directory Domain Services                | AD ドメインサービス             | N                     |
| Active Directory フェデレーション サービス (AD FS)            | ADFS-フェデレーション                | N                     |
| Active Directory ライトウェイト ディレクトリ サービス | ADLDS                          | N                     |
| Active Directory Rights Management サービス     | ADRMS                          | N                     |
| デバイス正常性構成証明                       | DeviceHealthAttestationService | N                     |
| DHCP サーバー                                     | DHCP                           | N                     |
| DNS サーバー                                      | DNS                            | N                     |
| ファイル サービスおよび記憶域サービス                       | FileAndStorage-サービス        | Y                     |
| ホスト ガーディアン サービス                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 印刷とドキュメント サービス                     | 印刷サービス                 | N                     |
| リモート アクセス                                   | RemoteAccess                   | N                     |
| リモート デスクトップ サービス                         | リモート デスクトップのサービス        | N                     |
| ボリューム ライセンス認証サービス                      | VolumeActivation               | N                     |
| Web サーバー IIS                                  | Web サーバー                     | N                     |
| Windows Server Essentials エクスペリエンス            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | Updateservices-api                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core に含まれる役割サービス
Server Core インストールオプションには、次の役割サービスが含まれています。

| ロール                                  | 役割サービス                                                   | 名前                    | 既定でインストールされますか? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 証明書サービス | 証明機関                                        | ADCS-証明書の機関     | N                     |
|                                       | 証明書の登録ポリシー Web サービス                      | ADCS-Web-Registry.pol     | N                     |
|                                       | 証明書の登録 Web サービス                             | ADCS-Web-Svc     | N                     |
|                                       | 証明機関 Web 登録                         | ADCS-Web 登録     | N                     |
|                                       | ネットワーク デバイス登録サービス                              | ADCS-デバイス-登録  | N                     |
|                                       | オンライン レスポンダー                                               | ADCS-Cert        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management サーバー                      | ADRMS-サーバー            | N                     |
|                                       | ID フェデレーション サポート                                    | ADRMS-Id          | N                     |
| ファイル サービスおよび記憶域サービス             | ファイル サービスおよび iSCSI サービス                                        | ファイル サービス           | N                     |
|                                       | ファイル サーバー                                                    | FS FileServer           | N                     |
|                                       | ネットワーク ファイル用 BranchCache                                  | FS-BranchCache          | N                     |
|                                       | データ重複除去                                             | FS-データ-重複除去   | N                     |
|                                       | DFS 名前空間                                                 | FS-DFS 名前空間        | N                     |
|                                       | DFS レプリケーション                                                | FS-DFS レプリケーション      | N                     |
|                                       | ファイル サーバー リソース マネージャー                                   | FS-リソースマネージャー     | N                     |
|                                       | ファイル サーバー VSS エージェント サービス                                  | FS VSS-エージェント            | N                     |
|                                       | iSCSI ターゲット サーバー                                            | iSCSITarget-サーバー      | N                     |
|                                       | iSCSI ターゲット記憶域プロバイダー (VDS および VSS ハードウェアプロバイダー) | iSCSITarget-VDS     | N                     |
|                                       | NFS サーバー                                                 | NFS-サービス          | N                     |
|                                       | ワーク フォルダー                                                   | FS 同期サービス     | N                     |
|                                       | 記憶域サービス                                               | ストレージ-サービス        | Y                     |
| 印刷とドキュメント サービス           | プリント サーバー                                                   | プリントサーバー            | N                     |
|                                       | LPD サービス                                                    | 印刷-LPD-サービス       | N                     |
| リモート アクセス                         | DirectAccess と VPN (RAS)                                     | DirectAccess VPN        | N                     |
|                                       | ルーティング                                                        | ルーティング                 | N                     |
|                                       | Web アプリケーション プロキシ                                          | Web アプリケーション-プロキシ   | N                     |
| リモート デスクトップ サービス               | リモート デスクトップ接続ブローカー                               | RDS-接続-ブローカー   | N                     |
|                                       | リモート デスクトップ ライセンス                                       | RDS-ライセンス           | N                     |
|                                       | リモート デスクトップ仮想化ホスト                             | RDS-仮想化      | N                     |
| Web サーバー (IIS)                      | Web サーバー                                                     | Web サーバーの web           | N                     |
|                                       | 一般的な HTTP 機能                                           | 一般的な Http-web         | N                     |
|                                       | 既定のドキュメント                                               | Web の既定のドキュメント         | N                     |
|                                       | ディレクトリの参照                                             | Web ディレクトリ参照        | N                     |
|                                       | HTTP エラー                                                    | Web Http-エラー         | N                     |
|                                       | 静的コンテンツ                                                 | Web 静的コンテンツ      | N                     |
|                                       | HTTP リダイレクト                                               | Web Http のリダイレクト       | N                     |
|                                       | WebDAV 発行                                              | Web DAV 発行      | N                     |
|                                       | 正常性と診断                                         | Web ヘルス              | N                     |
|                                       | HTTP ログ                                                   | Web Http ログ記録        | N                     |
|                                       | カスタムログ                                                 | Web のカスタム ログの記録      | N                     |
|                                       | ログツール                                                  | Web ログ-ライブラリ       | N                     |
|                                       | ODBC のログ記録                                                   | Web の ODBC ログの記録        | N                     |
|                                       | 要求モニター                                              | Web 要求のモニター     | N                     |
|                                       | トレース                                                        | Web-Http-トレース        | N                     |
|                                       | パフォーマンス                                                    | Web パフォーマンス         | N                     |
|                                       | 静的なコンテンツの圧縮                                     | Web の圧縮状態    | N                     |
|                                       | 動的なコンテンツの圧縮                                    | Web の圧縮 Dyn     | N                     |
|                                       | セキュリティ                                                       | Web セキュリティ            | N                     |
|                                       | Request Filtering                                              | Web フィルター処理           | N                     |
|                                       | 基本認証                                           | Web Basic-認証          | N                     |
|                                       | 一元化された SSL 証明書のサポート                            | Web CertProvider        | N                     |
|                                       | クライアント証明書マッピング認証                      | Web クライアントの認証         | N                     |
|                                       | ダイジェスト認証                                          | Web ダイジェストの認証         | N                     |
|                                       | IIS クライアント証明書マッピング認証                  | Web 証明書の認証           | N                     |
|                                       | IP とドメインの制限                                     | Web IP セキュリティ         | N                     |
|                                       | URL 承認                                              | Web Url の認証            | N                     |
|                                       | [Windows 認証]                                         | Windows-認証 web        | N                     |
|                                       | アプリケーションの開発                                        | Web アプリの開発             | N                     |
|                                       | .NET 拡張3.5                                         | Web-Net-Ext             | N                     |
|                                       | .NET 拡張4.6                                         | Ext45           | N                     |
|                                       | Application Initialization                                     | Web AppInit             | N                     |
|                                       | ASP                                                            | Web-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Net45           | N                     |
|                                       | CGI                                                            | Web CGI                 | N                     |
|                                       | ISAPI 拡張機能                                               | Web-ISAPI の拡張           | N                     |
|                                       | ISAPI Filters                                                  | ISAPI-フィルターが web        | N                     |
|                                       | サーバー側インクルード                                           | Web が含まれています            | N                     |
|                                       | WebSocket プロトコル                                             | Web Websocket          | N                     |
|                                       | FTP サーバー                                                     | Web-Ftp サーバー          | N                     |
|                                       | FTP サービス                                                    | Web-Ftp サービス         | N                     |
|                                       | FTP 拡張                                              | Web-Ftp-Ext             | N                     |
|                                       | 管理ツール                                               | Web 管理ツール          | N                     |
|                                       | IIS 6 管理互換                                 | Web の互換性の管理         | N                     |
|                                       | IIS 6 メタベース互換                                   | Web メタベース            | N                     |
|                                       | IIS 6 スクリプトツール                                          | Lgcy-スクリプト      | N                     |
|                                       | IIS 6 WMI 互換性                                        | Web-WMI                 | N                     |
|                                       | IIS 管理スクリプトおよびツール                               | Web スクリプト-ツール     | N                     |
|                                       | 管理サービス                                             | Web 管理サービス        | N                     |
| Windows Server Update Services        | WID 接続                                               | UpdateServices-WidDB    | N                     |
|                                       | WSUS サービス                                                  | UpdateServices-サービス | N                     |
|                                       | SQL Server 接続                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core に含まれる機能
Server Core インストールオプションには、次の機能があります。

| 機能                                                | 名前                               | 既定でインストールされますか? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5 の機能                            | .NET-フレームワーク-機能             | N                     |
| .NET Framework 3.5 (.NET 2.0 と3.0 を含む)       | NET-フレームワーク-コア                 | 状態             |
| HTTP アクティブ化                                        | NET-HTTP-アクティブ化                | N                     |
| 非 HTTP アクティブ化                                    | NET-アクティブな                 | N                     |
| .NET Framework 4.6 の機能                            | .NET-フレームワーク-45-機能          | Y                     |
| .NET Framework 4.6                                     | .NET-フレームワーク-45-コア              | Y                     |
| ASP.NET 4.6                                            | .NET-フレームワーク-45-ASPNET            | N                     |
| WCF サービス                                           | Services45                 | Y                     |
| HTTP アクティブ化                                        | NET-Activation45          | N                     |
| メッセージキュー (MSMQ) のアクティブ化                      | NET-Activation45          | N                     |
| 名前付きパイプのアクティブ化                                  | NET-Activation45          | N                     |
| TCP アクティベーション                                         | NET-Activation45           | N                     |
| TCP ポート共有                                       | NET-PortSharing45          | Y                     |
| バックグラウンド インテリジェント転送サービス (BITS)         | BITS                               | N                     |
| コンパクト サーバー                                         | BITS-Compact サーバー                | N                     |
| 役割と機能の追加ウィザード                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS クライアント                                         | NFS-クライアント                         | N                     |
| コンテナー                                             | コンテナー                         | N                     |
| データ センター ブリッジング                                   | データセンターブリッジング               | N                     |
| 拡張記憶域                                       | EnhancedStorage                    | N                     |
| フェールオーバー クラスタリング                                    | フェールオーバー-クラスタリング                | N                     |
| グループ ポリシーの管理                                | GPMC                               | N                     |
| サービスの I/O 品質                                 | DiskIo-QoS                         | N                     |
| IIS ホスト可能な Web コア                                  | Web-WHC                            | N                     |
| IP アドレス管理 (IPAM) サーバー                    | IPAM                               | N                     |
| iSNS サーバー サービス                                    | IS                               | N                     |
| Management OData IIS 拡張機能                         | ManagementOdata                    | N                     |
| メディア ファンデーション                                       | サーバーのメディアの基盤            | N                     |
| メッセージ キューイング (Message Queuing)                                        | MSMQ (MSMQ)                               | N                     |
| メッセージキューサービス                               | MSMQ-サービス                      | N                     |
| メッセージキューサーバー                                 | MSMQ-サーバー                        | N                     |
| ディレクトリ サービス統合                          | MSMQ-ディレクトリ                     | N                     |
| HTTP サポート                                           | MSMQ-HTTP サポート                  | N                     |
| メッセージキュートリガー                               | MSMQ-トリガー                      | N                     |
| ルーティングサービス                                        | MSMQ-ルーティング                       | N                     |
| メッセージ キュー DCOM プロキシ                             | MSMQ DCOM                          | N                     |
| マルチパス I/O                                          | マルチパス-IO                       | N                     |
| MultiPoint Connector                                   | MultiPoint-コネクタ               | N                     |
| MultiPoint コネクタサービス                          | MultiPoint-コネクタ-サービス      | N                     |
| MultiPoint マネージャーと MultiPoint ダッシュボード            | MultiPoint-ツール                   | N                     |
| ネットワーク負荷分散                                 | NLB                                | N                     |
| ピア名解決プロトコル                          | PNRP                               | N                     |
| 高品質な Windows オーディオ ビデオ エクスペリエンス                 | qWave                              | N                     |
| Remote Differential Compression                        | RDC                                | N                     |
| リモート サーバー管理ツール                     | RSAT                               | N                     |
| 機能管理ツール                           | RSAT-機能ツール                 | N                     |
| BitLocker ドライブ暗号化管理ユーティリティ  | RSAT 機能ツール BitLocker       | N                     |
| DataCenterBridging LLDP ツール                          | RSAT-DataCenterBridging-LLDP-ツール | N                     |
| フェールオーバー クラスタリング ツール                              | RSAT-クラスタリング                    | N                     |
| Windows PowerShell 用フェールオーバークラスターモジュール         | RSAT クラスタ リング PowerShell         | N                     |
| フェールオーバークラスターオートメーションサーバー                     | RSAT クラスタ リング AutomationServer   | N                     |
| フェールオーバークラスターコマンドインターフェイス                     | RSAT クラスタ リング CmdInterface       | N                     |
| IP アドレス管理 (IPAM) クライアント                    | IPAM-クライアント機能                | N                     |
| シールドされた VM ツール                                      | RSAT の影響を受けません-VM-ツール             | N                     |
| Windows PowerShell 用記憶域レプリカモジュール          | RSAT-ストレージ-レプリカ               | N                     |
| 役割管理ツール                              | RSAT-ロールツール                    | N                     |
| AD DS および AD LDS ツール                                 | RSAT AD-ツール                      | N                     |
| Windows PowerShell 用 Active Directory モジュール         | RSAT AD-PowerShell                 | N                     |
| AD DS ツール                                            | RSAT 追加                          | N                     |
| Active Directory 管理センター                 | RSAT-AD-AdminCenter                | N                     |
| AD DS スナップインおよびコマンドライン ツール                  | RSAT 追加ツール                    | N                     |
| スナップインとコマンドラインツールの AD LDS                 | RSAT ADLDS                         | N                     |
| Hyper-V 管理ツール                               | RSAT-Hyper-v ツール                 | N                     |
| Windows PowerShell 用 Hyper-V モジュール                  | Hyper-V の PowerShell                 | N                     |
| Windows Server Update Services ツール                   | UpdateServices-RSAT                | N                     |
| API と PowerShell コマンドレット                             | UpdateServices API                 | N                     |
| DHCP サーバーツール                                      | RSAT-DHCP                          | N                     |
| DNS サーバーツール                                       | RSAT-DNS-サーバー                    | N                     |
| リモートアクセス管理ツール                         | RSAT-RemoteAccess                  | N                     |
| Windows PowerShell 用のリモート アクセス モジュール            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC over HTTP プロキシ                                    | RPC over HTTP-プロキシ                | N                     |
| セットアップおよびブート イベント収集                        | セットアップ-ブート-イベントコレクション    | N                     |
| Simple TCP/IP Services                                 | Simple-TCPIP                       | N                     |
| SMB 1.0/CIFS ファイル共有のサポート                      | FS-SMB1                            | Y                     |
| SMB 帯域幅の制限                                    | FS SMBBW                           | N                     |
| SNMP サービス                                           | SNMP サービス                       | N                     |
| SNMP WMI プロバイダー                                      | SNMP-WMI プロバイダー                  | N                     |
| Telnet クライアント                                          | Telnet クライアント                      | N                     |
| Fabric Management 用の VM シールド ツール               | FabricShieldedTools                | N                     |
| Windows Defender の機能                              | Windows Defender-機能          | Y                     |
| Windows Defender                                       | Windows-Defender                   | Y                     |
| Windows Internal Database                              | Windows-内部データベース          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 エンジン                          | PowerShell-V2                      | 状態             |
| Windows PowerShell Desired State Configuration サービス | DSC-サービス                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Windows プロセス アクティブ化サービス                     | が                                | N                     |
| プロセス モデル                                          | プロセス モデル                  | N                     |
| .NET 環境3.5                                   | WAS-NET-環境                | N                     |
| 構成 API                                     | 構成 Api                    | N                     |
| Windows Server バックアップ                                  | Windows Server のバックアップ              | N                     |
| Windows Server 移行ツール                         | Migration                          | N                     |
| Windows 標準ベースの記憶域の管理             | WindowsStorageManagementService    | N                     |
| WinRM IIS 拡張機能                                    | WinRM-IIS-Ext                      | N                     |
| WINS サーバー                                            | WINS                               | N                     |
| WoW64 サポート                                          | WoW64-サポート                      | Y                     |
|                                                        |                                    |                       |
