---
title: vRSS の問題を解決する
description: 負荷分散のトラフィックを VM Lp vRSS が表示されない場合は、vRSS 問題を解決します。
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
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232521"
---
## vRSS の問題を解決する

すべての準備の手順を完了したまま、負荷分散のトラフィックを VM Lp vRSS 表示されない場合は、さまざまな考えられる問題があります。

1. 準備の手順を実行する前に、vRSS が無効にし、これで、有効にする必要があります。 VM の vRSS を有効にする**設定 VMNetworkAdapter**を実行できます。

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. VM のまたはホスト vNIC RSS が無効です。 既定では Windows Server 2016 により、RSS他のユーザーが無効にします。 

   - 有効になっている = **True**

   **現在の設定を表示するには。** 

   (用で、VM\ vRSS) VM\ で次の PowerShell コマンドレットを実行またはホストで \ (ホスト vNIC vRSS\) 用です。

   ```PowerShell
   Get-NetAdapterRss
   ```

   **この機能を有効にします。** 

   True から False 値を変更するには、次の PowerShell コマンドレットを実行します。

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   RSS を構成する別のシステム全体の方法では、netsh を使用しています。 使用 
   
    ```cmd
   netsh int tcp show global
   ```
   
   確認してその RSS がないグローバルに無効にします。 必要な場合に有効にします。 この設定によって影響のない *-NetAdapterRSS します。

3. VMMQ が有効でない vRSS を構成した後場合は、仮想スイッチに接続されている各アダプターでは、次の設定を確認します。

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq 有効になっています。](../../media/vmmq-enabled.png)

   **現在の設定を表示するには。** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **この機能を有効にします。** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_ VMMQ を有効にすることはできません (VmmqEnabled = False) **VrssQueueSchedulingMode**を**動的**に設定します。 VMMQ が有効にすると、VrssQueueSchedulingMode は動的に変更されません。<p>**動的**の**VrssQueueSchedulingMode**では、VMMQ が有効にすると、ドライバーのサポートが必要です。  VMMQ の論理プロセッサ上でパケットの配置のオフロードにして、ように、動的なアルゴリズムを活用するドライバーのサポートが必要です。  NIC のベンダーのドライバーおよびファームウェアの動的な VMMQ をサポートしているをインストールしてください。



---
