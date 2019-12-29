---
title: シールドされた VMの展開
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f7892dabb028b99cb4cb1c9045764a8e36aba7dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386766"
---
# <a name="deploy-shielded-vms"></a>シールドされた VMの展開


>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

次のトピックでは、テナントがシールドされた Vm を操作する方法について説明します。

1. Optional[Windows テンプレートディスクを作成](guarded-fabric-create-a-shielded-vm-template.md)するか[、Linux テンプレートディスクを作成](guarded-fabric-create-a-linux-shielded-vm-template.md)します。 テンプレートディスクは、テナントまたはホスティングサービスプロバイダーによって作成できます。 

2. Optional[既存の WINDOWS VM をシールドされた vm に変換](guarded-fabric-vm-shielding-helper-vhd.md)します。 

3. シールドされ[た VM を定義するシールドデータを作成](guarded-fabric-tenant-creates-shielding-data.md)します。

    シールドデータファイルの説明と図については、「[シールドデータとは何ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary) 」を参照してください。
    
    シールドされたデータファイルに含める応答ファイルの作成の詳細については、「シールドされ[た vm-ShieldingDataAnswerFile 関数を使用して応答ファイルを生成](guarded-fabric-sample-unattend-xml-file.md)する」を参照してください。

4. シールドされた VM を作成します。
 
    - **Windows Azure Pack**の使用:[Windows Azure Pack を使用してシールドされた VM をデプロイする](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - **Virtual Machine Manager**の使用:[Virtual Machine Manager を使用してシールドされた VM をデプロイする](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [シールドされた VM テンプレートを作成する](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>関連項目

- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
