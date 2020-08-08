---
title: HTTPS 通信用に HGS を構成する
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 4e708b61bd629b5b784926338b1aee122e2ecbee
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966159"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 通信用に HGS を構成する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

既定では、HGS サーバーを初期化すると、IIS web サイトは HTTP 専用通信用に構成されます。
HGS との間で送受信されるすべての機密情報は、常にメッセージレベルの暗号化を使用して暗号化されますが、高いレベルのセキュリティが求められる場合は、HGS を SSL 証明書で構成して HTTPS を有効にすることもできます。

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)]

