---
title: TPM の信頼された構成証明を使用して HGS を初期化する
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b8ceebe63a586ec95b502dfea12f99d174549448
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856615"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM の信頼された構成証明を使用して HGS を初期化する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

これらの手順は、新しいフォレストまたは既存の要塞フォレストで HGS を初期化するかどうかによって異なります。

1. [新しいフォレストで HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   \- または -

   [既存の要塞フォレストの HGS クラスターを初期化する](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [信頼された TPM ルート証明書をインストールする](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [ファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns.md)

