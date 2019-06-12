---
title: Windows server、HYPER-V のシステム要件
description: Windows server、HYPER-V のハードウェアおよびファームウェアの要件を示します
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc4a4971-f727-40cd-91f5-2ee6d24b54cb
author: KBDAzure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 97fb1b9003705ba8ad26c2b3e71eda34e88642ee
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812622"
---
# <a name="system-requirements-for-hyper-v-on-windows-server"></a>Windows server、HYPER-V のシステム要件

>適用先:Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

HYPER-V では、特定のハードウェア要件を持ち、一部の HYPER-V 機能の追加要件があります。 この記事で詳細情報を使用すると、どのような要件を計画する方法は、HYPER-V を使用できるように、システムが満たしている必要がありますを決定できます。 その後、確認、 [Windows Server カタログ](https://www.windowsservercatalog.com/)します。 HYPER-V の要件では、仮想化環境には、多くのコンピューティング リソースが必要とするために、Windows Server 2016 の一般的な最小要件が超えていることに留意してください。

HYPER-V を既に使用している場合は、既存のハードウェアを使用すること勧めします。 全般的なハードウェア要件は、Windows Server 2012 R2 から大幅に変更していません。  しかし、シールドを使用して仮想マシンや個別のデバイスの割り当てに新しいハードウェアは必要があります。 これらの機能は、以下に示すように、特定のハードウェアのサポートに依存します。 ハードウェアの主な違いがその第 2 レベルのアドレスは、それ以外の変換 (SLAT) は必要なくことをお勧めします。

実行中の仮想マシンの数など、HYPER-V の最大のサポートされる構成の詳細については「 [Windows Server 2016 での HYPER-V のスケーラビリティの計画](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)します。 仮想マシンで実行できるオペレーティング システムの一覧は、「 [Windows サーバーにインストールされた Hyper-v のサポートされている Windows ゲスト オペレーティング システム](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)します。

## <a name="general-requirements"></a>一般的な要件

HYPER-V の機能を使用する場合に関係なく必要があります。

- 第 2 レベルのアドレス変換 (SLAT) と 64 ビット プロセッサ。 Windows ハイパーバイザーなど、HYPER-V 仮想化コンポーネントをインストールするには、SLAT が、プロセッサに必要です。 ただし、Windows PowerShell 用の仮想マシン接続 (VMConnect)、HYPER-V マネージャー、および HYPER-V コマンドレットのように、HYPER-V 管理ツールのインストールに必要はありません。 以下、「HYPER-V の要件を確認する方法」を参照してください SLAT を持つか、プロセッサを判断しますします。

- VM モードを監視する拡張機能

- メモリ不足のための計画を *少なくとも* 4 GB の RAM。 多くのメモリをお勧めします。 ホストと同時に実行するすべての仮想マシンは、十分なメモリを必要があります。

- BIOS または UEFI で仮想化のサポートをオンにします。

  - ハードウェア補助による仮想化。 これは、仮想化オプションの Intel Virtualization Technology (Intel VT) または AMD Virtualization (AMD-V) テクノロジとプロセッサ、特にプロセッサで使用できます。

  - ハードウェアによるデータ実行防止 (DEP) が利用でき、有効にされていることが必要です。 Intel システムでは、これは、XD ビット (execute disable bit)。 AMD のシステムでは、これは、NX ビット (no execute bit) です。

## <a name="how-to-check-for-hyper-v-requirements"></a>HYPER-V の要件を確認する方法

Windows PowerShell またはコマンド プロンプトと種類を開きます。

```cmd
Systeminfo.exe
```

レポートを確認する HYPER-V の要件 セクションまでスクロールします。

## <a name="requirements-for-specific-features"></a>特定の機能の要件

個別のデバイスの割り当てとシールドされたバーチャル マシンの要件を次に示します。 これらの機能の説明については、次を参照してください。[新機能については、Hyper-v で Windows Server](What-s-new-in-Hyper-V-on-Windows.md)します。

### <a name="discrete-device-assignment"></a>個別のデバイスの割り当て

**ホスト** 要件、HYPER-V の SR-IOV 機能の既存の要件に似ています。

- プロセッサは、Intel Extended Page テーブル (EPT) または AMD の Nested Page テーブル (NPT) が必要です。

- チップセットが必要です。

  - 割り込み再マップの再マップの中断機能 (VT d2) または AMD I/O メモリ管理ユニット (MMU の I/O) の任意のバージョンの Intel の vt-d です。

  - DMA の再マップのキューに登録の無効化または任意の AMD I/O MMU Intel の VT-d します。

  - Pci ルート ポートでアクセス制御サービス (ACS) します。

- ファームウェア テーブルには、Windows ハイパーバイザーに I/O MMU を公開する必要があります。 UEFI または BIOS でこの機能はオフに可能性がありますに注意してください。 手順については、ハードウェアのマニュアルを参照してください。 または、ハードウェアの製造元に問い合わせてください。

**デバイス** 必要がある GPU または非揮発性メモリ express (NVMe)。 GPU は、特定のデバイスは、個別のデバイスの割り当てをサポートします。 確認、ハードウェアのマニュアルを参照してください。 または、ハードウェアの製造元に問い合わせてください。 この機能の詳細と考慮事項、使用する方法を参照してください、投稿"[説明およびバック グラウンドで-デバイスの割り当てが不連続](https://blogs.technet.com/b/virtualization/archive/2015/11/19/discrete-device-assignment.aspx)"仮想化のブログにします。

### <a name="shielded-virtual-machines"></a>シールドされた仮想マシン

これらの仮想マシンは仮想化ベースのセキュリティに依存し、Windows Server 2016 以降で利用します。

**ホスト** の要件。

- UEFI 2.3.1c - は、セキュリティで保護された、計測されたブートをサポートしています。

  次の 2 つは一般に、仮想化ベースのセキュリティのオプションが、これらの機能を提供する保護する場合に、ホストに必要な。

- TPM のバージョン 2.0 では、プラットフォーム セキュリティの資産を保護します。
- ほとんどサポート (Intel VT-d-)、ハイパーバイザーは、ダイレクト メモリ アクセス (DMA) の保護を提供できるように

**仮想マシン** の要件。

- 第 2 世代
- Windows Server 2012 以降、ゲスト オペレーティング システムとして

