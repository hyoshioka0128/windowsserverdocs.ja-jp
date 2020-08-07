---
title: 管理者によって信頼された構成証明のホスト情報を追加する
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: abc01dbb691843d199169bd654afaa5cf06bbb87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971439"
---
# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>管理者によって信頼された構成証明を使用して Hyper-v ホストを承認する

> 適用先:Windows Server (半期チャネル)、Windows Server 2016

> [!IMPORTANT]
> 管理者によって信頼された構成証明 (AD モード) は、Windows Server 2019 以降では非推奨とされます。 TPM の構成証明が不可能な環境では、[ホストキー](guarded-fabric-initialize-hgs-key-mode.md)の構成証明を構成します。 ホストキーの構成証明により、AD モードと同様の保証が提供され、セットアップが簡単になります。


AD モードで保護されたホストを承認するには、次のようにします。

1. ファブリックドメインで、Hyper-v ホストをセキュリティグループに追加します。
2. HGS ドメインで、セキュリティグループの SID を HGS に登録します。

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Hyper-v ホストをセキュリティグループに追加し、ホストを再起動します。

1. ファブリックドメインに**グローバル**セキュリティグループを作成し、シールドされた vm を実行する hyper-v ホストを追加します。
   ホストを再起動して、グループメンバーシップを更新します。

2. Get ADGroup を使用して、セキュリティグループのセキュリティ識別子 (SID) を取得し、それを HGS 管理者に提供します。

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Get-AdGroup コマンドの出力](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>セキュリティグループの SID を HGS に登録する

1. ファブリック管理者から保護されたホストのセキュリティグループの SID を取得し、次のコマンドを実行してセキュリティグループを HGS に登録します。
   必要に応じて、追加のグループに対してコマンドを再実行します。
   グループのフレンドリ名を指定します。
   Active Directory セキュリティグループ名と一致する必要はありません。

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. グループが追加されたことを確認するには、 [HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)を実行します。


