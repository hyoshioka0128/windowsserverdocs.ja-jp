---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server
ms:topic: include
ms.openlocfilehash: ba2723e4387620154187fe20c3bd80c5ce3fc929
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71935062"
---
動的では、TCP ポートと IP アドレスのハッシュに基づいて、送信負荷が分散されます。 また、動的モードでは、特定の送信フローがチームメンバー間を行き来するように、リアルタイムでの読み込みがバランスされます。 一方、受信の負荷は、Hyper-v ポートと同じ方法で配布されます。 簡単に言うと、動的モードでは、アドレスハッシュと Hyper-v ポートの両方の最適な側面が利用されます。これは、最もパフォーマンスの高い負荷分散モードです。 

