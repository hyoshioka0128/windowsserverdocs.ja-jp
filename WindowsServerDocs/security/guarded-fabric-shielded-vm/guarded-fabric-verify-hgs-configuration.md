---
title: HGS の構成を確認する
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8098edd1eea475cea1face5541459b262364a07b
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469552"
---
# <a name="verify-the-hgs-configuration"></a>HGS の構成を確認する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


次に、モ ノが想定どおりに動作するかを検証する必要があります。 これを行うには、管理者特権での Windows PowerShell コンソールで、次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS の構成で保護されたファブリックに追加するホストに関する情報がまだ含まれないため、診断はホストできなくなるなしに、まだ正常に証明を示します。 この結果を無視し、診断によって提供されるその他の情報を確認します。

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

HGS クラスター内の各ノードで、診断を実行します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [保護されたホストの展開](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

