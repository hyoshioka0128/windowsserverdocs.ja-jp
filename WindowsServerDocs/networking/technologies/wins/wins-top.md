---
title: Windows インターネット ネーム サービス (WINS)
description: このトピックでは、WINS の使用を停止し、ネットワーク上の名前解決サービスに DNS を使用する方法について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 219c313dfeb26319cd5f537df417724de7044648
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405248"
---
#  <a name="windows-internet-name-service-wins"></a>Windows インターネット ネーム サービス (WINS)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。

ネットワークに WINS が展開されていない場合は、WINS を展開せずに、ドメインネームシステム \(DNS\)を展開します。 また、DNS にはコンピューター名の登録と解決のサービスが用意されており、Active Directory Domain Services との統合など、WINS よりも多くの追加の利点があります。

詳細については、「[ドメインネームシステム (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top) 」を参照してください。

ネットワークに WINS を既に展開している場合は、DNS を展開してから、WINS の使用を停止することをお勧めします。
