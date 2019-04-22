---
title: 役割、役割サービス、および Windows Server の Server Core ではなく機能
description: 役割と Windows Server の Server Core インストール オプションで含まれていない機能について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 308bc8a5d25e2ec67438f0ee03cbfce6f7411ca2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825533"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>役割、役割サービス、および Windows Server の Server Core ではなく機能

> 適用対象:Windows Server (半期チャネル) および Windows Server 2016

Windows Server の Server Core インストール オプションから、次の役割、役割サービス、および機能が削除されました。 環境内の Server Core オプションの動作はかどうかを把握するのにには、この情報を使用します。

> [!NOTE]
> 役割、役割サービスの一覧を表示もでき、機能を[Server Core に含まれる](server-core-roles-and-services.md)します。 これは非常に大きなリストでは、したがって最良の結果を特定の役割または機能に関心があるは、その一覧を検索します。

## <a name="roles-not-in-server-core"></a>Server Core ではなくロール

- FAX
- MultiPointServerRole
- NPAS
- WDS

## <a name="role-services-not-in-server-core"></a>Server Core ではなくロール サービス
ある (接続ブローカー、ライセンス、仮想化ホスト) の Server Core に一部のリモート デスクトップ ロール サービスが含まれますが、他のユーザーに注意してください (ゲートウェイ、RD セッション ホスト、Web アクセス)。

- スキャン サーバーの印刷
- インターネット印刷
- RDS ゲートウェイ
- RDS-RD サーバー
- RDS Web アクセス
- Web の管理コンソール
- Web Lgcy 管理コンソール
- WDS の展開
- WDS トランスポート *(前に Windows Server バージョン 1803)*

## <a name="features-not-in-server-core"></a>Server Core ではなく機能

- BITS、IIS-Ext
- BitLocker NetworkUnlock
- 直接再生
- インターネット印刷のクライアント
- LPR-Port-Monitor
- MSMQ マルチキャスト
- CMAK
- リモート アシスタンス
- RSAT-SMTP
- RSAT-Feature-Tools-BitLocker-RemoteAdminTool
- RSAT-Bits サーバー
- RSAT-NLB
- RSAT-SNMP
- RSAT WINS
- Hyper V ツール
- RSAT RDS-ツール
- RSAT から RDS ゲートウェイ
- RSAT の RDS のライセンス-診断-UI
- RDS ライセンス UI
- UpdateServices UI
- RSAT ADCS
- RSAT ADCS 個の管理
- オンライン レスポンダーの RSAT
- RSAT ADRMS
- RSAT Fax
- RSAT のファイル サービス
- RSAT-DFS-Mgmt-Con
- RSAT FSRM 個の管理
- RSAT の NFS の管理者
- RSAT NPAS
- RSAT の印刷サービス
- RSAT VA-ツール
- WDS AdminPack
- SMTP サーバー
- TFTP クライアント
- WebDAV リダイレクター
- 生体認証フレームワーク
- Windows Defender の Gui
- Windows-Identity-Foundation
- PowerShell ISE
- 検索サービス
- Windows-TIFF IFilter
- ワイヤレス ネットワーク
- XPS ビューアー

