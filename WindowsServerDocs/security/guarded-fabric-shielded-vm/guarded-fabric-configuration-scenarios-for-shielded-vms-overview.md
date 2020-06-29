---
title: シールドされた VMの展開
ms.prod: windows-server
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 78d8d76c2d8fc92e7fc5ca070d04942facd97427
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475359"
---
# <a name="deploy-shielded-vms"></a>シールドされた VMの展開


>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

次のトピックでは、テナントがシールドされた Vm を操作する方法について説明します。

1. Optional[Windows テンプレートディスクを作成](guarded-fabric-create-a-shielded-vm-template.md)するか[、Linux テンプレートディスクを作成](guarded-fabric-create-a-linux-shielded-vm-template.md)します。 テンプレートディスクは、テナントまたはホスティングサービスプロバイダーによって作成できます。

2. Optional[既存の WINDOWS VM をシールドされた vm に変換](guarded-fabric-vm-shielding-helper-vhd.md)します。

3. シールドされ[た VM を定義するシールドデータを作成](guarded-fabric-tenant-creates-shielding-data.md)します。

    シールドデータファイルの説明と図については、「[シールドデータとは何ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary) 」を参照してください。

    シールドされたデータファイルに含める応答ファイルの作成の詳細については、「シールドされ[た vm-ShieldingDataAnswerFile 関数を使用して応答ファイルを生成](guarded-fabric-sample-unattend-xml-file.md)する」を参照してください。

4. シールドされた VM を作成します。

    - **Windows Azure Pack**の使用: [Windows Azure Pack を使用してシールドされた VM をデプロイ](guarded-fabric-shielded-vm-windows-azure-pack.md)する

    - **Virtual Machine Manager**の使用: [Virtual Machine Manager を使用してシールドされた VM をデプロイ](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)する

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [シールドされた VM テンプレートを作成する](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="additional-references"></a>その他のリファレンス

- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
