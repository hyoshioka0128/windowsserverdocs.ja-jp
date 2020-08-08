---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms:topic: include
ms.openlocfilehash: f07840220dbbe955a47879b3090ddd340c8c514f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952846"
---
動的では、TCP ポートと IP アドレスのハッシュに基づいて、送信負荷が分散されます。 また、動的モードでは、特定の送信フローがチームメンバー間を行き来するように、リアルタイムでの読み込みがバランスされます。 一方、受信の負荷は、Hyper-v ポートと同じ方法で配布されます。 簡単に言うと、動的モードでは、アドレスハッシュと Hyper-v ポートの両方の最適な側面が利用されます。これは、最もパフォーマンスの高い負荷分散モードです。

