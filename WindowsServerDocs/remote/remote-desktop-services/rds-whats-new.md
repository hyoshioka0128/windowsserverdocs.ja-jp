---
title: リモート デスクトップ サービスの新機能
description: Windows Server 2016 の RDS の新機能について説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/11/2016
ms.topic: article
ms.assetid: 04d52dff-e61b-4633-9908-be8600abc2ba
author: ChristianMontoya
manager: scottman
ms.openlocfilehash: 85d5b1e1c4367cc961ae8ea628f46f224d8dae5c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857255"
---
# <a name="whats-new-in-remote-desktop-services"></a>リモート デスクトップ サービスの新機能

リモート デスクトップ サービス (RDS) Windows Server 2016 上に構築されたは、さまざまな顧客シナリオを有効にする仮想化プラットフォームです。 RDS ソリューション全体の機能強化には、リモート デスクトップ チームとマイクロソフトの他のテクノロジ パートナーの両方によって実行される作業が組み込まれています。 次のシナリオとテクノロジは、新しい Windows Server 2016 改良されています。

また、Ignite 2016 の次の Microsoft のセッションをぜひご覧ください。「[Harness RDS improvements in Windows Server 2016 (Windows Server 2016 で RDS の機能強化を活用する)](https://channel9.msdn.com/Events/Ignite/2016/BRK3098)」。 このビデオでは、製品チームが、vGPU のサポートなど、リモート デスクトップ サービスの新機能と機能強化をすべて紹介します。 

## <a name="app-compatibility---windows-server-2016-and-windows-10"></a>アプリの互換性: Windows Server 2016 および Windows 10
Windows 10 と同じ基盤上に構築された Windows Server 2016 は、デスクトップの外観が同じだけでなく、同じアプリケーションを多数実行できます。 Windows Server 2016 とグラフィックス機能 (後述) を組み合わせると、すべてのユーザーの生産性を向上できる環境を用意できます。 

## <a name="azure-sql-database---the-new-database-for-your-highly-available-environment"></a>Azure SQL Database - 高可用性環境のための新しいデータベース
RD 接続ブローカーは、すべての展開情報 (接続状態やユーザー/ホストのマッピングなど) を Azure SQL データベースなどの共有 SQL データベースに格納できます。 SQL Server Always On 可用性グループ展開マニュアルを使用せず、Azure SQL データベースへの接続文字列を取得して、高可用性環境の使用を開始します。

追加情報:[高可用性環境のリモート デスクトップ接続ブローカーでの Azure SQL DB の使用](https://blogs.technet.microsoft.com/enterprisemobility/2016/05/03/new-windows-server-2016-capability-use-azure-sql-db-for-your-remote-desktop-connection-broker-high-availability-environment/)

## <a name="graphics---solving-graphics-needs-across-various-scenarios"></a>グラフィックス - さまざまなシナリオでグラフィックのニーズを解決する
Hyper-V の個別のデバイス割り当てにより、ホスト マシン上の GPU を VM に直接マップし、その GPU が必要なアプリケーションから使用できるようになりました。 OpenGL 4.4、OpenCL 1.1、4K の解像度、Windows Server 仮想マシンのサポートなど、RemoteFX vGPU の機能強化も行われています。

追加情報:[個別のデバイスの割り当て](https://blogs.technet.microsoft.com/virtualization/2015/11/)

## <a name="rd-connection-broker---improved-connection-handling-during-logon-storms"></a>RD 接続ブローカー - ログオン ストーム中の接続処理の改善
接続処理が改善されたことで、RD 接続ブローカーは "ログオン ストーム" の間に見られることがある 10,000 を超える同時ログオン要求を処理できるようになりました。 改善された RD 接続ブローカーは、サーバーをより迅速に環境に戻すことができるように改善され、展開の保守がより簡単になりました。

追加情報:[リモート デスクトップ接続ブローカーのパフォーマンスの向上](https://blogs.technet.microsoft.com/enterprisemobility/2015/12/15/improved-remote-desktop-connection-broker-performance-with-windows-server-2016-and-windows-server-2012-r2-hotfix-kb3091411/)

## <a name="rdp-10---new-capabilities-built-into-the-protocol"></a>RDP 10 - プロトコルに組み込まれた新機能
RDP 10 は、H.264/AVC 444 コーデックを使用して、ビデオとテキストの両方にわたって適切に最適化するようになりました。 今回のリリースでは、ペンのリモート処理もサポートされています。 これらの機能を使用すると、リモート セッションの操作感がローカル セッションのようになります。  

追加情報:[Windows 10 および Windows Server 2016 での RDP 10 AVC/H.264 の機能強化](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

## <a name="personal-session-desktops---providing-individual-desktops-to-any-end-user"></a>個人用セッション デスクトップ - 個別のデスクトップをすべてのユーザーに提供
個人用セッション デスクトップは、お客様の個人用デスクトップをクラウドでホストする新しい方法です。 管理特権と専用セッション ホストにより、ユーザーがデスクトップを個人のものと同様に管理するという複雑なホスティング環境が解消されます。

追加情報:[個人用セッション デスクトップ](rds-personal-session-desktops.md)
