---
title: vRSS の問題を解決する
description: 負荷分散トラフィックが VM LPs に vRSS が表示されない場合は、vRSS 問題を解決します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: a2d6eb43149361b4270565b63fc99f483f364f74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824033"
---
## <a name="resolve-vrss-issues"></a>vRSS の問題を解決する

すべての準備手順を完了しても、vRSS が負荷分散トラフィックが VM LPs に表示されない場合は、さまざまな考えられる問題があります。

1. 準備手順を実行する前に、vRSS が無効になっているのと、今すぐ有効にする必要があります。 実行することができます**Set-vmnetworkadapter** VM の vRSS を有効にします。

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS は、VM またはホスト vNIC に無効にされました。 既定では RSS を有効に Windows Server 2016だれかが可能性がありますがこれを無効にします。 

   - 有効になっている =**は True。**

   **現在の設定を表示するには。** 

   VM で、次の PowerShell コマンドレットを実行\(VM で vRSS を\)またはホストで\(ホスト vNIC vRSS の\)します。

   ```PowerShell
   Get-NetAdapterRss
   ```

   **この機能を有効にします。** 

   True から False 値を変更するには、次の PowerShell コマンドレットを実行します。

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   RSS を構成する別の全体的な方法は、netsh を使用しています。 使用 
   
    ```cmd
   netsh int tcp show global
   ```
   
   確認するグローバルを RSS で無効はありません。 必要な場合に有効にします。 この設定は変更されません *-NetAdapterRSS します。

3. VRSS を構成した後、VMMQ が有効にしない場合は、仮想スイッチに接続されている各アダプターでは、次の設定を確認します。

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq 対応](../../media/vmmq-enabled.png)

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **この機能を有効にします。** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_ VMMQ を有効にすることはできません (VmmqEnabled = False) の設定中に**VrssQueueSchedulingMode**に**動的**します。 VrssQueueSchedulingMode は VMMQ が有効にすると動的に変更します。<p>**VrssQueueSchedulingMode**の**動的**VMMQ が有効にすると、ドライバーのサポートを必要とします。  VMMQ、オフロードの論理プロセッサ上でパケットの配置は、そのため、動的アルゴリズムを活用するドライバーのサポートが必要です。  NIC ベンダーのドライバーと動的 VMMQ をサポートしているファームウェアをインストールしてください。



---
