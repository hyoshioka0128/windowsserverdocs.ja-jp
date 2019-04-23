---
title: 新しいフォレストでの HGS をインストールします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7f04d9964f1a19e79335e50a1882f0326f15ddc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860033"
---
# <a name="install-hgs-in-a-new-forest"></a>新しいフォレストでの HGS をインストールします。 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

## <a name="add-the-hgs-server-role"></a>HGS サーバーの役割を追加します。

HGS サーバーの役割を追加し、HGS をインストールする管理者特権の PowerShell セッションで、次のコマンドを実行します。

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>HGS のインストール 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>次のステップ

- TPM ベースの構成証明を設定する次の手順を参照してください。[初期化 TPM モードを使用して、新しい専用フォレスト (既定値) の HGS クラスター](guarded-fabric-initialize-hgs-tpm-mode-default.md)します。
- ホスト キーの構成証明を設定する次の手順を参照してください。[初期化キーのモードを使用して、新しい専用フォレスト (既定値) の HGS クラスター](guarded-fabric-initialize-hgs-key-mode-default.md)します。
- (Windows Server 2019 で非推奨) 管理ベースの認証、設定する手順を参照してください、次の[初期化 (既定値) の新しい専用フォレストに AD モードを使用して、HGS クラスター](guarded-fabric-initialize-hgs-ad-mode-default.md)します。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[HGS を初期化します。](guarded-fabric-initialize-hgs.md)


