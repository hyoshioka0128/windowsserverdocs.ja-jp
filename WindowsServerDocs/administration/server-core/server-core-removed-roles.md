---
title: Windows Server ではない役割、役割サービス、および機能-Server Core
description: Windows Server の Server Core インストールオプションに含まれていない役割と機能について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: ce5107e8e0ab573df7588428db65c8b223cf1f13
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476514"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Windows Server ではない役割、役割サービス、および機能-Server Core

> 適用対象:Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Windows Server の Server Core インストールオプションから、次の役割、役割サービス、および機能が削除されました。 この情報は、お使いの環境で Server Core オプションが機能するかどうかを判断するのに役立ちます。

> [!NOTE]
> また、 [Server Core に含ま](server-core-roles-and-services.md)れる役割、役割サービス、および機能の一覧も表示できます。 これは非常に大きなリストなので、最適な結果を得るために、目的の特定の役割または機能を一覧で検索します。

## <a name="roles-not-in-server-core"></a>Server Core にないロール

- FAX
- MultiPointServerRole
- NPAS
- WDS

## <a name="role-services-not-in-server-core"></a>Server Core にない役割サービス
一部のリモートデスクトップの役割サービスは、Server Core (接続ブローカー、ライセンス、仮想化ホスト) に含まれていますが、他の役割はありません (ゲートウェイ、RD セッションホスト、Web アクセス)。

- 印刷-スキャン-サーバー
- 印刷-インターネット
- RDS-ゲートウェイ
- RDS-RD サーバー
- RDS-Web アクセス
- Web 管理-コンソール
- Lgcy-管理コンソール
- WDS-展開
- WDS-トランスポート *(Windows Server バージョン1803以前)*

## <a name="features-not-in-server-core"></a>Server Core に含まれていない機能

- BITS-IIS-Ext
- BitLocker-NetworkUnlock
- 直接再生
- インターネット-印刷-クライアント
- LPR-ポートモニター
- MSMQ-マルチキャスト
- マネージャー
- リモートアシスタンス
- RSAT-SMTP
- RSAT-機能ツール-BitLocker-RemoteAdminTool
- RSAT-Bits サーバー
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- Hyper-v-ツール
- RSAT-RDS-ツール
- RSAT-RDS-ゲートウェイ
- RSAT-RDS-Licensing-診断-UI
- RDS-Licensing-UI
- UpdateServices-UI
- RSAT-ADCS
- RSAT-ADCS-管理
- RSAT-オンラインレスポンダー
- RSAT-ADRMS
- RSAT-Fax
- RSAT-ファイルサービス
- RSAT-DFS 管理-Con
- RSAT-FSRM-管理
- RSAT-NFS-管理者
- RSAT-NPAS
- RSAT-印刷サービス
- RSAT-VA-ツール
- WDS-AdminPack
- SMTP-サーバー
- TFTP-クライアント
- WebDAV-リダイレクター
- 生体認証-フレームワーク
- Windows-Defender-Gui
- Windows-Identity-Foundation
- PowerShell-ISE
- 検索-サービス
- Windows-TIFF-IFilter
- ワイヤレスネットワーク
- XPS ビューアー

