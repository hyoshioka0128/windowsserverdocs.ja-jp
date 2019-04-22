---
title: HGS 管理者によって信頼された構成証明を使用して初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 664404cb72981e162bca016df14847e684d987c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821833"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>HGS 管理者によって信頼された構成証明を使用して初期化します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) では、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 


次の手順は、新しいフォレストまたは既存の要塞フォレストでの HGS を初期化するかどうかによって異なります。

1. [新しいフォレスト (既定値) での HGS クラスターを初期化します。](guarded-fabric-initialize-hgs-ad-mode-default.md)

   - または -

   [既存の要塞フォレスト内での HGS クラスターを初期化します。](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Fabric ドメインの DNS の転送を構成します。](guarded-fabric-configuring-fabric-dns.md)

3. [DNS の転送と HGS ドメイン内の一方向の信頼を構成します。](guarded-fabric-configure-dns-forwarding-and-trust.md)



