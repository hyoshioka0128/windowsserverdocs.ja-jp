---
title: 新しいフォレストに HGS をインストールする
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8f896b0cea49f9dd26a828a2580b59a78348763a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856605"
---
# <a name="install-hgs-in-a-new-forest"></a>新しいフォレストに HGS をインストールする 

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

## <a name="add-the-hgs-server-role"></a>HGS サーバーロールを追加する

管理者特権の PowerShell セッションで次のコマンドを実行して、HGS サーバーの役割を追加し、HGS をインストールします。

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>HGS のインストール 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>次のステップ:

- TPM ベースの構成証明を設定する次の手順については、「[新しい専用フォレストで tpm モードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-tpm-mode-default.md)」を参照してください。
- ホストキーの構成証明を設定する次の手順については、「[新しい専用フォレストでキーモードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-key-mode-default.md)」を参照してください。
- 管理者ベースの構成2019証明をセットアップする次の手順については、「[新しい専用フォレストで AD モードを使用して HGS クラスターを初期化する (既定)](guarded-fabric-initialize-hgs-ad-mode-default.md)」を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS の初期化](guarded-fabric-initialize-hgs.md)


