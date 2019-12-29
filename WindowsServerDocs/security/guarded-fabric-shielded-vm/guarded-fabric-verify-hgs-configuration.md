---
title: HGS の構成を確認する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: d219b7aa9ca1e17df3281fd756106a6f07864116
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386350"
---
# <a name="verify-the-hgs-configuration"></a>HGS の構成を確認する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


次に、予期したとおりに動作していることを検証する必要があります。 これを行うには、管理者特権の Windows PowerShell コンソールで次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS 構成には、保護されたファブリック内のホストに関する情報がまだ含まれていないため、正常に証明できないホストがないことが診断によって示されます。 この結果を無視し、診断によって提供されるその他の情報を確認します。

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

HGS クラスター内の各ノードで診断を実行します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [保護されたホストの展開](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

