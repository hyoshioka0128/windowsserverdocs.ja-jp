---
title: Server Core コンテナーに含まれていない役割、役割サービス、および機能-Windows Server、バージョン1803
description: Windows Server の Server Core コンテナーイメージから削除した役割と機能について説明します。
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 41b5a9ac32066f1b2a41de84f66b9be79252c336
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383410"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Server Core コンテナーに含まれていない役割、役割サービス、および機能-Windows Server、バージョン1803

> 適用対象:Windows Server Version 1803

Windows Server バージョン1803では、 [Server Core コンテナーイメージ全体のサイズが**1.58 GB**に縮小](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)されています。 これを行うには、アーキテクチャを最適化し、 [Server Core コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/about/)で必要のないものを削除します。 コンテナーでは機能しなかったものもあれば、ロールや機能が使用されていないものもあります。 

> [!IMPORTANT]
> Server Core**コンテナー**イメージから削除しました。[サーバーコア自体](server-core-roles-and-services.md)ではありません。 

Server Core コンテナーイメージから削除された機能とロールの完全な一覧を次に示します。

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>しくみ
<br>Bitlocker-ユーティリティ
<br>BitLocker
<br>BITS
<br>BITSExtensions-アップロード
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>すべてのサービス
<br>ClientForNFS-インフラストラクチャ
<br>コンテナー
<br>CoreFileServer 場合
<br>DataCenterBridging-LLDP-Tools
<br>DataCenterBridging
<br>重複除去-コア
<br>DeviceHealthAttestationService
<br>DFSN-サーバー
<br>DFSR-Infrastructure-ServerEdition
<br>System.directoryservices-ADAM
<br>System.directoryservices-DomainController
<br>DiskIo-QoS
<br>EnhancedStorage
<br>FailoverCluster-AdminPak
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>ファイル サービス
<br>FileServerVSSAgent
<br>FRS-インフラストラクチャ
<br>FSRM-インフラストラクチャサービス
<br>FSRM-インフラストラクチャ
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-パッケージ
<br>サーバー-z
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>Add-windowsfeature fs-iscsitargetserver-PowerShell
<br>Add-windowsfeature fs-iscsitargetserver
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>Licensing
<br>LightweightServer
<br>Microsoft-Hyper-v-管理-クライアント
<br>Microsoft-hyper-v-Offline
<br>Microsoft-hyper-v-Online
<br>Microsoft-Hyper-v
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft-Windows-GroupPolicy-ServerAdminTools-Update
<br>Microsoft-Windows-Subsystem-Linux
<br>MSRDC-インフラストラクチャ
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P-Pnの場合のみ
<br>PeerDist
<br>印刷-クライアント-Gui
<br>印刷-LPDPrintService
<br>印刷-サーバー-基礎-機能
<br>印刷-サーバー-役割
<br>QWAVE
<br>RasRoutingProtocols
<br>リモート デスクトップのサービス
<br>RemoteAccess
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices-ロール
<br>RightsManagementServices
<br>RMS-フェデレーション
<br>SBMgr-UI
<br>ServerCore-Drivers-General-WOW64
<br>ServerCore-ドライバー-全般
<br>ServerForNFS-インフラストラクチャ
<br>ServerManager---ツール
<br>ServerMediaFoundation
<br>Servermigration.log
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol-サーバー
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>ソフトウェア Loadbalancer
<br>ストレージ-レプリカ-AdminPack
<br>記憶域レプリカ
<br>Tpm-PSH-コマンドレット
<br>UpdateServices-データベース
<br>UpdateServices-サービス
<br>UpdateServices-WidDatabase
<br>Updateservices-api
<br>VmHostAgent
<br>VolumeActivation-完全ロール
<br>Web アプリケーション-プロキシ
<br>Web アクセス
<br>WebEnrollmentServices
<br>Windows-Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>W誤 Nmpprovider
<br>ワークフォルダー-サーバー
<br>WSS-製品パッケージ

</div>