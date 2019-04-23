---
title: HGS の初期化
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c689a1d5f69731db0cb85a884f5af2ee0230e7be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865453"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>ホスト ガーディアン サービス (HGS) の初期化します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を初期化するときに、HGS が保護されたホストの正常性の測定に使用するモードを指定します。 相互に排他的な 2 つのオプションがあります。 背景情報を選択するモードについては、次を参照してください。[保護されたファブリックとホスト側の VM の計画ガイドのシールドされた](guarded-fabric-planning-for-hosters.md)します。

次のトピックでは、各モードの展開の手順を説明します。

- [TPM によって信頼された構成証明 (TPM モード)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [ホスト キーの構成証明 (キー モード)](guarded-fabric-initialize-hgs-key-mode.md)
- [管理者によって信頼された構成証明 (AD モード)](guarded-fabric-initialize-hgs-ad-mode.md)

物理サーバーでは、これらの手順を実行する必要があります。