---
title: NIC 詳細プロパティ
description: Windows PowerShell またはネットワークコントロールパネルを使用して、Nic とすべての機能を管理できます。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 1395cefca5d9ef696eed3f2735334954b9ee02a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405712"
---
# <a name="nic-advanced-properties"></a>NIC 詳細プロパティ

[Netadapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps)コマンドレットを使用して、Windows PowerShell を使用して nic とすべての機能を管理できます。  Nic およびすべての機能は、ネットワークコントロールパネル (ncpa.cpl」) を使用して管理することもできます。 

1. **Windows PowerShell**では、nic の2つの異なる作成/モデルに対して `Get‑NetAdapterAdvancedProperties` コマンドレットを実行します。

   ![NetAdapterAdvancedProperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![NetAdapterAdvancedProperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   これら2つの NIC の詳細プロパティリストには、類似点と相違点があります。

2. **ネットワークコントロールパネル**(ncpa.cpl」) で、次の操作を行います。

   a. NIC を右クリックします。

   ![ネットワーク接続ダイアログ](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. プロパティ ダイアログボックスで、**構成** をクリックします。

    ![C1 プロパティ](../../media/network-offload-and-optimization/c1-properties.png)

   c. 詳細設定のプロパティを表示するには、 **[詳細設定]** タブをクリックします。<p>この一覧の項目は `Get-NetAdapterAdvancedProperties` 出力の項目に関連付けられています。

   ![Chelsio ネットワークアダプターのプロパティ](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---
