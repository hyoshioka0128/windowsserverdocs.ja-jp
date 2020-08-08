---
title: NIC 詳細プロパティ
description: Windows PowerShell またはネットワークコントロールパネルを使用して、Nic とすべての機能を管理できます。
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: ce9c4049ab701d647701029f41d2570b7fc8cd03
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997653"
---
# <a name="nic-advanced-properties"></a>NIC 詳細プロパティ

[Netadapter](/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps)コマンドレットを使用して、Windows PowerShell を使用して nic とすべての機能を管理できます。  Nic およびすべての機能は、ネットワークコントロールパネル (ncpa.cpl) を使用して管理することもできます。

1. **Windows PowerShell**では、 `Get‑NetAdapterAdvancedProperties` nic の2つの異なる作成/モデルに対してコマンドレットを実行します。

   ![NetAdapterAdvancedProperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![NetAdapterAdvancedProperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   これら2つの NIC の詳細プロパティリストには、類似点と相違点があります。

2. **ネットワークコントロールパネル**(ncpa.cpl) で、次の操作を行います。

   a. NIC を右クリックします。

   ![ネットワーク接続ダイアログ](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. [プロパティ] ダイアログボックスで、[**構成**] をクリックします。

    ![C1 プロパティ](../../media/network-offload-and-optimization/c1-properties.png)

   c. 詳細設定のプロパティを表示するには、[**詳細設定**] タブをクリックします。<p>この一覧の項目は、出力の項目に関連付けられて `Get-NetAdapterAdvancedProperties` います。

   ![Chelsio ネットワークアダプターのプロパティ](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---