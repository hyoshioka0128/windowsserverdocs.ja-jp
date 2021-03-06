---
title: TPM によって信頼された構成証明を使用して HGS を初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 672054462437b615236dfc4f00c8b20c946f11a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882333"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM によって信頼された構成証明を使用して HGS を初期化します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

次の手順は、新しいフォレストまたは既存の要塞フォレストでの HGS を初期化するかどうかによって異なります。

1. [新しいフォレスト (既定値) での HGS クラスターを初期化します。](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   - または -

   [既存の要塞フォレスト内での HGS クラスターを初期化します。](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [信頼済み TPM ルート証明書をインストールします。](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [Fabric の DNS を構成します。](guarded-fabric-configuring-fabric-dns.md)

