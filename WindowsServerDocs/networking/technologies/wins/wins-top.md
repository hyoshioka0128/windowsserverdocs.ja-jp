---
title: Windows インターネット ネーム サービス (WINS)
description: このトピックでは、WINS を使用停止と、DNS、ネットワーク上の名前解決サービスを使用するについて説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bbc1871d29021aa3c99f14368a4711dac63f4cee
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843633"
---
#  <a name="windows-internet-name-service-wins"></a>Windows インターネット ネーム サービス (WINS)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows インターネット ネーム サービス (WINS) は、コンピューターの NetBIOS 名と IP アドレスを対応付け、コンピューター名の登録と解決を行う従来型サービスです。

ネットワークに展開されている WINS がいない場合はいない展開 WINS の代わりに、ドメイン ネーム システムを展開\(DNS\)します。 DNS は、コンピューター名の登録と解決サービスを提供しますもとその他の多くのメリットには WINS、経由で Active Directory Domain Services との統合などが含まれます。

詳細については、次を参照してください[ドメイン ネーム システム (DNS)。](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

ネットワーク上、WINS が既に展開されている場合は、DNS の展開し、WINS の使用を停止することをお勧めします。
