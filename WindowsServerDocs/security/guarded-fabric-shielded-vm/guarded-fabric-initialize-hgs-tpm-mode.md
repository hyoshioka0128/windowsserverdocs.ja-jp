---
title: TPM の信頼された構成証明を使用して HGS を初期化する
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: f8d9f2f8df0a69d8faf7d6c87200b379b55749b3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939613"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM の信頼された構成証明を使用して HGS を初期化する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

これらの手順は、新しいフォレストまたは既存の要塞フォレストで HGS を初期化するかどうかによって異なります。

1. [新しいフォレストで HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   または

   [既存の要塞フォレストの HGS クラスターを初期化する](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [信頼された TPM ルート証明書をインストールする](guarded-fabric-install-trusted-tpm-root-certificates.md)
3. [ファブリック DNSの構成](guarded-fabric-configuring-fabric-dns.md)

