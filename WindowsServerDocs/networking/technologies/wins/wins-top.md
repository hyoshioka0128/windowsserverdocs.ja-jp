---
title: Windows インターネット ネーム サービス (WINS)
description: このトピックでは、WINS の使用を停止し、DNS 名前解決サービスをネットワーク上の使用に関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5a3d132ada7b1ede83b046499058399a9da12190
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
#  <a name="windows-internet-name-service-wins"></a>Windows インターネット ネーム サービス (WINS)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名を IP アドレスにマップする従来のコンピューター名の登録と解決サービスです。

WINS は、ネットワーク上に展開があるない場合はしない展開 WINS の代わりに、ドメイン ネーム システム \(DNS\) が展開されます。 DNS は、サービスを提供コンピューター名の登録と解決もとその他の多くのメリットには WINS、経由で Active Directory ドメイン サービスとの統合などが含まれます。

詳細については、次を参照してください[ドメイン ネーム システム (DNS)。](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

ネットワーク上で、WINS が既に展開されている場合は、DNS を展開して、WINS の使用を停止することをお勧めします。
