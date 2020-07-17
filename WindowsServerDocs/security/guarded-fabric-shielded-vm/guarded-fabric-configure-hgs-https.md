---
title: HTTPS 通信用に HGS を構成する
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: de57a4026a33561760ad36fd78d732352b3aa340
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856845"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 通信用に HGS を構成する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

既定では、HGS サーバーを初期化すると、IIS web サイトは HTTP 専用通信用に構成されます。
HGS との間で送受信されるすべての機密情報は、常にメッセージレベルの暗号化を使用して暗号化されますが、高いレベルのセキュリティが求められる場合は、HGS を SSL 証明書で構成して HTTPS を有効にすることもできます。

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

