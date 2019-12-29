---
title: Hyper-v の第1世代仮想マシンセキュリティ設定
description: 第1世代仮想マシン用 Hyper-v マネージャーで使用できるセキュリティ設定について説明します。
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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392790"
---
# <a name="generation-1-virtual-machine-security-settings"></a>第1世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

Hyper-v マネージャーで、第1世代の仮想マシンのセキュリティ設定を使用して、仮想マシンのデータと状態を保護します。

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-v マネージャーでの暗号化サポートの設定

次の暗号化サポートオプションを選択すると、仮想マシンのデータと状態を保護することができます。

- **[状態と仮想マシンの移行トラフィックを暗号化**する]-仮想マシンの保存された状態がディスクとライブマイグレーションのトラフィックに書き込まれるときに、その状態を暗号化します。

このオプションを有効にするには、仮想マシンのキー記憶域ドライブを追加する必要があります。

## <a name="key-storage-drive-in-hyper-v-manager"></a>Hyper-v マネージャーのキー記憶域ドライブ

キーストレージドライブは、BitLocker キーを格納するための小さなドライブを仮想マシンに提供します。 これにより、仮想化されたトラステッドプラットフォームモジュール (TPM) チップを必要とせずに、仮想マシンがそのオペレーティングシステムディスクを暗号化できるようになります。 キーのストレージドライブの内容は、キー保護機能を使用して暗号化されます。 キーの保護機能は、仮想マシンを実行するために Hyper-v ホストを提供します。 キーストレージドライブの内容とキー保護機能の両方が、仮想マシンのランタイム状態の一部として格納されます。

キー記憶域ドライブの内容の暗号化を解除し、仮想マシンを起動するには、Hyper-v ホストが次のいずれかである必要があります。

- この仮想マシンの承認された保護されたファブリックの一部、または
- 仮想マシンのいずれかのガーディアンからの秘密キーを取得します。

保護されたファブリックの詳細については、「[セキュリティと保証](../../../security/Security-and-Assurance.md)」の「シールドされた Vm の概要」セクションを参照してください。

仮想マシンの IDE コントローラーの1つに、空のスロットにキーストレージドライブを追加することができます。 これを行うには、 **[キー記憶域ドライブの追加]** をクリックして、この仮想マシンの最初の空き IDE コントローラースロットにキー記憶域ドライブを追加します。

## <a name="see-also"></a>関連項目

- [Hyper-v マネージャーでの第2世代仮想マシンのセキュリティ設定](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [セキュリティおよび保証](../../../security/Security-and-Assurance.md)