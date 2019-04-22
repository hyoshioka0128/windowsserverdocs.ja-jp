---
title: NIC 詳細プロパティ
description: Nic と Windows PowerShell またはコントロール パネルの ネットワーク経由でのすべての機能を管理することができます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: d1a5fb57bf71fd981e001cfd9ac595ab5bc3cfc5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819903"
---
# <a name="nic-advanced-properties"></a>NIC 詳細プロパティ

Nic とを使用して Windows PowerShell を使用してすべての機能を管理することができます、 [NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps)コマンドレット。  Nic とネットワーク コントロール パネル (ncpa.cpl) を使用してすべての機能を管理することもできます。 

1. **Windows PowerShell**、実行、`Get‑NetAdapterAdvancedProperties`コマンドレットの Nic のさまざまな型/モデルを 2 つに対して。

   ![Get-netadapteradvancedproperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![Get-netadapteradvancedproperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   類似点と、これら 2 つの NIC 高度なプロパティを一覧表示の違いがあります。

2. **コントロール パネルの ネットワーク**(ncpa.cpl)、次の操作を行います。

   a.  NIC を右クリック

   ![ネットワーク接続 ダイアログ ボックス](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b.  [プロパティ] ダイアログ ボックスで、次のようにクリックします。**構成**します。

    ![C1 のプロパティ](../../media/network-offload-and-optimization/c1-properties.png)

   c. をクリックして、 **[詳細設定]** タブには、高度なプロパティを表示します。<p>このリスト内の項目が内の項目に関連付けられた、`Get-NetAdapterAdvancedProperties`出力します。

   ![Chelsio ネットワーク アダプターのプロパティ](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---