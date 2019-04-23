---
title: 管理者によって信頼された構成証明書のホスト情報を追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7949711dbb0f89f5404b491d60938985bfa98c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849463"
---
>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>管理者によって信頼された構成証明を使用して、HYPER-V ホストを承認します。

>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) では、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 


モードの AD で保護されたホストを承認するには。 

1. ファブリックのドメインでは、セキュリティ グループに HYPER-V ホストを追加します。
2. HGS のドメインでは、HGS をセキュリティ グループの SID を登録します。 

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>セキュリティ グループに HYPER-V ホストを追加し、ホストの再起動

1. 作成、 **GLOBAL**セキュリティ fabric ドメインでグループ化し、シールドされた Vm を実行する HYPER-V ホストを追加します。 
   そのグループ メンバーシップを更新するホストを再起動します。

2. Get ADGroup を使用して、セキュリティ グループのセキュリティ識別子 (SID) を取得し、HGS 管理者に提供します。 

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Get AdGroup コマンドの出力](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>セキュリティ グループの SID を HGS に登録します。  

1. ファブリック管理者から保護されたホストのセキュリティ グループの SID を取得し、セキュリティ グループを HGS に登録するには、次のコマンドを実行します。 
   他のグループに必要な場合、コマンドを再実行します。 
   グループのフレンドリ名を提供します。 
   Active Directory セキュリティ グループの名前と一致する必要はありません。 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. グループが追加されたことを検証するには、 [Get HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)します。 


