---
title: Windows Admin Center 関連の管理ソリューション
description: Windows Admin Center が他の Microsoft 監視および管理ソリューション/製品 (Project Honolulu) とどのように比肩し補完するか
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d681e5007cd3ae3c14de774df0bc85abc23b51d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406832"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center と Microsoft の関連する管理ソリューション

>適用先:Windows Admin Center、Windows Admin Center Preview

[Windows Admin Center](windows-admin-center.md) は、従来のインボックス サーバー管理ツールを進化させたもので、トラブルシューティングまたは構成のためにリモート デスクトップ (RDP) を使用してサーバーに接続した可能性のある状況に対するものです。 これは、その他の既存の Microsoft 管理ソリューションを置き換えるものではなく、むしろ、以下に説明するように、これらのソリューションを補完するものです。

## <a name="remote-server-administration-tools-rsat"></a>リモート サーバー管理ツール (RSAT)

[リモート サーバー管理ツール (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) は、Windows Server のオプションのロールや機能を管理する GUI および PowerShell ツールをまとめたものです。 RSAT には、Windows Admin Center にはない多くの機能があります。 今後、RSAT でよく使用されているツールのいくつかが、Windows Admin Center に追加されるかもしれません。 管理に GUI を必要とする 新しい Windows サーバーのロールまたは機能はすべて、Windows Admin Center にあります。

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) は、一連のポリシーに基づいて、iOS、Android、Windows、および macOS デバイスを管理できる、クラウド ベースのエンタープライズ モビリティ管理サービスです。 Intune は、従業員が情報にアクセスして共有する方法を制御することにより、会社の情報をセキュリティで保護できるようにすることを重視しています。 対照的に、Windows Admin Center はポリシー主導ではありませんが、PowerShell および WMI over WinRM を使用して、Windows 10 と Windows Server システムのアドホック管理を有効にします。

## <a name="azure-stack"></a>Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) は、データ センターから Azure サービスを提供できるようにするハイブリッド クラウド プラットフォームです。 Azure Stack は、PowerShell または管理者ポータルを使用して管理されます。このポータルは、従来の Azure サービスにアクセスして管理するために使用される従来の Azure portal に類似しています。 Windows Admin Center は Azure Stack インフラストラクチャを管理するように意図されていませんが、これを使用して、(Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している) [Azure IaaS 仮想マシンを管理](../azure/manage-azure-vms.md)したり、Azure Stack 環境に展開されている個々 の物理サーバーをトラブルシューティングしたりできます。

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) は、データ センター全体の展開、構成、管理、監視を行うためのオンプレミスのデータ センター管理ソリューションです。 System Center では環境内のすべてのシステムのステータスを確認できますが、Windows Admin Center では、特定のサーバーにドリル ダウンして、より詳細なツールで管理またはトラブルシューティングすることができます。

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **一新された "インボックス" プラットフォームおよびツール** | **データセンターの管理および監視** |
| Windows Server ライセンスに付属 – **追加コストなし**、MMC やその他の従来のインボックス ツールと同様 | 環境およびプラットフォームにわたる追加の値に対するソリューションの**包括的**なスイート |
| **軽量**、Windows Server インスタンスのブラウザー ベースのリモート管理、**任意の場所**; RDP の代替 | Hyper-V、VMware、Linux など**大規模**な**異種**システムを管理および監視 |
|トラブルシューティング、構成、およびメンテナンスに対する**ディープ**な単一サーバーおよび単一クラスターのドリルダウン|インフラストラクチャ プロビジョニング; 自動化およびセルフ サービス; インフラストラクチャおよびワークロードの監視**幅**|
|Hyper-V、記憶域スペース ダイレクト、および SDN を統合した、**個別**の 2 から 4 のノード **HCI** クラスターの最適化された管理|SCVMM を使用して**ベア メタル**から**データ センター規模**で Hyper-V、Windows Server クラスターを展開および管理|
|**HCI で監視**のみ; クラスター正常性サービスは履歴を格納します。 1 番目と 3 番目のパーティ**管理ツール拡張機能**の拡張可能なプラットフォーム|アラート、通知、サード パーティ製負荷監視を備えた SCOM での**拡張可能** & **スケーラブルな監視**プラットフォーム; 履歴用 SQL|
|**ハイブリッド**への最も簡単なブリッジ; オンボードであり、データ保護、レプリケーション、更新プログラムなどにさまざまな Azure サービスを使用|**組み込み**データ保護、レプリケーション、更新プログラム (DPM/VMM/SCCM)。 Log Analytics および Service Map とのハイブリッド統合|
|次の Windows Server の**プラットフォーム機能に焦点を当てます**。Storage Migration Service、Storage Replica、System Insights など。|**追加のプラットフォーム**:Orchestrator/SMA での自動化。SCSM およびその他のサービス管理ツールとの統合|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>それぞれは独立して目標値を提供します; 補完機能と**一緒に使用するとより適切**です。
