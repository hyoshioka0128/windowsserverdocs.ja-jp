---
title: 保護されたホスト (AD) の fabric の DNS を構成します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9d302dcd06b7a3a40afbb6f613c39caaabbeba91
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443719"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>保護されたホストの fabric の DNS を構成します。

>適用先:Windows Server 2016


>[!IMPORTANT]
>AD モードでは、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 

ファブリック管理者は、DNS が HGS クラスターを解決するのには、保護されたホストできるようにするのには、ファブリックを構成する必要があります。 HGS クラスターが既にあります[HGS 管理者によってセットアップ](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)します。



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS DNS と一方向の信頼の構成](guarded-fabric-configure-dns-forwarding-and-trust.md)
