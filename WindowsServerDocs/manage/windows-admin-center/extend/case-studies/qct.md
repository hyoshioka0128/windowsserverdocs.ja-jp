---
title: Windows 管理センター SDK ケーススタディ-QCT
description: Windows 管理センター SDK ケーススタディ-QCT
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2922bcdd08fac7bf2179a0ebbad37c7151d660b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357250"
---
# <a name="qct-management-suite-extension"></a>QCT Management Suite 拡張機能

## <a name="a-simple-path-to-server-infrastructure-management"></a>サーバーインフラストラクチャ管理の単純なパス

Windows 管理センター用 QCT Management Suite 拡張機能には、システム構成を監視し、 [qct AZURE STACK HCI 認定システム](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/windows-server-software-defined-solution-wssd/)のサーバーの正常性を管理するための1つのウィンドウが表示されます。[QUANTAGRID D52BQ](https://www.qct.io/product/index/Server/rackmount-server/2U-Rackmount-Server/QuantaGrid-D52BQ-2U)、 [QuantaGrid D52T-1ulh](https://www.qct.io/product/index/Storage/Storage-Server/1U-Storage-Server/QuantaGrid-D52T-1ULH) And [QuantaPlex T21P-4u](https://www.qct.io/product/index/Storage/Storage-Server/4U-Storage-Server/QuantaPlex-T21P-4U)。

QCT は、既存の監視と管理に関する顧客の問題点に基づいており、システムイベントログの概要、ドライバーの監視、ハードウェアコンポーネントの正常性を含む機能を提供します。管理エクスペリエンス。

![QCT 拡張機能](../../media/extend-case-study-qct/D52T_DarkMode_Disk-Detail-General.PNG)

QCT Management Suite は、次の主要な機能を備えた Windows 管理センターの機能を拡張します。
- **ワンクリック専用のハードウェア管理**-直感的なユーザーインターフェイスには、モデル名、プロセッサ、メモリ、BIOS などのハードウェア情報が表示されます。 IT 管理者は、簡単なワンクリック UI で BMC を再起動できます。

![QCT 拡張機能](../../media/extend-case-study-qct/D52T_Overview.PNG)

- **効率的なサービスサポートのためのディスクマッピングと led の識別**-Qct Management Suite ウィザードの UI デザインでは、選択した各ディスクのスロットが、ディスクプロファイルの概要と、選択したディスクの led ライトコントロールによって効率的に置換されます。

![QCT 拡張機能](../../media/extend-case-study-qct/T21P_disk_mapping.png)

- ハードウェアイベントログと正常性状態用の使いやすい監視ツール。

![QCT 拡張機能](../../media/extend-case-study-qct/D52T_event_log.PNG)

- **予測的なディスク管理**-システムの状態と、エラーの発生前に組織がアクションを実行できるようにする異常な通知を使用して評価します。

![QCT 拡張機能](../../media/extend-case-study-qct/T21P_SMART.PNG)

Windows 管理センターの QCT Management Suite の詳細については、次を参照してください。
- [QCT Management Suite の web ページ](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/)
- [QCT Management Suite のデータシート](https://go.qct.io/wp-content/uploads/2019/04/WAC-data-sheet_v04222019.pdf)