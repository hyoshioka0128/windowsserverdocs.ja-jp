---
title: HGS の初期化
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: e36451c90fd543ea49989e51832ab3104d4137c0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939593"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>ホストガーディアンサービス (HGS) を初期化します

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を初期化するときに、HGS が保護されたホストの正常性を測定するために使用するモードを指定します。 相互に排他的な2つのオプションがあります。 選択するモードの背景情報については、「ホスト側の保護された[ファブリックとシールドされた VM 計画ガイド](guarded-fabric-planning-for-hosters.md)」を参照してください。

次のトピックでは、各モードの展開手順について説明します。

- [TPM-信頼された構成証明 (TPM モード)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [ホストキーの構成証明 (キーモード)](guarded-fabric-initialize-hgs-key-mode.md)
- [管理者によって信頼された構成証明 (AD モード)](guarded-fabric-initialize-hgs-ad-mode.md)

物理サーバーでこれらの手順を実行する必要があります。