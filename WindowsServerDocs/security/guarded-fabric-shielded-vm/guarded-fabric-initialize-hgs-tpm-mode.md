---
title: TPM の信頼された構成証明を使用して HGS を初期化する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c67e15aa011dbff0be5d428c8012a161d9eaea2f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386598"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM の信頼された構成証明を使用して HGS を初期化する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

これらの手順は、新しいフォレストまたは既存の要塞フォレストで HGS を初期化するかどうかによって異なります。

1. [新しいフォレストで HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   \- または -

   [既存の要塞フォレストの HGS クラスターを初期化する](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [信頼された TPM ルート証明書をインストールする](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [ファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns.md)

