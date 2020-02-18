---
title: Hyper-V の第 1 世代仮想マシンのセキュリティ設定
description: 第 1 世代仮想マシン向けに Hyper-V マネージャーで使用できるセキュリティ設定について説明します
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: ceb3c2628546815f9b0af35946e173f4276130d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392790"
---
# <a name="generation-1-virtual-machine-security-settings"></a>第 1 世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

Hyper-V マネージャーで第 1 世代仮想マシンのセキュリティ設定を使用して、仮想マシンのデータと状態を保護します。

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-V マネージャーでの暗号化サポートの設定

次の暗号化サポート オプションを選択することで、仮想マシンのデータと状態を保護できます。

- **状態と仮想マシンのマイグレーション トラフィックの暗号化** - ディスクに書き込む際の仮想マシンの保存された状態と、ライブ マイグレーション トラフィックを暗号化します。

このオプションを有効にするには、仮想マシンのキー記憶域ドライブを追加する必要があります。

## <a name="key-storage-drive-in-hyper-v-manager"></a>Hyper-V マネージャーのキー記憶域ドライブ

キー記憶域ドライブは、BitLocker キーを格納するための小さなドライブを仮想マシンに提供します。 これにより、仮想マシンは、仮想化されたトラステッド プラットフォーム モジュール (TPM) チップを必要とせずに、そのオペレーティング システム ディスクを暗号化できます。 キー記憶域ドライブの内容は、キーの保護機能を使用して暗号化されます。 キーの保護機能により、仮想マシンを実行する権限が Hyper-V ホストに付与されます。 キー記憶域ドライブの内容とキーの保護機能の両方が、仮想マシンのランタイム状態の一部として格納されます。

キー記憶域ドライブの内容の暗号化を解除し、仮想マシンを起動するには、Hyper-V ホストが次のいずれかである必要があります。

- この仮想マシンの承認済みの保護されたファブリックの一部であるか、
- この仮想マシンのいずれかのガーディアンからの秘密キーを持っている。

保護されたファブリックの詳細については、「[セキュリティおよび保証](../../../security/Security-and-Assurance.md)」の「シールドされた VM の概要」セクションを参照してください。

仮想マシンの IDE コントローラーの 1 つにある空のスロットにキー記憶域ドライブを追加できます。 これを行うには、 **[キー記憶域ドライブの追加]** をクリックして、この仮想マシンの最初の空き IDE コントローラー スロットにキー記憶域ドライブを追加します。

## <a name="see-also"></a>「

- [Hyper-V マネージャーの第 2 世代仮想マシンのセキュリティ設定](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [セキュリティおよび保証](../../../security/Security-and-Assurance.md)