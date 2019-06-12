---
title: 保護されたホストのセキュリティ グループを作成し、HGS をグループに登録
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: fb84720b94746a3c5757037ceb5c9bc8c965ff7f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447167"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>保護されたホストのセキュリティ グループを作成し、HGS をグループに登録

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

>[!IMPORTANT]
>AD モードでは、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 


このトピックでは、管理者によって信頼された構成証明 (AD モード) を使用して保護されたホストに HYPER-V ホストを準備する中間の手順について説明します。 次の手順を実行する前に手順を完了[fabric DNS を構成する保護されたホストとなるホストの](guarded-fabric-configuring-fabric-dns-ad.md)します。


## <a name="create-a-security-group-and-add-hosts"></a>セキュリティ グループを作成し、ホストの追加

1. 新規作成**GLOBAL**セキュリティ fabric ドメインでグループ化し、シールドされた Vm を実行する HYPER-V ホストを追加します。 そのグループ メンバーシップを更新するホストを再起動します。

2. Get ADGroup を使用して、セキュリティ グループのセキュリティ識別子 (SID) を取得し、HGS 管理者に提供します。 

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Get AdGroup コマンドの出力](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>セキュリティ グループの SID を HGS に登録します。  

1. HGS サーバーでは、セキュリティ グループを HGS に登録する次のコマンドを実行します。 
   他のグループに必要な場合、コマンドを再実行します。 
   グループのフレンドリ名を提供します。 
   Active Directory セキュリティ グループの名前と一致する必要はありません。 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. グループが追加されたことを検証するには、 [Get HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)します。 

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のホスト ガーディアン サービスを展開します。](guarded-fabric-deploying-hgs-overview.md)
