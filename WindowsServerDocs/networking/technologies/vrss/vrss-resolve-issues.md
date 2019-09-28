---
title: vRSS の問題を解決する
description: VRSS の負荷分散トラフィックが VM LPs に表示されない場合は、vRSS の問題を解決します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: 850aa376e8cd0060992573561a0c32af563b88ad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405159"
---
## <a name="resolve-vrss-issues"></a>vRSS の問題を解決する

すべての準備手順を完了しても、まだ VM LPs への azure の負荷分散トラフィックが表示されない場合は、さまざまな問題が発生する可能性があります。

1. 準備手順を実行する前に、vRSS は無効になりました。これで、を有効にする必要があります。 **VMNetworkAdapter**を実行して、VM の vRSS を有効にすることができます。

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS が VM またはホスト vNIC で無効になっています。 Windows Server 2016 では、既定で RSS が有効になっています。だれかが無効にした可能性があります。 

   - Enabled = **True**

   **現在の設定を表示します。** 

   Vm\(\)またはホスト vNIC \(vRSS\)のホストで、vrss 用の vm で次の PowerShell コマンドレットを実行します。

   ```PowerShell
   Get-NetAdapterRss
   ```

   **次の機能を有効にします。** 

   値を False から True に変更するには、次の PowerShell コマンドレットを実行します。

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   他のシステム全体の RSS 構成方法では、netsh を使用します。 新しく使用する機能 
   
    ```cmd
   netsh int tcp show global
   ```
   
   RSS がグローバルに無効になっていないことを確認します。 必要に応じて有効にします。 *-Set-netadapterrss では、この設定には影響しません。

3. VRSS を構成した後に VMMQ が有効になっていないことが判明した場合は、仮想スイッチに接続されている各アダプターで次の設定を確認してください。

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq-有効](../../media/vmmq-enabled.png)

   **現在の設定を表示します。** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **次の機能を有効にします。** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_ **VrssQueueSchedulingMode**を**Dynamic**に設定するときに、VMMQ (VmmqEnabled = False) を有効にすることはできません。 VMMQ が有効になっていると、VrssQueueSchedulingMode は動的に変更されません。<p>VMMQ が有効になっている場合、 **VrssQueueSchedulingMode**の**動的**なドライバーサポートが必要になります。  VMMQ は論理プロセッサ上のパケット配置のオフロードであり、そのため、動的アルゴリズムを利用するにはドライバーサポートが必要です。  動的 VMMQ をサポートする NIC ベンダーのドライバーとファームウェアをインストールしてください。



---
