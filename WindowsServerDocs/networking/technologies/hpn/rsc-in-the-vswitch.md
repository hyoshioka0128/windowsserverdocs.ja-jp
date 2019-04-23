---
title: vSwitch の Receive Segment Coalescing (RSC)
description: 受信セグメント Coalescing (RSC)、vSwitch では、Windows Server 2019 の機能と Windows 10 年 2018年 10 月の更新が少数の大きなに複数の TCP セグメントの結合での仮想ワークロードのスループットを増加ホストの CPU 使用率が軽減します。セグメント。 処理よりも効率的で (結合)、大規模な少なくのセグメントの処理が多数あり、小規模のセグメント。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.author: dacuo
author: shortpatti
ms.date: 09/07/2018
ms.openlocfilehash: 667e795e398443cadd4c966cc31e65eeee4962f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827783"
---
# <a name="rsc-in-the-vswitch"></a>VSwitch で RSC
>適用対象:Windows Server 2019

受信セグメント Coalescing (RSC)、vSwitch では、Windows Server 2019 の機能と Windows 10 年 2018年 10 月の更新が少数の大きなに複数の TCP セグメントの結合での仮想ワークロードのスループットを増加ホストの CPU 使用率が軽減します。セグメント。 処理よりも効率的で (結合)、大規模な少なくのセグメントの処理が多数あり、小規模のセグメント。

Windows Server 2012 以降では、受信 Segment Coalescing とも呼ばれるテクノロジの専用のハードウェアのオフロード バージョン (物理ネットワーク アダプターで実装) が含まれています。 RSC のオフロードされたこのバージョンは、以降のバージョンの Windows で引き続き使用できます。 ただし、仮想ワークロードと互換性がないと、vSwitch を物理ネットワーク アダプターがアタッチされると無効になりました。 RSC のハードウェアのみのバージョンの詳細については、次を参照してください。 [Receive セグメント Coalescing (RSC)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11))します。

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>RSC vSwitch で有益なシナリオ

データパスが、仮想スイッチを経由するワークロードは、この機能からメリットがあります。

例:

-   ホスト仮想 Nic を含む:

    -   ソフトウェア定義ネットワーク

    -   Hyper-V ホスト

    -   記憶域スペース ダイレクト

-   HYPER-V ゲスト仮想 Nic

-   ソフトウェア定義ネットワーク GRE ゲートウェイ

-   コンテナー

この機能と互換性がないワークロードは次のとおりです。

-   ソフトウェア定義ネットワーク IPSEC ゲートウェイ

-   SR-IOV には、仮想 Nic が有効になっています。

-   SMB ダイレクト

## <a name="configure-rsc-in-the-vswitch"></a>VSwitch の RSC を構成します。


既定では、外部の Vswitch では、RSC が有効になります。

**現在の設定を表示するには。**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**有効にするか、vSwitch の RSC を無効にします。**


>[!IMPORTANT]
>重要:VSwitch で RSC を有効になっているし、既存の接続に影響を与えずにその場で無効になっていることができます。


**VSwitch の RSC を無効にします。**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**再度、vSwitch の RSC を有効にします。**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
詳細については、次を参照してください。 [Set-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/set-vmswitch?view=win10-ps)します。
