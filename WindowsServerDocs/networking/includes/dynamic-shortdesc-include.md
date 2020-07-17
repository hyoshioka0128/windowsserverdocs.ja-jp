---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms.prod: windows-server
ms:topic: include
ms.openlocfilehash: f2065acb89af4bed4dc525453bb5a294a4e2c3ef
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316513"
---
動的では、TCP ポートと IP アドレスのハッシュに基づいて、送信負荷が分散されます。 また、動的モードでは、特定の送信フローがチームメンバー間を行き来するように、リアルタイムでの読み込みがバランスされます。 一方、受信の負荷は、Hyper-v ポートと同じ方法で配布されます。 簡単に言うと、動的モードでは、アドレスハッシュと Hyper-v ポートの両方の最適な側面が利用されます。これは、最もパフォーマンスの高い負荷分散モードです。 

