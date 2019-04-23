---
title: Https 通信の HGS を構成します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 83529a5bdb4547b9881bb307a8a4cd526552d02c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829003"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 通信の HGS を構成します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

既定では、HGS サーバーを初期化するときに、HTTP のみの通信用の IIS web サイトが構成します。
HGS との間に送信されるすべての機密情報が使用して always encrypted メッセージ レベルの暗号化が、また、SSL 証明書での HGS を構成することで HTTPS を有効にできます高いレベルのセキュリティを希望する場合。

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

