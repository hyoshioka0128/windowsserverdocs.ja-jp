---
title: HGS の初期化
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 07c40b1da829239dda5210dde0dabe485f659ae0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403585"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>ホストガーディアンサービス (HGS) を初期化します

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を初期化するときに、HGS が保護されたホストの正常性を測定するために使用するモードを指定します。 相互に排他的な2つのオプションがあります。 選択するモードの背景情報については、「ホスト側の保護された[ファブリックとシールドされた VM 計画ガイド](guarded-fabric-planning-for-hosters.md)」を参照してください。

次のトピックでは、各モードの展開手順について説明します。

- [TPM-信頼された構成証明 (TPM モード)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [ホストキーの構成証明 (キーモード)](guarded-fabric-initialize-hgs-key-mode.md)
- [管理者によって信頼された構成証明 (AD モード)](guarded-fabric-initialize-hgs-ad-mode.md)

物理サーバーでこれらの手順を実行する必要があります。