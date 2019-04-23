---
title: 仮想ネットワーク アダプターで vRSS を有効にします。
description: このトピックでは、デバイス マネージャーまたは Windows PowerShell を使用して Windows Server で vRSS を有効にする方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cb48315c-0204-4927-aa24-64f6789c2e20
manager: dougkim
ms.localizationpriority: medium
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19e8011fb98b84c20e8237792664551d2362d589
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882683"
---
# <a name="enable-vrss-on-a-virtual-network-adapter"></a>仮想ネットワーク アダプターで vRSS を有効にします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

仮想 RSS \(vRSS\)仮想マシン キューを必要と\(VMQ\) 、物理アダプターからをサポートします。 VMQ が無効になっているか、サポートされていない場合、Virtual receive-side scaling は無効です。 

詳細については、次を参照してください。 [vRSS の使用を計画](vrss-plan.md)します。

## <a name="enable-vrss-on-a-vm"></a>VM で vRSS を有効にします。
 
Windows PowerShell またはデバイス マネージャーを使用して vRSS を有効にするのにには、次の手順を使用します。

-   デバイス マネージャー
-   Windows PowerShell
  
### <a name="device-manager"></a>デバイス マネージャー

デバイス マネージャーを使用して、vRSS を有効にするのには、この手順を使用することができます。

>[!NOTE]
>この手順では、最初の手順では、Windows 10 または Windows Server 2016 を実行している Vm に固有です。 VM で別のオペレーティング システムが実行されている場合は、最初コントロール パネルを開くを検索し、デバイス マネージャーを開き、デバイス マネージャーを開くことができます。
  
1.  VM タスク バーで**ここで入力して検索**、型**デバイス**します。 

2.  検索結果では、次のようにクリックします。**デバイス マネージャー**します。

3.  デバイス マネージャーで、クリックして展開**ネットワーク アダプター**します。 

4.  クリックして、構成するネットワーク アダプターを右クリックして**プロパティ**します。<p>ネットワーク アダプター**プロパティ** ダイアログ ボックスが表示されます。

5.  ネットワーク アダプターで**プロパティ**、 をクリックして、**詳細**タブ。 

6.  **プロパティ**下へスクロールして をクリックして**Receive side scaling**します。 

7.  選択項目で**値**は**有効**します。 

8.  **[OK]** をクリックします。
  
> [!NOTE]
> **詳細** タブで、一部のネットワーク アダプターはまた、アダプターでサポートされている RSS キュー数表示します。

---

### <a name="windows-powershell"></a>Windows PowerShell

Windows PowerShell を使用して vRSS を有効にするのにには、次の手順を使用します。

1. 仮想マシンで開きます**Windows PowerShell**します。

2. 次のコマンドを交換することを確認入力、 *AdapterName*値、 **-名前**を構成し、enter するネットワーク アダプターの名前を持つパラメーター。 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >または、次のコマンドを使用して、vRSS を有効にすることができます。
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

詳細については、次を参照してください。 [RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)します。

---