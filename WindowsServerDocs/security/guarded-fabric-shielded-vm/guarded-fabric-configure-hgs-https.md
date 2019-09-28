---
title: Https 通信用に HGS を構成する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f0cbf6a6dc1970499758a6a48bfaadb95c464ec1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403675"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 通信用に HGS を構成する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

既定では、HGS サーバーを初期化すると、IIS web サイトは HTTP 専用通信用に構成されます。
HGS との間で送受信されるすべての機密情報は、常にメッセージレベルの暗号化を使用して暗号化されますが、高いレベルのセキュリティが求められる場合は、HGS を SSL 証明書で構成して HTTPS を有効にすることもできます。

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

