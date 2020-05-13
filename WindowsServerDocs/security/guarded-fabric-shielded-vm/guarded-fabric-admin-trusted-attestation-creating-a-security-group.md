---
title: 保護されたホストのセキュリティグループを作成し、そのグループを HGS に登録します
ms.prod: windows-server
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b6fac7792b91e7415d0714b43201c404da2155bf
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203406"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>保護されたホストのセキュリティグループを作成し、そのグループを HGS に登録します

> 適用先:Windows Server (半期チャネル)、Windows Server 2016

> [!IMPORTANT]
> AD モードは、Windows Server 2019 以降では非推奨とされます。 TPM の構成証明が不可能な環境では、[ホストキー](guarded-fabric-initialize-hgs-key-mode.md)の構成証明を構成します。 ホストキーの構成証明により、AD モードと同様の保証が提供され、セットアップが簡単になります。

このトピックでは、管理者によって信頼された構成証明 (AD モード) を使用して、保護されたホストになるように Hyper-v ホストを準備する中間手順について説明します。 これらの手順を実行する前に、「[保護されたホストとなるホストのファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns-ad.md)」の手順を完了してください。


## <a name="create-a-security-group-and-add-hosts"></a>セキュリティグループの作成とホストの追加

1. ファブリックドメインに新しい**グローバル**セキュリティグループを作成し、シールドされた vm を実行する hyper-v ホストを追加します。 ホストを再起動して、グループメンバーシップを更新します。

2. Get ADGroup を使用して、セキュリティグループのセキュリティ識別子 (SID) を取得し、それを HGS 管理者に提供します。

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Get-AdGroup コマンドの出力](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>セキュリティグループの SID を HGS に登録する

1. HGS サーバーで次のコマンドを実行して、セキュリティグループを HGS に登録します。
   必要に応じて、追加のグループに対してコマンドを再実行します。
   グループのフレンドリ名を指定します。
   Active Directory セキュリティグループ名と一致する必要はありません。

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. グループが追加されたことを確認するには、 [HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)を実行します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた VM のためのホスト ガーディアン サービスの展開](guarded-fabric-deploying-hgs-overview.md)
