---
title: Windows Server-Server Core に含まれる役割、役割サービス、および機能
description: Windows Server の Server Core インストールオプションにはどのような役割と機能が含まれていますか。
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 1569feb27a75815771cf84317bebb2fde9d83dfa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895868"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Windows Server-Server Core に含まれる役割、役割サービス、および機能

> 適用対象: Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

通常、 [Server Core では*ないこと*](server-core-removed-roles.md)について説明します。ここでは、別のアプローチを試して、*含まれ*ているものと、既定で何かが*インストールさ*れているかどうかを確認します。 次の役割、役割サービス、および機能は、Windows Server の Server Core インストールオプション*に含ま*れています。 この情報は、お使いの環境で Server Core オプションが機能するかどうかを判断するのに役立ちます。 これは大きなリストなので、関心のある特定の役割または機能を検索することを検討してください。探しているものが見つからない場合、Server Core には含まれていません。

たとえば、"リモートデスクトップセッションホスト" を検索すると、このページには見つかりません。 これは、RD セッションホストが Server Core イメージに含まれていないためです。

何も含まれて*いない*ことを[常に確認](server-core-removed-roles.md)できることに注意してください。 これは、何かを確認するための別の方法にすぎません。

## <a name="roles-included-in-server-core"></a>Server Core に含まれる役割
Server Core インストールオプションには、次のサーバーの役割があります。

| Role                                            | 名前                           | 既定でインストールされますか? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 証明書サービス           | 証明書の AD                 | N                     |
| Active Directory ドメイン サービス                | AD ドメインサービス             | N                     |
| Active Directory フェデレーション サービス (AD FS)            | ADFS-Federation                | N                     |
| Active Directory ライトウェイト ディレクトリ サービス | ADLDS                          | N                     |
| Active Directory Rights Management サービス     | ADRMS                          | N                     |
| デバイス正常性構成証明                       | DeviceHealthAttestationService | N                     |
| DHCP サーバー                                     | [DHCP]                           | N                     |
| DNS サーバー                                      | DNS                            | N                     |
| ファイル サービスおよび記憶域サービス                       | FileAndStorage-サービス        | Y                     |
| ホスト ガーディアン サービス                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 印刷とドキュメント サービス                     | Print-Services                 | N                     |
| リモート アクセス                                   | RemoteAccess                   | N                     |
| リモート デスクトップ サービス                         | リモート デスクトップのサービス        | N                     |
| ボリューム ライセンス認証サービス                      | VolumeActivation               | N                     |
| Web サーバー IIS                                  | Web サーバー                     | N                     |
| Windows Server Essentials Experience            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | Updateservices-api                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core に含まれる役割サービス
Server Core インストールオプションには、次の役割サービスが含まれています。

| Role                                  | 役割サービス                                                   | 名前                    | 既定でインストールされますか? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 証明書サービス | 証明機関                                        | ADCS-証明書の機関     | N                     |
|                                       | 証明書の登録ポリシー Web サービス                      | ADCS-Web-Registry.pol     | N                     |
|                                       | 証明書の登録 Web サービス                             | ADCS-Web-Svc     | N                     |
|                                       | 証明機関 Web 登録                         | ADCS-Web 登録     | N                     |
|                                       | ネットワーク デバイス登録サービス                              | ADCS-デバイス-登録  | N                     |
|                                       | オンライン レスポンダー                                               | ADCS-Online-Cert        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management サーバー                      | ADRMS-サーバー            | N                     |
|                                       | ID フェデレーション サポート                                    | ADRMS-Id          | N                     |
| ファイル サービスおよび記憶域サービス             | ファイル サービスおよび iSCSI サービス                                        | ファイル サービス           | N                     |
|                                       | ファイル サーバー                                                    | FS FileServer           | N                     |
|                                       | ネットワーク ファイル用 BranchCache                                  | FS-BranchCache          | N                     |
|                                       | データ重複除去                                             | FS-データ-重複除去   | N                     |
|                                       | DFS 名前空間                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS レプリケーション                                                | FS-DFS-Replication      | N                     |
|                                       | File Server Resource Manager                                   | FS-Resource-Manager     | N                     |
|                                       | ファイル サーバー VSS エージェント サービス                                  | FS VSS-エージェント            | N                     |
|                                       | iSCSI ターゲット サーバー                                            | iSCSITarget-サーバー      | N                     |
|                                       | iSCSI ターゲット記憶域プロバイダー (VDS および VSS ハードウェアプロバイダー) | iSCSITarget-VDS     | N                     |
|                                       | NFS サーバー                                                 | NFS-サービス          | N                     |
|                                       | 作業フォルダー                                                   | FS 同期サービス     | N                     |
|                                       | ストレージ サービス                                               | ストレージ-サービス        | Y                     |
| 印刷とドキュメント サービス           | プリント サーバー                                                   | Print-Server            | N                     |
|                                       | LPD サービス                                                    | Print-LPD-Service       | N                     |
| リモート アクセス                         | DirectAccess と VPN (RAS)                                     | DirectAccess VPN        | N                     |
|                                       | ルーティング                                                        | ルーティング                 | N                     |
|                                       | Web アプリケーション プロキシ                                          | Web アプリケーション-プロキシ   | N                     |
| リモート デスクトップ サービス               | リモート デスクトップ接続ブローカー                               | RDS-接続-ブローカー   | N                     |
|                                       | リモート デスクトップ ライセンス                                       | RDS-ライセンス           | N                     |
|                                       | リモート デスクトップ仮想化ホスト                             | RDS-仮想化      | N                     |
| Web サーバー (IIS)                      | Web サーバー                                                     | Web サーバーの web           | N                     |
|                                       | HTTP 基本機能                                           | 一般的な Http-web         | N                     |
|                                       | 既定のドキュメント                                               | Web の既定のドキュメント         | N                     |
|                                       | ディレクトリの参照                                             | Web ディレクトリ参照        | N                     |
|                                       | HTTP エラー                                                    | Web Http-エラー         | N                     |
|                                       | 静的なコンテンツ                                                 | Web 静的コンテンツ      | N                     |
|                                       | HTTP リダイレクト                                               | Web Http のリダイレクト       | N                     |
|                                       | WebDAV 発行                                              | Web DAV 発行      | N                     |
|                                       | 状態と診断                                         | Web ヘルス              | N                     |
|                                       | HTTP ログ                                                   | Web Http ログ記録        | N                     |
|                                       | カスタム ログ                                                 | Web のカスタム ログの記録      | N                     |
|                                       | ログ ツール                                                  | Web ログ-ライブラリ       | N                     |
|                                       | ODBC ログ                                                   | Web の ODBC ログの記録        | N                     |
|                                       | 要求モニター                                              | Web 要求のモニター     | N                     |
|                                       | トレース                                                        | Web-Http-Tracing        | N                     |
|                                       | パフォーマンス                                                    | Web パフォーマンス         | N                     |
|                                       | 静的なコンテンツの圧縮                                     | Web の圧縮状態    | N                     |
|                                       | 動的なコンテンツ圧縮                                    | Web の圧縮 Dyn     | N                     |
|                                       | セキュリティ                                                       | Web セキュリティ            | N                     |
|                                       | 要求フィルター                                              | Web フィルター処理           | N                     |
|                                       | 基本認証                                           | Web Basic-認証          | N                     |
|                                       | SSL 証明書サポートの集中化                            | Web CertProvider        | N                     |
|                                       | クライアント証明書マッピング認証                      | Web クライアントの認証         | N                     |
|                                       | ダイジェスト認証                                          | Web ダイジェストの認証         | N                     |
|                                       | IIS クライアント証明書マッピング認証                  | Web 証明書の認証           | N                     |
|                                       | IP およびドメインの制限                                     | Web IP セキュリティ         | N                     |
|                                       | URL 認証                                              | Web Url の認証            | N                     |
|                                       | Windows 認証                                         | Windows-認証 web        | N                     |
|                                       | アプリケーション開発                                        | Web アプリの開発             | N                     |
|                                       | .NET Extensibility 3.5                                         | Web-Net-Ext             | N                     |
|                                       | .NET 拡張4.6                                         | Ext45           | N                     |
|                                       | Application Initialization                                     | Web AppInit             | N                     |
|                                       | ASP                                                            | Web-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Net45           | N                     |
|                                       | CGI                                                            | Web CGI                 | N                     |
|                                       | ISAPI 拡張                                               | Web-ISAPI の拡張           | N                     |
|                                       | ISAPI フィルター                                                  | ISAPI-フィルターが web        | N                     |
|                                       | サーバー側インクルード                                           | Web が含まれています            | N                     |
|                                       | WebSocket プロトコル                                             | Web Websocket          | N                     |
|                                       | FTP サーバー                                                     | Web-Ftp-Server          | N                     |
|                                       | FTP サービス                                                    | Web-Ftp サービス         | N                     |
|                                       | FTP 拡張機能                                              | Web-Ftp-Ext             | N                     |
|                                       | 管理ツール                                               | Web-Mgmt-Tools          | N                     |
|                                       | IIS 6 管理互換性                                 | Web の互換性の管理         | N                     |
|                                       | IIS 6 メタベース互換                                   | Web メタベース            | N                     |
|                                       | IIS 6 スクリプト ツール                                          | Web-Lgcy-Scripting      | N                     |
|                                       | IIS 6 WMI 互換                                        | Web-WMI                 | N                     |
|                                       | IIS 管理スクリプトおよびツール                               | Web-Scripting-Tools     | N                     |
|                                       | Management Service                                             | Web-Mgmt-Service        | N                     |
| Windows Server Update Services        | WID 接続                                               | UpdateServices-WidDB    | N                     |
|                                       | WSUS サービス                                                  | UpdateServices-サービス | N                     |
|                                       | SQL Server 接続                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core に含まれる機能
Server Core インストールオプションには、次の機能があります。

| 機能                                                | 名前                               | 既定でインストールされますか? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5 の機能                            | .NET-フレームワーク-機能             | N                     |
| .NET Framework 3.5 (.NET 2.0 と3.0 を含む)       | NET-Framework-Core                 | (削除済み)             |
| HTTP アクティブ化                                        | NET-HTTP-Activation                | N                     |
| 非 HTTP アクティブ化                                    | NET-Non-HTTP-Activ                 | N                     |
| .NET Framework 4.6 の機能                            | .NET-フレームワーク-45-機能          | Y                     |
| .NET Framework 4.6                                     | .NET-フレームワーク-45-コア              | Y                     |
| ASP.NET 4.6                                            | .NET-フレームワーク-45-ASPNET            | N                     |
| WCF サービス                                           | Services45                 | Y                     |
| HTTP アクティブ化                                        | NET-Activation45          | N                     |
| メッセージキュー (MSMQ) のアクティブ化                      | NET-Activation45          | N                     |
| 名前付きパイプのアクティブ化                                  | NET-Activation45          | N                     |
| TCP のアクティブ化                                         | NET-Activation45           | N                     |
| TCP ポート共有                                       | NET-PortSharing45          | Y                     |
| Background Intelligent Transfer Service (BITS)         | BITS                               | N                     |
| コンパクト サーバー                                         | BITS-Compact サーバー                | N                     |
| BitLocker ドライブ暗号化                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS クライアント                                         | NFS-クライアント                         | N                     |
| Containers                                             | Containers                         | N                     |
| データ センター ブリッジング                                   | データセンターブリッジング               | N                     |
| 拡張記憶域                                       | EnhancedStorage                    | N                     |
| フェールオーバー クラスタリング                                    | Failover-Clustering                | N                     |
| グループ ポリシー管理                                | GPMC                               | N                     |
| サービスの I/O 品質                                 | DiskIo-QoS                         | N                     |
| IIS ホスト可能な Web コア                                  | Web-WHC                            | N                     |
| IP アドレス管理 (IPAM) サーバー                    | IPAM                               | N                     |
| iSNS サーバー サービス                                    | ISNS                               | N                     |
| Management OData IIS 拡張機能                         | ManagementOdata                    | N                     |
| メディア ファンデーション                                       | サーバーのメディアの基盤            | N                     |
| メッセージ キューイング (Message Queuing)                                        | MSMQ (MSMQ)                               | N                     |
| メッセージ キュー サービス                               | MSMQ-Services                      | N                     |
| メッセージ キュー サーバー                                 | MSMQ-Server                        | N                     |
| ディレクトリ サービス統合                          | MSMQ-Directory                     | N                     |
| HTTP サポート                                           | MSMQ-HTTP-Support                  | N                     |
| メッセージ キュー トリガー                               | MSMQ-Triggers                      | N                     |
| ルーティング サービス                                        | MSMQ-Routing                       | N                     |
| メッセージ キュー DCOM プロキシ                             | MSMQ DCOM                          | N                     |
| マルチパス I/O                                          | Multipath-IO                       | N                     |
| MultiPoint Connector                                   | MultiPoint-コネクタ               | N                     |
| MultiPoint コネクタサービス                          | MultiPoint-コネクタ-サービス      | N                     |
| MultiPoint マネージャーと MultiPoint ダッシュボード            | MultiPoint-ツール                   | N                     |
| ネットワーク負荷分散                                 | NLB                                | N                     |
| ピア名解決プロトコル                          | PNRP                               | N                     |
| 高品質な Windows オーディオ ビデオ エクスペリエンス                 | qWave                              | N                     |
| Remote Differential Compression                        | RDC                                | N                     |
| リモート サーバー管理ツール                     | RSAT                               | N                     |
| 機能管理ツール                           | RSAT-Feature-Tools                 | N                     |
| BitLocker ドライブ暗号化管理ユーティリティ  | RSAT 機能ツール BitLocker       | N                     |
| DataCenterBridging LLDP ツール                          | RSAT-DataCenterBridging-LLDP-ツール | N                     |
| フェールオーバー クラスタリング ツール                              | RSAT-Clustering                    | N                     |
| Windows PowerShell 用フェールオーバークラスターモジュール         | RSAT クラスタ リング PowerShell         | N                     |
| フェールオーバークラスターオートメーションサーバー                     | RSAT クラスタ リング AutomationServer   | N                     |
| フェールオーバークラスターコマンドインターフェイス                     | RSAT クラスタ リング CmdInterface       | N                     |
| IP アドレス管理 (IPAM) クライアント                    | IPAM-クライアント機能                | N                     |
| シールドされた VM ツール                                      | RSAT の影響を受けません-VM-ツール             | N                     |
| Windows PowerShell 用記憶域レプリカモジュール          | RSAT-ストレージ-レプリカ               | N                     |
| 役割管理ツール                              | RSAT-Role-Tools                    | N                     |
| AD DS および AD LDS ツール                                 | RSAT AD-ツール                      | N                     |
| Windows PowerShell 用 Active Directory モジュール         | RSAT AD-PowerShell                 | N                     |
| AD DS ツール                                            | RSAT 追加                          | N                     |
| [Active Directory 管理センター]                 | RSAT-AD-AdminCenter                | N                     |
| AD DS スナップインおよびコマンドライン ツール                  | RSAT 追加ツール                    | N                     |
| スナップインとコマンドラインツールの AD LDS                 | RSAT ADLDS                         | N                     |
| Hyper-V 管理ツール                               | RSAT-Hyper-v ツール                 | N                     |
| Windows PowerShell 用 Hyper-V モジュール                  | Hyper V の PowerShell                 | N                     |
| Windows Server Update Services ツール                   | UpdateServices-RSAT                | N                     |
| API と PowerShell コマンドレット                             | UpdateServices API                 | N                     |
| DHCP サーバー ツール                                      | RSAT-DHCP                          | N                     |
| DNS サーバー ツール                                       | RSAT-DNS-Server                    | N                     |
| リモートアクセス管理ツール                         | RSAT-RemoteAccess                  | N                     |
| Windows PowerShell 用のリモート アクセス モジュール            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC over HTTP プロキシ                                    | RPC-over-HTTP-Proxy                | N                     |
| セットアップおよびブート イベント収集                        | セットアップ-ブート-イベントコレクション    | N                     |
| 簡易 TCP/IP サービス                                 | Simple-TCPIP                       | N                     |
| SMB 1.0/CIFS ファイル共有のサポート                      | FS-SMB1                            | Y                     |
| SMB 帯域幅の制限                                    | FS SMBBW                           | N                     |
| SNMP サービス                                           | SNMP-Service                       | N                     |
| WMI SNMP プロバイダー                                      | SNMP-WMI-Provider                  | N                     |
| Telnet クライアント                                          | Telnet クライアント                      | N                     |
| Fabric Management 用の VM シールド ツール               | FabricShieldedTools                | N                     |
| Windows Defender の機能                              | Windows Defender-機能          | Y                     |
| Windows Defender                                       | Windows-Defender                   | Y                     |
| Windows Internal Database                              | Windows-内部データベース          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 エンジン                          | PowerShell-V2                      | (削除済み)             |
| Windows PowerShell Desired State Configuration サービス | DSC-サービス                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Windows プロセス アクティブ化サービス                     | WAS                                | N                     |
| プロセス モデル                                          | プロセス モデル                  | N                     |
| .NET 環境3.5                                   | WAS-NET-Environment                | N                     |
| 構成 API                                     | 構成 Api                    | N                     |
| Windows Server バックアップ                                  | Windows Server のバックアップ              | N                     |
| Windows Server 移行ツール                         | 移行                          | N                     |
| Windows 標準ベースの記憶域の管理             | WindowsStorageManagementService    | N                     |
| WinRM IIS 拡張機能                                    | WinRM-IIS-Ext                      | N                     |
| WINS サーバー                                            | WINS                               | N                     |
| WoW64 サポート                                          | WoW64-サポート                      | Y                     |
|                                                        |                                    |                       |
