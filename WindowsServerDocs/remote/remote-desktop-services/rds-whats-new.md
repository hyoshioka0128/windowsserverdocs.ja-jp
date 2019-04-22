---
title: リモート デスクトップ サービスの新機能新機能
description: Windows Server 2016 での RDS の新機能の説明を提供します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/11/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04d52dff-e61b-4633-9908-be8600abc2ba
author: ChristianMontoya
manager: scottman
ms.openlocfilehash: ad13fdce251c1f84bac725e9f1ee266c6aae5e13
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816313"
---
# <a name="whats-new-in-remote-desktop-services"></a>リモート デスクトップ サービスの新機能新機能

リモート デスクトップ サービス (RDS) Windows Server 2016 上に構築されたは、さまざまな顧客シナリオを有効にする仮想化プラットフォームです。 RDS ソリューション全体の機能強化には、リモート デスクトップ チームとマイクロソフトの他のテクノロジ パートナーの両方によって実行される作業が組み込まれています。 次のシナリオとテクノロジは、新しい Windows Server 2016 改良されています。

あります Ignite 2016 から、セッションを確認してください。[Windows Server 2016 で RDS 機能強化を活用](https://channel9.msdn.com/Events/Ignite/2016/BRK3098)します。 このビデオでは、製品チームは、すべてのリモート デスクトップ サービス、vGPU のサポートを含む新規および改良された機能を確認します。 

## <a name="app-compatibility---windows-server-2016-and-windows-10"></a>アプリケーションの互換性 - Windows Server 2016 および Windows 10
Windows 10 の同じ基盤上に構築された Windows Server 2016 はだけでなく、同じルック アンド フィールをデスクトップに期待するが、同じアプリケーションの多くを実行することもが。 (下記参照)、グラフィックス機能を備えた Windows Server 2016 のペアと、生産性を向上するすべてのユーザーのための環境を提供します。 

## <a name="azure-sql-database---the-new-database-for-your-highly-available-environment"></a>Azure SQL Database - 高可用性環境の新しいデータベース
RD 接続ブローカーは、Azure SQL database など、共有 SQL データベースのすべての展開情報 (ユーザー/ホストへのマッピングの前の接続状態など) を格納できます。 SQL Server Always On 可用性グループの手動の展開を見限る、Azure SQL database への接続文字列を取得し、高可用性環境の使用を開始します。

追加情報:[Azure SQL DB を使用して、リモート デスクトップ接続ブローカーの高可用性環境](https://blogs.technet.microsoft.com/enterprisemobility/2016/05/03/new-windows-server-2016-capability-use-azure-sql-db-for-your-remote-desktop-connection-broker-high-availability-environment/)

## <a name="graphics---solving-graphics-needs-across-various-scenarios"></a>グラフィックス - さまざまなシナリオでグラフィックスのニーズを解決します。
HYPER-V の個別のデバイスの割り当てに協力してくれた、GPU が必要なアプリケーションで使用する VM に直接ホスト マシンのようになりました Gpu をマップできます。 RemoteFX vGPU、OpenGL 4.4、OpenCL 1.1、4 k 解像度、および Windows Server 仮想マシンのサポートなどの機能強化も行われました。

追加情報:[個別のデバイスの割り当て](https://blogs.technet.microsoft.com/virtualization/2015/11/)

## <a name="rd-connection-broker---improved-connection-handling-during-logon-storms"></a>RD 接続ブローカー - 強化された接続が大量のログオン時の処理
強化された接続の処理での RD 接続ブローカーは「ログオン ストーム」の中にされることがあります、10,000 個以上の同時ログオン要求を処理できないようになりました。 強化された RD 接続ブローカーは、すばやく、環境にサーバーを追加することによって簡単な展開のメンテナンスにもなります。

追加情報:[リモート デスクトップ接続ブローカーのパフォーマンスの向上](https://blogs.technet.microsoft.com/enterprisemobility/2015/12/15/improved-remote-desktop-connection-broker-performance-with-windows-server-2016-and-windows-server-2012-r2-hotfix-kb3091411/)

## <a name="rdp-10---new-capabilities-built-into-the-protocol"></a>10 - RDP プロトコルに組み込まれている新機能
今すぐに RDP 10 は H.264/AVC 444 コーデックを使用して、ビデオとテキストの両方で適切に最適化します。 このリリースでは、ペンのリモート処理もサポートされます。 これらの機能を備えたローカル セッションと同じようにさらに、リモート セッションが起動します。  

追加情報:[Windows 10 および Windows Server 2016 での RDP 10 AVC/H.264 機能強化](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

## <a name="personal-session-desktops---providing-individual-desktops-to-any-end-user"></a>個人用セッション デスクトップ - 個々 のデスクトップ、エンドユーザーに提供します。
個人用セッション デスクトップは、新しい方法をクラウドでホストされる独自の個人用デスクトップです。 管理者特権と専用のセッション ホストの削除のホスティング環境のユーザーが同じように、デスクトップを管理する複雑さは独自です。

追加情報:[個人用セッション デスクトップ](rds-personal-session-desktops.md)
