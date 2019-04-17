---
title: Windows Admin Center に関連する管理ソリューション
description: Windows Admin Center のと比較すると、他の Microsoft の監視および管理ソリューション/製品 (Project Honolulu) を補完
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f7bf0e32b1156fe361c79ac4ccd0e3536df767e2
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296714"
---
# Windows Admin Center と Microsoft からの関連する管理ソリューション

>適用対象: Windows Admin Center、Windows Admin Center Preview

[Windows Admin Center](windows-admin-center.md)は、状況で使用したリモート デスクトップ (RDP) のトラブルシューティングや構成用のサーバーに接続するための従来のインボックス サーバー管理ツールの進化したものです。 その他の既存の Microsoft 管理ソリューション; を置換するためのものがありません。代わりに次のように、これらのソリューションを補完します。

## リモート サーバー管理ツール (RSAT)

[リモート サーバー管理ツール (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) 、GUI と PowerShell ツール オプションのロールと Windows Server の機能を管理するためのコレクションです。 RSAT は、Windows Admin Center がない多くの機能があります。 追加される可能性最もよく使用されるツールの一部 RSAT で Windows Admin Center を今後します。 すべての新しい Windows サーバーの役割または管理の GUI を必要とする機能は、Windows Admin Center になります。

## Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune)は、ポリシーのセットに基づいて、iOS、Android、Windows、macOS、デバイスを管理できる、クラウド ベースのエンタープライズ モビリティ管理サービスです。 Intune は、有効にすると、従業員がアクセスして情報を共有する方法を制御することで、会社についての情報をセキュリティで保護することについて説明します。 これに対し、Windows Admin Center は、ポリシーに基づいて動作ではありませんが、WinRM 経由でリモート PowerShell と WMI を使用して、Windows 10 および Windows Server システムのアドホック管理が可能します。

## Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/)はできるように、データ センターから Azure サービスを提供するため、ハイブリッド クラウド プラットフォームです。 Azure スタックは、PowerShell またはアクセスし、従来の Azure サービスを管理するために使用する従来の Azure portal に似た管理者ポータルを使って管理されます。 Windows Admin Center は、Azure Stack のインフラストラクチャを管理するものが、 [Azure IaaS 仮想マシンの管理](../azure/manage-azure-vms.md)(Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している) に使用したり、個々 の物理のトラブルシューティングAzure Stack 環境に展開されたサーバー。

## System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center)は、オンプレミス データ センター管理ソリューションの展開、構成、管理、データ センター全体の監視します。 System Center では、Windows Admin Center では、特定のサーバーを管理またはさらに細かくツールのトラブルシューティングにドリルダウンできます。 環境内のすべてのシステムの状態を確認できます。

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **について再考しました「インボックス」プラットフォーム & ツール** | **データ センター管理 & の監視** |
| Windows Server ライセンス –**追加コストなし**、MMC などの従来のインボックス ツールと同様に含まれています。 | **包括的、環境とプラットフォーム間で追加の値のソリューション** |
| **軽量な**ブラウザー ベースのリモート管理、Windows Server インスタンスの**任意の場所**です。代わりに、RDP | _AMP_ モニター**異種**システムに**拡大縮小**HYPER-V、VMware、Linux などの管理します。 |
|**ディープ**1 台のサーバー & 単一のクラスター ドリルダウン トラブルシューティング、構成 & メンテナンス|インフラストラクチャを提供できます。オートメーションとセルフ サービスです。 インフラストラクチャとワークロードの**多様性**の監視|
|**個別**2 ~ 4 ノード**HCI**クラスター、HYPER-V、記憶域スペース ダイレクトおよび SDN の統合の最適化された管理|展開 & HYPER-V、SCVMM の**ベア メタル**から**データ センターの倍率**で Windows Server のクラスターを管理します。|
|**HCI を監視する**だけです。クラスターの正常性のサービスは、履歴を保存します。 ファーストおよびサード パーティ製の**管理ツールの拡張機能**の拡張可能なプラットフォーム|**拡張可能な** & **スケーラブルな監視**プラットフォームを SCOM で警告が通知, 通知, 監視のためのサード パーティ製ワークロードに履歴の SQL|
|**ハイブリッド**; する最も簡単なブリッジオンボードし、さまざまなデータ保護、レプリケーション、更新プログラムとの Azure サービスの使用|**組み込み**のデータ保護、レプリケーション、更新プログラム (DPM/VMM/SCCM)。 Log Analytics とサービス マップとハイブリッドの統合|
|Windows Server の**プラットフォームの機能が点灯**を:、ストレージ移行サービス、記憶域レプリカ、システム インサイトなどです。|**その他のプラットフォーム**: Orchestrator/SMA で自動化します。その他の SCSM & との統合サービスの管理ツール|

#### ターゲットの値を個別に提供各**相乗効果**と補完的な機能です。
