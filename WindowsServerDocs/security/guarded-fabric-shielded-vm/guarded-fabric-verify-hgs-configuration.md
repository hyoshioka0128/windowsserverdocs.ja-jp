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
ms.openlocfilehash: 43b2a90eaa987e96b716e10259f75ffaf9f136a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832573"
---
# <a name="verify-the-hgs-configuration"></a>HGS の構成を確認する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


次に、モ ノが想定どおりに動作するかを検証する必要があります。 これを行うには、管理者特権での Windows PowerShell コンソールで、次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS の構成で保護されたファブリックに追加するホストに関する情報がまだ含まれないため、診断はホストできなくなるなしに、まだ正常に証明を示します。 この結果を無視し、診断によって提供されるその他の情報を確認します。

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

<!-- When a link is available for an updated troubleshooting guide, add a sentence like the following and create a link to the troubleshooting guide:
If failures did occur, please review the remediation steps provided or see the Troubleshooting Guide.
-->

HGS クラスター内の各ノードで、診断を実行します。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[保護されたホストを展開します。](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

