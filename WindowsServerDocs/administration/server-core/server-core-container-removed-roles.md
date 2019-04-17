---
title: 役割、役割サービス、および Server Core コンテナーの Windows Server バージョン 1803 ではなく機能
description: 役割と Windows server Server Core コンテナー イメージから削除した機能について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 0ad574a04ba7ecd235f1825bd25c247a1565edf6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1859912"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>役割、役割サービス、および Server Core コンテナーの Windows Server バージョン 1803 ではなく機能

> 対象: Windows Server、バージョン 1803

Windows server、バージョン 1803、 [ **1.58**gb Server Core コンテナー画像全体のサイズを削減](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)おしています。 この行った方法は、アーキテクチャを最適化して[サーバー コア コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/about/)の不要なものを削除することです。 いくつか点をうまく行かなかったコンテナーに、役割と機能が使用できない一部でした。 

> [!IMPORTANT]
> Server Core**コンテナー**の画像、 [Server Core 自身](server-core-roles-and-services.md)いないから削除しました。 

機能と Server Core コンテナーの画像から削除されるロールの一覧を示します。

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>認証マネージャー
<br>Bitlocker ユーティリティ
<br>BitLocker
<br>ビット
<br>BITSExtensions アップロード
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS インフラストラクチャ
<br>コンテナー
<br>CoreFileServer
<br>DataCenterBridging-LLDP-ツール
<br>DataCenterBridging
<br>Dedup コア
<br>DeviceHealthAttestationService
<br>DFSN サーバー
<br>DFSR-インフラストラクチャ-ServerEdition
<br>つ ADAM
<br>つ-ドメイン コント ローラー
<br>DiskIo QoS
<br>EnhancedStorage
<br>FailoverCluster AdminPak
<br>FailoverCluster AutomationServer
<br>FailoverCluster CmdInterface
<br>FailoverCluster FullServer
<br>FailoverCluster PowerShell
<br>ファイル サービス
<br>FileServerVSSAgent
<br>FRS インフラストラクチャ
<br>FSRM インフラストラクチャのサービス
<br>FSRM インフラストラクチャ
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService パッケージ
<br>IdentityServer SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>ライセンス
<br>LightweightServer
<br>Microsoft のハイパー-V-管理-クライアント
<br>Microsoft ハイパー-V-オフライン
<br>Microsoft ハイパー-V-オンライン
<br>Microsoft の Hyper-v
<br>Microsoft Windows-FCI-クライアント-パッケージ
<br>Microsoft Windows-GroupPolicy-ServerAdminTools の更新
<br>Microsoft Windows サブシステム Linux
<br>MSRDC インフラストラクチャ
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P PnrpOnly
<br>PeerDist
<br>印刷クライアント-Gui
<br>印刷 LPDPrintService
<br>印刷 Server Foundation 機能
<br>印刷のサーバーの役割
<br>QWAVE
<br>RasRoutingProtocols
<br>リモート デスクトップ サービス-
<br>リモート アクセス
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices ロール
<br>RightsManagementServices
<br>RMS フェデレーション
<br>SBMgr UI
<br>ServerCore ドライバー全般 WOW64
<br>ServerCore ドライバー-全般
<br>ServerForNFS インフラストラクチャ
<br>ServerManager-コア-RSAT-機能のツール
<br>ServerMediaFoundation
<br>ServerMigration
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol サーバー
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>SoftwareLoadBalancer
<br>記憶域のレプリカ-AdminPack
<br>記憶域レプリカ
<br>Tpm-PSH-コマンドレット
<br>UpdateServices データベース
<br>UpdateServices サービス
<br>UpdateServices WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>VolumeActivation-全の役割
<br>Web アプリケーションのプロキシ
<br>Web アクセス
<br>WebEnrollmentServices
<br>Windows Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders サーバー
<br>WSS 商品のパッケージ

</div>