---
title: HYPER-V の第 1 世代仮想マシンのセキュリティ設定
description: 第 1 世代仮想マシンの HYPER-V マネージャーで使用できるセキュリティ設定について説明します
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 73cc2e45367d448aa736644e4a3bc02d3670fc6c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447911"
---
# <a name="generation-1-virtual-machine-security-settings"></a>第 1 世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

データと仮想マシンの状態を保護するために、HYPER-V マネージャーで第 1 世代仮想マシンのセキュリティ設定を使用します。

## <a name="encryption-support-settings-in-hyper-v-manager"></a>HYPER-V マネージャーでの暗号化のサポートの設定

次の暗号化のサポート オプションを選択してデータと、仮想マシンの状態を保護に役立てることができます。

- **状態と仮想マシンの移行のトラフィックを暗号化する**-ディスクと、ライブ マイグレーション トラフィックに書き込まれるときに、仮想マシンの保存された状態を暗号化します。

このオプションを有効にするには、仮想マシンのキー記憶域ドライブを追加する必要があります。

## <a name="key-storage-drive-in-hyper-v-manager"></a>HYPER-V マネージャーでのキー記憶域ドライブ

キー記憶域ドライブは、小規模にドライブを BitLocker キーを格納する仮想マシンを提供します。 これにより、仮想マシンを仮想化されたトラステッド プラットフォーム モジュール (TPM) チップを必要とせず、オペレーティング システム ディスクを暗号化できます。 キー記憶域ドライブの内容は、キー保護機能を使用して暗号化されます。 仮想マシンを実行するキーの保護機能 authories、HYPER-V ホスト。 両方のキー記憶域ドライブとキー保護機能の内容は、仮想マシンのランタイム状態の一部として格納されます。

キー記憶域ドライブの内容の暗号化を解除し、仮想マシンを開始するには、HYPER-V ホストがいずれかを指定する必要があります。

- この仮想マシンの承認済みの保護されたファブリックの一部または
- 仮想マシンのガーディアンのいずれかから秘密キーを所持します。

保護されたファブリックの詳細については、シールドされた Vm の概要」セクションを参照してください[セキュリティおよび保証](../../../security/Security-and-Assurance.md)します。

仮想マシンの IDE コント ローラーの 1 つの空のスロットには、キー記憶域ドライブを追加できます。 これを行うには、次のようにクリックします。**キー記憶域ドライブを追加**無料 IDE コント ローラーの最初のスロットこの仮想マシンに、キー記憶域ドライブを追加します。

## <a name="see-also"></a>関連項目

- [HYPER-V マネージャーで第 2 世代仮想マシンのセキュリティ設定](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [セキュリティおよび保証](../../../security/Security-and-Assurance.md)