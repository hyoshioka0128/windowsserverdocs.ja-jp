---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms.prod: windows-server
ms:topic: include
ms.openlocfilehash: 47a91c86ac75aedf532289055c94b34899fa01df
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316480"
---
Hyper-v ポートを使用すると、Hyper-v ホスト上に構成された NIC チームは、Vm に依存しない MAC アドレスを提供します。  Hyper-v スイッチに接続されている vm の MAC アドレスまたは VM は、NIC チームのメンバー間でネットワークトラフィックを分割するために使用できます。 Hyper-v ポートの負荷分散モードを使用して、Vm 内に作成する NIC チームを構成することはできません。 代わりに、アドレスハッシュモードを使用します。 