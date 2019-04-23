---
title: シールドされた VMの展開
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: fa6da3f4a98686f83fff3937c2dc44fd4d623fe3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871013"
---
# <a name="deploy-shielded-vms"></a>シールドされた VMの展開


>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

次のトピックでは、テナントをシールドされた Vm と連携する方法について説明します。

1. (省略可能)[Windows テンプレート ディスクを作成する](guarded-fabric-create-a-shielded-vm-template.md)または[Linux テンプレート ディスクを作成する](guarded-fabric-create-a-linux-shielded-vm-template.md)します。 テンプレート ディスクは、テナントまたはホスティング サービス プロバイダーのいずれかで作成できます。 

2. (省略可能)[既存の Windows VM をシールドされた VM に変換](guarded-fabric-vm-shielding-helper-vhd.md)します。 

3. [定義のシールドされた VM をシールド データを作成する](guarded-fabric-tenant-creates-shielding-data.md)します。

    説明と図は、シールド データ ファイルのでは、次を参照してください[シールド データを使用するものが、なぜ必要ですか?。](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)
    
    シールド データ ファイルに含める応答ファイルを作成する方法の詳細については、次を参照してください。[シールドされた Vm - New-shieldingdataanswerfile 関数を使用して応答ファイルを生成する](guarded-fabric-sample-unattend-xml-file.md)します。

4. シールドされた VM を作成します。
 
    - 使用して**Windows Azure Pack**:[Windows Azure Pack を使用して、シールドされた VM をデプロイします。](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - 使用して**Virtual Machine Manager**:[Virtual Machine Manager を使用して、シールドされた VM をデプロイします。](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[シールドされた VM テンプレートを作成します。](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>関連項目

- [保護されたファブリックとシールドされた Vm](guarded-fabric-and-shielded-vms-top-node.md)
