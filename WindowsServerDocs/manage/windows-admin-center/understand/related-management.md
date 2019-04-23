---
title: Windows Admin Center に関連する管理ソリューション
description: Windows Admin Center のと比較すると、他の Microsoft の監視と管理のソリューション/製品 (プロジェクト ホノルル) を補完するもの
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 385a066cb828f58d698c2ca47e0553e996a77733
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847323"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center と Microsoft の関連する管理ソリューション

>適用先:Windows Admin Center、Windows Admin Center プレビュー

[Windows Admin Center](windows-admin-center.md)管理ツールを使用したリモート デスクトップ (RDP) は、トラブルシューティングまたは構成サーバーに接続する場合は、従来のボックスでサーバーの進化します。 その他の既存の Microsoft 管理ソリューションです。 を置き換えるためのものがありません。はなく以下に示すように、これらのソリューションを補完します。

## <a name="remote-server-administration-tools-rsat"></a>リモート サーバー管理ツール (RSAT)

[リモート サーバー管理ツール (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)は省略可能な役割と Windows Server の機能を管理する GUI ツールと PowerShell のツールのコレクションです。 RSAT では、Windows Admin Center でない多くの機能があります。 います可能性があります、最もよく使用されるツールの一部 RSAT で Windows Admin Center を将来に追加します。 任意の新しい Windows サーバーの役割または機能の管理 GUI を必要とするは、Windows Admin Center になります。

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune)はクラウド ベースのエンタープライズ モビリティ管理サービス、一連のポリシーに基づいて、iOS、Android、Windows、および macOS デバイスを管理することができます。 Intune は、従業員のアクセスし、情報を共有を制御することで会社の情報をセキュリティで保護できるようにすることについて説明します。 これに対し、Windows Admin Center では、ポリシー主導ではありませんが、WinRM 経由でリモートの PowerShell および WMI を使用して Windows 10 および Windows Server のシステムの臨機応変に管理を有効します。

## <a name="azure-stack"></a>Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/)は、データ センターから Azure サービスを提供することができます、ハイブリッド クラウド プラットフォームです。 Azure Stack は、PowerShell またはアクセスし、従来の Azure サービスを管理するために使用する従来の Azure portal に類似した管理者ポータルを使用して管理されます。 Windows Admin Center は、Azure Stack インフラストラクチャの管理を目的として、クエリを使用することができますが、 [Azure IaaS 仮想マシンの管理](../configure/manage-azure-vms.md)(Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している) やトラブルシューティングを行うAzure Stack 環境にデプロイされている個々 の物理サーバー。

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center)の展開、構成、管理、データ センター全体の監視、オンプレミス データ センター管理ソリューションです。 System Center では、Windows Admin Center では、特定のサーバーを管理またはより詳細なツールを使用してトラブルシューティングにドリル ダウンできます。 は、環境内のすべてのシステムのステータスを確認できます。

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **一新「ボックス」プラットフォームとツール** | **データ センター管理と監視** |
| Windows Server ライセンス – に含まれる**追加コストなし**MMC とその他の従来のインボックス ツールと同様に、 | **包括的な**さらなる価値を環境やプラットフォーム間でのソリューションのスイート |
| **ライトウェイト**、Windows Server のインスタンスのブラウザー ベースのリモート管理**任意の場所**RDP に代わる; | 管理し、監視**異種**システム**大規模**(HYPER-V、VMware、Linux など) |
|**ディープ**1 台のサーバーと単一のクラスターのドリルダウンのトラブルシューティング、構成とメンテナンス|インフラストラクチャを提供できます。自動化やセルフ サービスです。 インフラストラクチャとワークロードの監視**幅**|
|管理に最適化された**個々**2. ~ 4. ノード**HCI**クラスターでは、HYPER-V、記憶域スペース ダイレクトと SDN を統合します。|展開 (&)、HYPER-V を管理、Windows Server クラスター**データ センターのスケール**から**ベア メタル**SCVMM と|
|**HCI の監視**のみで、クラスターの正常性サービスは履歴を格納します。 1 番目と 3 番目のパーティの拡張可能なプラットフォーム**管理ツールの拡張機能**|**拡張可能な** & **拡張性の高い監視**scom で、アラート、通知、監視、サード パーティ製のワークロードのプラットフォーム履歴用の SQL|
|最も簡単な仲介役を**ハイブリッド**; オンボードのさまざまなデータ保護、レプリケーション、更新プログラムおよび Azure サービスを使用して、|**組み込み**データ保護、レプリケーション、更新プログラム (DPM/VMM/SCCM)。 Log Analytics と Service Map とハイブリッド統合|
|**プラットフォーム機能が点灯**の Windows Server:記憶域サービスの移行、記憶域レプリカでは、システム Insights など。|**追加のプラットフォーム**:Orchestrator または SMA の自動化します。SCSM & その他のサービス管理ツールとの統合|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>対象の値を個別に送信各**相乗効果**補完的な機能を使用します。
