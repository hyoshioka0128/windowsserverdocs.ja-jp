---
title: HGS の初期化
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 42f76dabbe150f229027909f8b58b843f31ae4e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856595"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>ホストガーディアンサービス (HGS) を初期化します

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を初期化するときに、HGS が保護されたホストの正常性を測定するために使用するモードを指定します。 相互に排他的な2つのオプションがあります。 選択するモードの背景情報については、「ホスト側の保護された[ファブリックとシールドされた VM 計画ガイド](guarded-fabric-planning-for-hosters.md)」を参照してください。

次のトピックでは、各モードの展開手順について説明します。

- [TPM-信頼された構成証明 (TPM モード)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [ホストキーの構成証明 (キーモード)](guarded-fabric-initialize-hgs-key-mode.md)
- [管理者によって信頼された構成証明 (AD モード)](guarded-fabric-initialize-hgs-ad-mode.md)

物理サーバーでこれらの手順を実行する必要があります。