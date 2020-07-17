---
title: 保護されたホスト (AD) のファブリック DNS を構成する
ms.prod: windows-server
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5b7deafb49083ad55d5a49d1ad3c5e063e91483f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856825"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>保護されたホストのファブリック DNS を構成する

>適用対象: Windows Server 2016


>[!IMPORTANT]
>AD モードは、Windows Server 2019 以降では非推奨とされます。 TPM の構成証明が不可能な環境では、[ホストキー](guarded-fabric-initialize-hgs-key-mode.md)の構成証明を構成します。 ホストキーの構成証明により、AD モードと同様の保証が提供され、セットアップが簡単になります。 

ファブリック管理者は、保護されたホストが HGS クラスターを解決できるようにするために、ファブリック DNS が必要とする構成を行う必要があります。 Hgs クラスターは、既に[hgs 管理者によって設定](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)されている必要があります。



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS DNS と一方向の信頼の構成](guarded-fabric-configure-dns-forwarding-and-trust.md)
