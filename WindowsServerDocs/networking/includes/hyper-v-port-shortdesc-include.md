---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server
ms:topic: include
ms.openlocfilehash: 01f231ca730a19ac0e7e868bcb7180377830afe1
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71935080"
---
Hyper-v ポートを使用すると、Hyper-v ホスト上に構成された NIC チームは、Vm に依存しない MAC アドレスを提供します。  Hyper-v スイッチに接続されている vm の MAC アドレスまたは VM は、NIC チームのメンバー間でネットワークトラフィックを分割するために使用できます。 Hyper-v ポートの負荷分散モードを使用して、Vm 内に作成する NIC チームを構成することはできません。 代わりに、アドレスハッシュモードを使用します。 