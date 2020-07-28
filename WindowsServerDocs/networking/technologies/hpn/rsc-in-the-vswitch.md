---
title: vSwitch の Receive Segment Coalescing (RSC)
description: VSwitch 内の受信セグメント合体 (RSC) は、Windows Server 2019 および Windows 10 10 月2018更新プログラムの機能です。これにより、複数の TCP セグメントを少数のセグメントに結合することによって、仮想ワークロードのスループットを向上させることができます。 処理を減らす、大きなセグメント (結合) は、多数の小さなセグメントを処理するよりも効率的です。
manager: dougkim
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.author: dacuo
author: dcuomo
ms.date: 09/07/2018
ms.openlocfilehash: e7db6656bd9331e5cc6c2deaee143b3602ef1239
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181818"
---
# <a name="rsc-in-the-vswitch"></a>VSwitch 内の RSC
>適用対象:Windows Server 2019

VSwitch 内の受信セグメント合体 (RSC) は、Windows Server 2019 および Windows 10 10 月2018更新プログラムの機能です。これにより、複数の TCP セグメントを少数のセグメントに結合することによって、仮想ワークロードのスループットを向上させることができます。 処理を減らす、大きなセグメント (結合) は、多数の小さなセグメントを処理するよりも効率的です。

Windows Server 2012 以降には、受信セグメントの結合とも呼ばれる、ハードウェアのみのオフロードバージョン (物理ネットワークアダプターに実装) が含まれていました。 このオフロードバージョンの RSC は、今後のバージョンの Windows でも使用できます。 ただし、仮想ワークロードと互換性がなく、物理ネットワークアダプターが vSwitch に接続されると無効になりました。 RSC のハードウェア専用バージョンの詳細については、「 [Receive Segment 合体 (rsc)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11))」を参照してください。

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>VSwitch で RSC を利用するシナリオ

データパスが仮想スイッチを通過するワークロードでは、この機能を活用できます。

次に例を示します。

-   以下を含む仮想 Nic をホストします。

    -   ソフトウェアによるネットワーク

    -   Hyper-V ホスト

    -   記憶域スペース ダイレクト

-   Hyper-v ゲスト仮想 Nic

-   ソフトウェア定義ネットワーク GRE ゲートウェイ

-   コンテナー

この機能と互換性のないワークロードは次のとおりです。

-   ソフトウェア定義ネットワーク IPSEC ゲートウェイ

-   Sr-iov が有効な仮想 Nic

-   SMB ダイレクト

## <a name="configure-rsc-in-the-vswitch"></a>VSwitch で RSC を構成する


既定では、外部 vSwitches で RSC が有効になっています。

**現在の設定を表示します。**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**VSwitch で RSC を有効または無効にする**


>[!IMPORTANT]
>重要: vSwitch の RSC は、既存の接続に影響を与えることなく、すぐに有効または無効にすることができます。


**VSwitch で RSC を無効にする**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**VSwitch で RSC を再度有効にする**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
詳細については、「 [Set-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/set-vmswitch?view=win10-ps)」を参照してください。
