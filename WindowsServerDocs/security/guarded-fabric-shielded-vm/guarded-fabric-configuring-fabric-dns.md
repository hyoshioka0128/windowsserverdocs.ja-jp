---
title: 保護されたホストのファブリック DNS を構成する
ms.prod: windows-server
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: cb0e317a97568c13f63c0d5abd71212b2990f536
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856805"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>保護されたホストのファブリック DNS を構成する

>適用対象: Windows Server 2016

ファブリック管理者は、保護されたホストが HGS クラスターを解決できるようにするために、ファブリック DNS が必要とする構成を行う必要があります。 Hgs クラスターは、既に[hgs 管理者によって設定](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)されている必要があります。

[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>次の手順

- [HTTPS の構成](guarded-fabric-configure-hgs-https.md)
