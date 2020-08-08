---
title: 'Windows インターネット ネーム サービス (WINS: Windows Internet Name Service)'
description: このトピックでは、WINS の使用を停止し、ネットワーク上の名前解決サービスに DNS を使用する方法について説明します。
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36dc2b0e8bbb6b65b0cc3568641017aa51122650
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955499"
---
#  <a name="windows-internet-name-service-wins"></a>Windows インターネット ネーム サービス (WINS: Windows Internet Name Service)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。

ネットワークに WINS が展開されていない場合は、WINS を展開せずに、ドメインネームシステム \( DNS を展開 \) します。 また、DNS にはコンピューター名の登録と解決のサービスが用意されており、Active Directory Domain Services との統合など、WINS よりも多くの追加の利点があります。

詳細については、「[ドメインネームシステム (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top) 」を参照してください。

ネットワークに WINS を既に展開している場合は、DNS を展開してから、WINS の使用を停止することをお勧めします。
