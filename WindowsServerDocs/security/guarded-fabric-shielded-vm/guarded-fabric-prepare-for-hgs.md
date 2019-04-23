---
title: HGS の前提条件を確認します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: dddf694aaceab93bd102456dbe86df17a001cb01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879883"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>ホスト ガーディアン サービスの前提条件を確認します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


このトピックでは、HGS の前提条件と HGS 展開を準備する初期手順について説明します。

## <a name="prerequisites"></a>前提条件 

-   **ハードウェア**:HGS は、物理または仮想のマシンで実行できますが、物理マシンはお勧めします。

    (可用性) の 3 つのノードの物理クラスターとして HGS を実行する場合は、次の 3 つの物理サーバーが必要です。 (クラスター化するためのベスト プラクティスとして、次の 3 つのサーバーが必要非常に類似するハードウェアです。)
  
-   **オペレーティング システム**:Windows Server 2019 Standard または Datacenter edition で動作してホスト キーの構成証明が必要と[v2 構成証明](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies)します。 HGS には、TPM ベースの構成証明は、Windows Server 2019 または Windows Server 2016、Standard または Datacenter edition を実行できます。

-   **サーバーの役割**:ホスト ガーディアン サービスとサーバーの役割をサポートします。

-   **ファブリック (ホスト) ドメインの構成のアクセス許可/特権**:ファブリック (ホスト) と HGS ドメイン間で DNS 転送を構成する必要があります。 
    
## <a name="upgrading-hgs"></a>HGS のアップグレード

HGS 既にデプロイ済みのオペレーティング システムをアップグレードする場合は、に従って、[アップグレード ガイダンスについて](guarded-fabric-upgrade-to-2019.md)HGS および HYPER-V サーバーを最新の OS にアップグレードします。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[HGS の証明書を取得します。](guarded-fabric-obtain-certs.md)