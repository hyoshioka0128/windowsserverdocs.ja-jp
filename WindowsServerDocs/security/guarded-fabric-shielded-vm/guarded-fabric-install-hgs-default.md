---
title: 新しいフォレストに HGS をインストールする
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 6dfbe24fb4d9011b48f366d7e5df92fdb80685d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386593"
---
# <a name="install-hgs-in-a-new-forest"></a>新しいフォレストに HGS をインストールする 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

## <a name="add-the-hgs-server-role"></a>HGS サーバーロールを追加する

管理者特権の PowerShell セッションで次のコマンドを実行して、HGS サーバーの役割を追加し、HGS をインストールします。

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>HGS のインストール 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>次の手順

- TPM ベースの構成証明を設定する次の手順については、「[新しい専用フォレストで tpm モードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-tpm-mode-default.md)」を参照してください。
- ホストキーの構成証明を設定する次の手順については、「[新しい専用フォレストでキーモードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-key-mode-default.md)」を参照してください。
- 管理者ベースの構成2019証明をセットアップする次の手順については、「[新しい専用フォレストで AD モードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-ad-mode-default.md)」を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS の初期化](guarded-fabric-initialize-hgs.md)


