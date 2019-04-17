---
title: 仮想ネットワーク アダプターで vRSS を有効にします。
description: このトピックでは、デバイス マネージャーまたは Windows PowerShell を使用して Windows server vRSS を有効にする方法について説明します。
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133418"
---
# 仮想ネットワーク アダプターで vRSS を有効にします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

仮想 RSS \(vRSS\) では、物理アダプターから仮想マシンのキュー \(VMQ\) のサポートが必要です。 VMQ が無効化またはサポートされていない場合、仮想受信側のスケーリングが無効です。 

詳細については、 [vRSS の使用を計画](vrss-plan.md)を参照してください。

## VRSS の vm を有効にします。
 
Windows PowerShell またはデバイス マネージャーを使用して vRSS を有効にするのにには、次の手順を使用します。

-   デバイス マネージャー
-   Windows PowerShell
  
### デバイス マネージャー

この手順を使用して、デバイス マネージャーを使用して vRSS を有効にすることができます。

>[!NOTE]
>この手順で最初の手順は、Windows 10 または Windows Server 2016 を実行している Vm に固有です。 VM が別のオペレーティング システムを実行している場合は、によって最初コントロール パネルを開いて、検索、デバイス マネージャーを開くデバイス マネージャーを開くことができます。
  
1.  VM タスク バーで**検索する型をここでは**、**デバイス**を入力します。 

2.  検索結果には、**デバイス マネージャー**をクリックします。

3.  デバイス マネージャーでは、**ネットワーク アダプター**を展開するクリックします。 

4.  、構成するネットワーク アダプターを右クリックし、[**プロパティ**] をクリックします。<p>ネットワーク アダプター**のプロパティ**] ダイアログ ボックスが開きます。

5.  ネットワーク アダプター**のプロパティ**では、**詳細設定**] タブをクリックします。 

6.  **プロパティ**、スクロールし、**受信側のスケーリング**をクリックします。 

7.  **値**の選択が**有効になっている**ことを確認します。 

8.  **[OK]** をクリックします。
  
> [!NOTE]
> [**詳細設定**] タブで、一部のネットワーク アダプターは、アダプターでサポートされている RSS キューの数を表示します。

---

### Windows PowerShell

Windows PowerShell を使用して vRSS を有効にするのにには、次の手順を使用します。

1. 仮想マシンで**Windows PowerShell**を開きます。

2. *AdapterName*値を交換することを確認して、次のコマンドを入力、 **-名**パラメーターを構成し、ENTER キーを押してするネットワーク アダプターの名前。 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >代わりに、次のコマンドを使用して、vRSS を有効にすることができます。
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

詳細については、 [RSS や vRSS 用の Windows PowerShell コマンド](vrss-wps.md)を参照してください。

---