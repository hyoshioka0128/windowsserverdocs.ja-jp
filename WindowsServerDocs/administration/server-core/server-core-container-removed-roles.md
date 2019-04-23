---
title: 役割、役割サービス、および Server Core コンテナー - Windows Server、バージョン 1803 ではなく機能
description: 役割と Windows Server の Server Core コンテナー イメージから削除する機能について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 0ad574a04ba7ecd235f1825bd25c247a1565edf6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873783"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>役割、役割サービス、および Server Core コンテナー - Windows Server、バージョン 1803 ではなく機能

> 適用対象:Windows Server Version 1803

Windows server、バージョン 1803、しました[を Server Core コンテナー イメージの全体的なサイズを縮小**1.58 GB**](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)します。 その方法は、アーキテクチャを最適化することによって、および削除を行うことの必要はありません、 [Server Core コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/about/)します。 一部がコンテナーで動作していないこと、役割と機能を使用しているだれがいくつか。 

> [!IMPORTANT]
> Server Core からこれらを削除しました**コンテナー**イメージ、いない[自体、Server Core](server-core-roles-and-services.md)します。 

機能と Server Core コンテナー イメージから削除するロールの完全な一覧を次に示します。

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>認証マネージャー
<br>Bitlocker ユーティリティ
<br>BitLocker
<br>BITS
<br>BITSExtensions アップロード
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS インフラストラクチャ
<br>コンテナー
<br>CoreFileServer
<br>DataCenterBridging LLDP-ツール
<br>DataCenterBridging
<br>重複除去コア
<br>DeviceHealthAttestationService
<br>DFSN サーバー
<br>DFSR-インフラストラクチャの ServerEdition
<br>DirectoryServices ADAM
<br>Directoryservices-domaincontroller
<br>DiskIo QoS
<br>EnhancedStorage
<br>名前の管理
<br>名前 AutomationServer
<br>名前 CmdInterface
<br>名前 FullServer
<br>名前-PowerShell
<br>ファイル サービス
<br>FileServerVSSAgent
<br>FRS インフラストラクチャ
<br>FSRM インフラストラクチャ-サービス
<br>FSRM インフラストラクチャ
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-Package
<br>IdentityServer-SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer-PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>Licensing
<br>LightweightServer
<br>Microsoft の Hyper-V の管理-クライアント
<br>Microsoft の Hyper-V-オフライン
<br>Microsoft-Hyper-V-Online
<br>Microsoft-Hyper-V
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft、Windows のグループ ポリシーの ServerAdminTools-Update
<br>Microsoft-Windows-Subsystem-Linux
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
<br>印刷の Gui クライアント
<br>印刷 LPDPrintService
<br>印刷 Server Foundation 機能
<br>サーバー ロールの印刷
<br>QWAVE
<br>RasRoutingProtocols
<br>リモート デスクトップのサービス
<br>リモート アクセス
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices ロール
<br>RightsManagementServices
<br>RMS フェデレーション
<br>SBMgr UI
<br>ServerCore-Drivers-General-WOW64
<br>ServerCore-ドライバー-全般
<br>ServerForNFS インフラストラクチャ
<br>ServerManager-Core-RSAT-機能-ツール
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
<br>ストレージ-レプリカ-AdminPack
<br>記憶域レプリカ
<br>Tpm-PSH-コマンドレット
<br>UpdateServices データベース
<br>UpdateServices サービス
<br>UpdateServices WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>-Volumeactivation-full-role
<br>Web アプリケーション プロキシ
<br>Web アクセス
<br>WebEnrollmentServices
<br>Windows Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders サーバー
<br>WSS-Product-パッケージ

</div>