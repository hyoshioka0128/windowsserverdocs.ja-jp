---
title: Windows Server ではない役割、役割サービス、および機能-Server Core
description: Windows Server の Server Core インストールオプションに含まれていない役割と機能について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 882410792c7b8df8a8275c357d64fc17c9f3479e
ms.sourcegitcommit: feec5cbe983c8c5800ccd4fc214914084fcceaba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70975258"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Windows Server ではない役割、役割サービス、および機能-Server Core

> 適用対象:Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Windows Server の Server Core インストールオプションから、次の役割、役割サービス、および機能が削除されました。 この情報は、お使いの環境で Server Core オプションが機能するかどうかを判断するのに役立ちます。

> [!NOTE]
> また、 [Server Core に含ま](server-core-roles-and-services.md)れる役割、役割サービス、および機能の一覧も表示できます。 これは非常に大きなリストなので、最適な結果を得るために、目的の特定の役割または機能を一覧で検索します。

## <a name="roles-not-in-server-core"></a>Server Core にないロール

- Fax サーバー (**fax**)
- MultiPoint Services (**MultiPointServerRole**)
- ネットワークポリシーとアクセスサービス (**NPAS**)
- Windows 展開サービス (**WDS**) *(Windows Server バージョン1803より前)*

## <a name="role-services-not-in-server-core"></a>Server Core にない役割サービス
一部のリモートデスクトップの役割サービスは、Server Core (接続ブローカー、ライセンス、仮想化ホスト) に含まれていますが、他の役割はありません (ゲートウェイ、RD セッションホスト、Web アクセス)。

- 印刷とドキュメントサービス \ 分散スキャンサーバー (**印刷-スキャン-サーバー**)
- 印刷とドキュメントサービス \ インターネット印刷 (**印刷-インターネット**)
- リモートデスクトップサービス \ リモートデスクトップゲートウェイ (**RDS-ゲートウェイ**)
- リモートデスクトップサービス \ リモートデスクトップセッションホスト (**RDS-RD サーバー**)
- リモートデスクトップサービス \ リモートデスクトップ Web アクセス (**RDS-Web アクセス**)
- 役割サービス Web サーバー (IIS) \ 管理ツール \ IIS 管理コンソール (**Web 管理**コンソール)
- 役割サービス Web サーバー (IIS) \ 管理ツール \ IIS 6 管理互換性 \ IIS 6 管理コンソール (**Web Lgcy**)
- Windows 展開サービス \ 配置サーバー (**WDS-展開**)
- Windows 展開サービス \ トランスポートサーバー (**WDS-transport**) *(Windows Server バージョン1803より前)*

## <a name="features-not-in-server-core"></a>Server Core に含まれていない機能
- バックグラウンドインテリジェント転送サービス (BITS) \ IIS サーバー拡張機能 (**bits-iis-Ext**)
- BitLocker ネットワークロック解除 (**bitlocker-networkunlock**)
- Direct Play (**Direct play**)
- インターネット印刷クライアント (**インターネット-印刷-クライアント**)
- LPR ポートモニター (**Lpr ポートモニター**)
- メッセージキュー \ メッセージキューサービス \ マルチキャストサポート (**MSMQ-マルチキャスト**)
- RAS 接続マネージャー管理キット (**CMAK**)
- リモートアシスタンス (**リモートアシスタンス**)
- リモートサーバー管理ツール \ 機能管理ツール \ SMTP サーバーツール (**RSAT-SMTP**)
- リモートサーバー管理ツール \ 機能管理ツール \ BitLocker ドライブ暗号化管理ユーティリティ \ BitLocker ドライブ暗号化ツール (**RSAT-機能-BitLocker-RemoteAdminTool**)
- リモートサーバー管理ツール \ 機能管理ツール \ BITS サーバー拡張ツール (**RSAT-BITS-サーバー**)
- リモートサーバー管理ツール \ 機能管理ツール \ ネットワーク負荷分散ツール (**RSAT-NLB**)
- リモートサーバー管理ツール \ 機能管理ツール \ SNMP ツール (**RSAT-SNMP**)
- リモートサーバー管理ツール \ 機能管理ツール \ WINS サーバーツール (**RSAT-WINS**)
- リモートサーバー管理ツール \ 役割管理ツール \ hyper-v 管理ツール \ hyper-v GUI 管理ツール (**hyper-v-ツール**)
- リモートサーバー管理ツール \ 役割管理ツール \ リモートデスクトップサービスツール \ リモートデスクトップゲートウェイツール (**RSAT-RDS-ツール**)
- リモートサーバー管理ツール \ 役割管理ツール \ リモートデスクトップサービスツール \ リモートデスクトップゲートウェイツール (**RSAT-ゲートウェイ**)
- リモートサーバー管理ツールの役割管理ツール \ リモートデスクトップサービスツール \ リモートデスクトップライセンス診断ツール (**RSAT-RDS-Licensing-診断-UI**)
- リモートサーバー管理ツール \ 役割管理ツール \ リモートデスクトップサービスツール \ リモートデスクトップライセンスツール (**RDS-Licensing-UI**)
- リモートサーバー管理ツール \ 役割管理ツール \ Windows Server Update Services ツール \ ユーザーインターフェイス管理コンソール (**Updateservices-UI**)
- リモートサーバー管理ツール \ 役割管理ツール \ Active Directory 証明書サービスツール (**RSAT-ADCS**)
- リモートサーバー管理ツール \ 役割管理ツール \ Active Directory 証明書サービスツール \ 証明機関管理ツール (**RSAT-ADCS-管理**)
- リモートサーバー管理ツール \ 役割管理ツール \ Active Directory 証明書サービスツール \ オンラインレスポンダーツール (**RSAT-オンラインレスポンダー**)
- リモートサーバー管理ツール \ 役割管理ツール \ Active Directory Rights Management サービスツール (**RSAT-ADRMS**)
- リモートサーバー管理ツール \ 役割管理ツール \ Fax サーバーツール (**RSAT-Fax**)
- リモートサーバー管理ツール \ 役割管理ツール \ ファイルサービスツール (**RSAT-ファイルサービス**)
- リモートサーバー管理ツール \ 役割管理ツール \ ファイルサービスツール \ DFS 管理ツール (**RSAT-dfs-管理-Con**)
- リモートサーバー管理ツール \ 役割管理ツール \ ファイルサービスツール \ ファイルサーバーリソースマネージャーツール (**RSAT-FSRM-管理**)
- リモートサーバー管理ツール \ 役割管理ツール \ ファイルサービスツール \ ネットワークファイルシステム管理ツール (**RSAT-NFS-Admin**) 用サービス
- リモートサーバー管理ツール \ 役割管理ツール \ ネットワークポリシーとアクセスサービスツール (**RSAT-NPAS**)
- リモートサーバー管理ツール \ 役割管理ツール \ 印刷とドキュメントサービスツール (**RSAT-印刷サービス**)
- リモートサーバー管理ツール \ 役割管理ツール \ ボリュームライセンス認証ツール (**RSAT-VA-ツール**)
- リモートサーバー管理ツール \ 役割管理ツール \ Windows 展開サービスツール (**WDS-AdminPack**)
- Simple TCP/IP Services (**simple-TCPIP**)
- SMTP サーバー (**Smtp サーバー**)
- TFTP クライアント (**Tftp クライアント**)
- WebDAV リダイレクター (**webdav-リダイレクター**)
- Windows 生体認証フレームワーク (**生体認証-フレームワーク**)
- Windows defender の機能 \ GUI (windows defender **-gui**)
- Windows Identity Foundation 3.5 (**windows-identity-Foundation**)
- Windows PowerShell \ Windows PowerShell ISE (**powershell-ISE**)
- Windows Search Service (**Search-Service**)
- Windows TIFF IFilter (**windows-tiff-ifilter**)
- ワイヤレス LAN サービス (**ワイヤレスネットワーク**)
- XPS ビューアー (**Xps ビューアー**)
