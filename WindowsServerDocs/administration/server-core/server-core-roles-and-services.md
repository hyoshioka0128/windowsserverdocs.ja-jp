---
title: 役割、役割サービス、および Windows Server - サーバー コアに含まれる機能
description: Windows Server のサーバーの主要なインストールのオプションでは、どのような役割や機能が含まれますか。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 439edac95e1427086268cab469ed03b94db630da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "2217742"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>役割、役割サービス、および Windows Server - サーバー コアに含まれる機能

> 対象: Windows Server (半年チャネル) および Windows Server 2016

通常について説明[との*ない*Server Core で](server-core-removed-roles.md)- はこれで別の方法を試すし、*含まれている*機能と、問題が*既定でインストールされている*かどうかにします。 次のような役割、役割サービス、および機能*の*Windows Server のサーバーの主要なインストールのオプションです。 Server Core オプション動作環境を把握するために、この情報を使用します。 これは大きなリストであるためは、特定の役割やを探している情報を検索が返されない場合に興味のある機能を検索することを検討してください Server Core では含まれていません。

たとえば、「リモート デスクトップ セッション ホスト」- を検索する場合は、このページで検出されません。 RD セッション ホストが、Server Core 画像に含まれていないためにです。

[常に検索](server-core-removed-roles.md)できることを覚えてに何が含まれて*いません*。 これは、項目を確認する別の方法でだけです。

## <a name="roles-included-in-server-core"></a>役割 Server Core に含まれています。
サーバーの主要なインストールのオプションには、次のサーバーの役割が含まれています。

| ロール                                            | 名前                           | 既定でインストールされている場合 |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 証明書サービス           | AD 証明書                 | N                     |
| [Active Directory Domain Services]                | AD ドメインのサービス             | N                     |
| Active Directory フェデレーション サービス (AD FS)            | Ad FS フェデレーション                | N                     |
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
| リモート デスクトップ サービス                         | リモート デスクトップ サービス-        | N                     |
| ボリューム ライセンス認証サービス                      | VolumeActivation               | N                     |
| IIS web サーバー                                  | Web サーバー                     | N                     |
| Windows Server Essentials Experience            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core に含まれる役割サービス
サーバーの主要なインストールのオプションには、次の役割サービスが含まれています。

| ロール                                  | サービスの役割                                                   | 名前                    | 既定でインストールされている場合 |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 証明書サービス | 証明機関                                        | ADC の証明書の権限     | N                     |
|                                       | 証明書の登録ポリシー Web サービス                      | ADC-登録-Web-Pol     | N                     |
|                                       | 証明書の登録 Web サービス                             | ADC-登録-Web-Svc     | N                     |
|                                       | 証明機関 Web 登録                         | ADC Web の登録     | N                     |
|                                       | ネットワーク デバイス登録サービス                              | ADC デバイスの登録  | N                     |
|                                       | オンラインの応答側                                               | ADC オンライン証明書        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management サーバー                      | ADRMS サーバー            | N                     |
|                                       | Id のフェデレーション サポート                                    | ADRMS Id          | N                     |
| ファイル サービスおよび記憶域サービス             | ファイルおよび iSCSI サービス                                        | ファイル サービス           | N                     |
|                                       | ファイル サーバー                                                    | FS-ファイル サーバー           | N                     |
|                                       | ネットワーク ファイル用 BranchCache                                  | FS BranchCache          | N                     |
|                                       | データ重複除去                                             | FS-データの重複   | N                     |
|                                       | DFS 名前空間                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS レプリケーション                                                | FS DFS レプリケーション      | N                     |
|                                       | ファイル サーバー リソース マネージャー                                   | FS リソース-マネージャー     | N                     |
|                                       | ファイル サーバー VSS エージェント サービス                                  | FS VSS-エージェント            | N                     |
|                                       | iSCSI Target Server                                            | iSCSITarget サーバー      | N                     |
|                                       | iSCSI ターゲット記憶域プロバイダー (VDS と VSS ハードウェア プロバイダー) | iSCSITarget-VSS-VDS     | N                     |
|                                       | NFS サーバー                                                 | FS NFS-サービス          | N                     |
|                                       | ワーク フォルダー                                                   | FS SyncShareService     | N                     |
|                                       | 記憶域サービス                                               | 記憶域サービス        | Y                     |
| 印刷とドキュメント サービス           | サーバーを印刷します。                                                   | プリント サーバー            | N                     |
|                                       | LPD サービス                                                    | 印刷 LPD-サービス       | N                     |
| リモート アクセス                         | DirectAccess と VPN (RAS)                                     | DirectAccess VPN        | N                     |
|                                       | ルーティング                                                        | ルーティング                 | N                     |
|                                       | Web アプリケーション プロキシ                                          | Web アプリケーションのプロキシ   | N                     |
| リモート デスクトップ サービス               | リモート デスクトップ接続ブローカー                               | RDS 接続-ブローカー   | N                     |
|                                       | リモート デスクトップ ライセンス                                       | RDS ライセンス           | N                     |
|                                       | リモート デスクトップ仮想化ホスト                             | RDS 仮想化      | N                     |
| Web サーバー (IIS)                      | Web サーバー                                                     | Web の web サーバー           | N                     |
|                                       | 一般的な HTTP 機能                                           | Web の一般的な-Http         | N                     |
|                                       | 既定のドキュメント                                               | Web の既定のドキュメント         | N                     |
|                                       | ディレクトリの参照                                             | Web ディレクトリの参照        | N                     |
|                                       | HTTP エラー                                                    | Web Http のエラー         | N                     |
|                                       | 静的なコンテンツ                                                 | Web 静的コンテンツ      | N                     |
|                                       | HTTP のリダイレクト                                               | Web Http のリダイレクト       | N                     |
|                                       | WebDAV 発行                                              | Web DAV 発行      | N                     |
|                                       | 正常性と診断                                         | Web の正常性              | N                     |
|                                       | HTTP のログ記録                                                   | Web のログ Http        | N                     |
|                                       | ユーザー設定のログ記録                                                 | Web のユーザー設定のログ      | N                     |
|                                       | ログ記録のツール                                                  | Web のログのライブラリ       | N                     |
|                                       | ODBC ログ                                                   | Web のログ ODBC        | N                     |
|                                       | 要求の監視                                              | Web のモニターの要求     | N                     |
|                                       | トレース                                                        | Web のトレース Http        | N                     |
|                                       | パフォーマンス                                                    | Web パフォーマンス         | N                     |
|                                       | 静的コンテンツ圧縮                                     | Web の状態の圧縮    | N                     |
|                                       | 動的なコンテンツの圧縮                                    | Web の圧縮 Dyn     | N                     |
|                                       | セキュリティ                                                       | Web のセキュリティ            | N                     |
|                                       | 要求のフィルタ リング                                              | Web フィルタ リング           | N                     |
|                                       | 基本認証                                           | Web の基本-認証          | N                     |
|                                       | 一元的な SSL 証明書のサポート                            | Web CertProvider        | N                     |
|                                       | クライアント証明書のマッピングの認証                      | Web クライアントの認証         | N                     |
|                                       | ダイジェスト認証                                          | Web のダイジェスト-認証         | N                     |
|                                       | IIS クライアント証明書のマッピング認証                  | Web の証明書の認証           | N                     |
|                                       | Ip アドレスとドメインの制限                                     | Web IP セキュリティ         | N                     |
|                                       | URL の承認                                              | Web の Url の認証            | N                     |
|                                       | Windows 認証                                         | Web から Windows の認証        | N                     |
|                                       | アプリケーションの開発                                        | Web アプリの開発             | N                     |
|                                       | .NET 拡張 3.5                                         | Web Net (内線)             | N                     |
|                                       | .NET 拡張 4.6                                         | Web の Net-Ext45           | N                     |
|                                       | アプリケーション初期化                                     | Web AppInit             | N                     |
|                                       | ASP                                                            | Web ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Asp 個人の web             | N                     |
|                                       | ASP.NET 4.6                                                    | Web の Asp-Net45           | N                     |
|                                       | CGI                                                            | Web CGI                 | N                     |
|                                       | ISAPI 拡張機能                                               | Web ISAPI (内線)           | N                     |
|                                       | ISAPI フィルター                                                  | Web ISAPI フィルター処理        | N                     |
|                                       | サーバー側が含まれています                                           | Web が含まれています            | N                     |
|                                       | WebSocket プロトコル                                             | Web Websocket          | N                     |
|                                       | FTP サーバー                                                     | Web から Ftp サーバー          | N                     |
|                                       | FTP サービス                                                    | Web Ftp サービス         | N                     |
|                                       | FTP 機能拡張                                              | Web で Ftp の拡張             | N                     |
|                                       | 管理ツール                                               | Web 管理-ツール          | N                     |
|                                       | IIS 6 管理互換性                                 | Web の管理の互換性         | N                     |
|                                       | IIS 6 メタベース互換性                                   | Web メタベース            | N                     |
|                                       | IIS 6 スクリプト ツール                                          | Web Lgcy スクリプト      | N                     |
|                                       | IIS 6 WMI 互換性                                        | Web WMI                 | N                     |
|                                       | IIS 管理スクリプトとツール                               | Web スクリプト ツール     | N                     |
|                                       | 管理サービス                                             | Web 管理サービス        | N                     |
| Windows Server Update Services        | WID 接続                                               | UpdateServices WidDB    | N                     |
|                                       | WSUS サービス                                                  | UpdateServices サービス | N                     |
|                                       | SQL Server の接続                                        | UpdateServices DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core に含まれる機能
サーバーの主要なインストールのオプションには、次の機能が含まれています。

| 機能                                                | 名前                               | 既定でインストールされている場合 |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET framework 3.5 の機能                            | ネット フレームワークの機能             | N                     |
| .NET framework 3.5 が (.NET 2.0、3.0 を含む)       | ネット ・ フレームワーク                 | (削除)             |
| HTTP のライセンス認証                                        | ネット HTTP のアクティブ化                | N                     |
| HTTP 非アクティブ化                                    | ネット-以外の HTTP-アクティブ                 | N                     |
| .NET framework 4.6 機能                            | ネット Framework 45 機能          | Y                     |
| .NET Framework 4.6                                     | ネット Framework 45 コア              | Y                     |
| ASP.NET 4.6                                            | ネット Framework 45 ASPNET            | N                     |
| WCF サービス                                           | ネット-WCF-Services45                 | Y                     |
| HTTP のライセンス認証                                        | ネット WCF HTTP Activation45          | N                     |
| メッセージ (キュー) のライセンス認証                      | ネット WCF MSMQ Activation45          | N                     |
| 名前付きパイプのライセンス認証                                  | ネット WCF パイプ Activation45          | N                     |
| TCP のアクティブ化                                         | ネット WCF TCP Activation45           | N                     |
| TCP ポートの共有                                       | ネット WCF TCP PortSharing45          | Y                     |
| バックグラウンド インテリジェント転送サービス (BITS)         | ビット                               | N                     |
| コンパクト サーバー                                         | ビットから最適化サーバー                | N                     |
| BitLocker ドライブ暗号化                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS クライアント                                         | NFS クライアント                         | N                     |
| コンテナー                                             | コンテナー                         | N                     |
| データ センター ブリッジング                                   | データ センター ブリッジ               | N                     |
| 拡張記憶域                                       | EnhancedStorage                    | N                     |
| フェールオーバー クラスタリング                                    | -しないで                | N                     |
| グループ ポリシーの管理                                | GPMC                               | N                     |
| サービスの I/O 品質                                 | DiskIo QoS                         | N                     |
| IIS ホスト可能な Web コア                                  | Web WHC                            | N                     |
| 管理 (IPAM) サーバーの IP アドレス                    | IPAM                               | N                     |
| iSNS サーバー サービス                                    | ISNS                               | N                     |
| Management OData IIS 拡張機能                         | ManagementOdata                    | N                     |
| メディア ファンデーション                                       | サーバーの基盤メディア            | N                     |
| メッセージ キュー                                        | MSMQ                               | N                     |
| メッセージ キュー サービス                               | MSMQ サービス                      | N                     |
| メッセージ キュー サーバー                                 | -キューイング                        | N                     |
| ディレクトリ サービスの統合                          | MSMQ ディレクトリ                     | N                     |
| HTTP のサポート                                           | MSMQ HTTP のサポート                  | N                     |
| メッセージ キューのトリガー                               | MSMQ トリガー                      | N                     |
| ルーティング サービス                                        | MSMQ ルーティング                       | N                     |
| メッセージ キュー DCOM プロキシ                             | MSMQ DCOM                          | N                     |
| マルチパス I/O                                          | マルチパス IO                       | N                     |
| MultiPoint Connector                                   | マルチポイント コネクタ               | N                     |
| マルチポイント コネクタ サービス                          | マルチポイント コネクタのサービス      | N                     |
| マルチポイント マネージャーとマルチポイント ダッシュ ボード            | マルチポイント ツール                   | N                     |
| ネットワーク負荷分散                                 | NLB                                | N                     |
| ピア名解決プロトコル                          | PNRP                               | N                     |
| 高品質な Windows オーディオ ビデオ エクスペリエンス                 | qWave                              | N                     |
| Remote Differential Compression                        | RDC                                | N                     |
| リモート サーバー管理ツール                     | RSAT                               | N                     |
| 機能の管理ツール                           | RSAT のツール機能                 | N                     |
| BitLocker ドライブ暗号化管理ユーティリティ  | RSAT 機能ツール BitLocker       | N                     |
| DataCenterBridging LLDP ツール                          | RSAT DataCenterBridging LLDP ツール | N                     |
| フェールオーバー クラスター ツール                              | RSAT クラスター                    | N                     |
| Windows PowerShell 用フェールオーバー モジュール         | RSAT クラスタ リング PowerShell         | N                     |
| フェールオーバー オートメーション サーバー                     | RSAT クラスター AutomationServer   | N                     |
| フェールオーバー コマンド インターフェイス                     | RSAT クラスター CmdInterface       | N                     |
| IP アドレスの管理 (IPAM) クライアント                    | IPAM クライアントの機能                | N                     |
| シールド VM ツール                                      | RSAT に影響を受けません-VM-ツール             | N                     |
| Windows PowerShell 用の記憶域レプリカ モジュール          | RSAT の記憶域のレプリカ               | N                     |
| 役割の管理ツール                              | RSAT 役割-ツール                    | N                     |
| AD DS および AD LDS ツール                                 | RSAT AD-ツール                      | N                     |
| Windows PowerShell 用の active Directory モジュール         | RSAT-AD-PowerShell                 | N                     |
| AD DS ツール                                            | RSAT 追加                          | N                     |
| Active Directory 管理センター                 | RSAT-広告の順に選び、                | N                     |
| AD DS スナップインおよびコマンド ライン ツール                  | RSAT 追加ツール                    | N                     |
| AD LDS スナップインおよびコマンド ライン ツール                 | RSAT ADLDS                         | N                     |
| HYPER-V 管理ツール                               | RSAT ハイパー-V-ツール                 | N                     |
| Windows PowerShell 用 HYPER-V モジュール                  | Hyper-V の PowerShell                 | N                     |
| Windows Server の更新サービスのツール                   | UpdateServices RSAT                | N                     |
| API および PowerShell コマンドレット                             | UpdateServices API                 | N                     |
| DHCP サーバー ツール                                      | RSAT DHCP                          | N                     |
| DNS サーバーのツール                                       | RSAT から DNS サーバー                    | N                     |
| リモート アクセス管理ツール                         | RSAT-されていません                  | N                     |
| Windows PowerShell 用のリモート アクセス モジュール            | --PowerShell RSAT されていません       | N                     |
| RPC over HTTP プロキシ                                    | RPC 上にポインターを HTTP プロキシ                | N                     |
| セットアップおよびブート イベント収集                        | セットアップとの起動のイベントのコレクション    | N                     |
| Simple TCP/IP Services                                 | 単純な TCPIP                       | N                     |
| SMB 1.0/CIFS ファイル共有のサポート                      | FS SMB1                            | Y                     |
| SMB 帯域幅の制限                                    | FS SMBBW                           | N                     |
| SNMP サービス                                           | SNMP サービス                       | N                     |
| SNMP WMI プロバイダー                                      | SNMP WMI-プロバイダー                  | N                     |
| Telnet クライアント                                          | Telnet クライアント                      | N                     |
| Fabric Management 用の VM シールド ツール               | FabricShieldedTools                | N                     |
| Windows Defender 機能                              | Windows Defender の機能          | Y                     |
| Windows Defender                                       | Windows Defender                   | Y                     |
| Windows Internal Database                              | Windows 内部データベース          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 エンジン                          | PowerShell V2                      | (削除)             |
| Windows PowerShell に必要なサービスの状態の構成 | DSC サービス                        | N                     |
| Windows PowerShell Web アクセス                          | WindowsPowerShellWebAccess         | N                     |
| Windows プロセス アクティブ化サービス                     | されました                                | N                     |
| プロセス モデル                                          | されたプロセス モデル                  | N                     |
| .NET 環境 3.5                                   | された NET 環境                | N                     |
| 構成 Api                                     | 構成 Api                    | N                     |
| Windows Server バックアップ                                  | Windows Server のバックアップ              | N                     |
| Windows Server 移行ツール                         | 移行                          | N                     |
| Windows 標準ベースの記憶域の管理             | WindowsStorageManagementService    | N                     |
| WinRM IIS 拡張機能                                    | WinRM IIS (内線)                      | N                     |
| WINS サーバー                                            | 優先                               | N                     |
| WoW64 のサポート                                          | WoW64 サポート                      | Y                     |
|                                                        |                                    |                       |
