---
title: HGS の前提条件を確認する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9024557dd42ede27144bf10aa5873b6bb12d585c
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322484"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>ホストガーディアンサービスの前提条件を確認する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016


このトピックでは、hgs の前提条件と、HGS の展開を準備するための初期手順について説明します。

## <a name="prerequisites"></a>前提条件 

-   **ハードウェア**: HGS は物理マシンまたは仮想マシンで実行できますが、物理マシンを使用することをお勧めします。

    HGS を3ノードの物理クラスター (可用性) として実行する場合は、3台の物理サーバーが必要です。 (クラスタリングのベストプラクティスとして、3台のサーバーには非常に類似したハードウェアが必要です)。
  
-   **オペレーティングシステム**: ホストキーの構成証明には、 [v2 構成証明](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies)で動作する Windows Server 2019 Standard または Datacenter edition が必要です。 TPM ベースの構成証明の場合、HGS では Windows Server 2019 または Windows Server 2016 (Standard または Datacenter edition) を実行できます。

-   **サーバーの役割**: ホストガーディアンサービスとサポートサーバーの役割。

-   **ファブリック (ホスト) ドメインの構成アクセス許可/特権**: ファブリック (ホスト) ドメインと HGS ドメイン間の DNS 転送を構成する必要があります。 
    
## <a name="upgrading-hgs"></a>HGS をアップグレードしています

既に HGS を展開済みで、そのオペレーティングシステムをアップグレードする場合は、[アップグレードのガイダンス](guarded-fabric-upgrade-to-2019.md)に従って、Hgs および hyper-v サーバーを最新の OS にアップグレードします。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS の証明書を取得する](guarded-fabric-obtain-certs.md)