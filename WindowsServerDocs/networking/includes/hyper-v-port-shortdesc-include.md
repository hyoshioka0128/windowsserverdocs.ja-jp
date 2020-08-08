---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms:topic: include
ms.openlocfilehash: 43a4149d44bd24a7d8b3d68ed9e3c2b68c99e285
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952845"
---
Hyper-v ポートを使用すると、Hyper-v ホスト上に構成された NIC チームは、Vm に依存しない MAC アドレスを提供します。  Hyper-v スイッチに接続されている vm の MAC アドレスまたは VM は、NIC チームのメンバー間でネットワークトラフィックを分割するために使用できます。 Hyper-v ポートの負荷分散モードを使用して、Vm 内に作成する NIC チームを構成することはできません。 代わりに、アドレスハッシュモードを使用します。