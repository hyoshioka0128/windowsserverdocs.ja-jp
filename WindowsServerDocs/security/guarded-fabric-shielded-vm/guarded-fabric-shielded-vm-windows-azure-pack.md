---
title: テナント用のシールドされた Vm-Windows Azure Pack を使用したシールドされた VM のデプロイ
ms.prod: windows-server
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ce3aac47ea6c44abd1811efc1e23b901f53333bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856465"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>テナント用のシールドされた Vm-Windows Azure Pack を使用したシールドされた VM のデプロイ

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

ホスティングサービスプロバイダーがサポートしている場合は、Windows Azure Pack を使用して、シールドされた VM をデプロイできます。

次の手順を実行します。

1. Windows Azure Pack で提供される1つ以上のプランをサブスクライブします。

2. Windows Azure Pack を使用して、シールドされた VM を作成します。

    シールドされた[仮想マシンを使用](https://technet.microsoft.com/library/mt720674.aspx)します。これについては、次のトピックで説明します。

   - [シールドデータを作成](https://technet.microsoft.com/library/mt720672.aspx)します (「」トピックの2番目の手順で説明されているように、シールドデータファイルをアップロードします)。
    
     > [!NOTE]
     > シールドデータの作成の一環として、ガーディアンキーファイルがダウンロードされます。これは、UTF-8 形式の XML ファイルです。 ファイルを UTF-16 に変更しないでください。
    
   - シールドされたテンプレートを使用し**て、また**は通常のテンプレートを使用して、シールドされた[仮想マシンを作成](https://technet.microsoft.com/library/mt720673.aspx)します。
    
       > [!WARNING]
       > 通常の[テンプレートを使用してシールドされた仮想マシンを作成](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2)する場合は、VM が "*シールド*なし" としてプロビジョニングされていることに注意する必要があります。 これは、シールドデータファイル内の信頼されたディスクの一覧に対してテンプレートディスクが検証されないこと、また、VM のプロビジョニングに使用されるシールドデータファイル内のシークレットではないことを意味します。 シールドされたテンプレートを使用できる場合は、シールドされたテンプレートを使用してシールドされた VM をデプロイし、シークレットのエンドツーエンドの保護を提供することをお勧めします。
    
   - [第2世代バーチャルマシンをシールドされたバーチャルマシンに変換する](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > バーチャルマシンをシールドされたバーチャルマシンに変換する場合、既存のチェックポイントとバックアップは暗号化されません。 以前の暗号化解除されたデータにアクセスできないようにするには、可能であれば、古いチェックポイントを削除する必要があります。

## <a name="see-also"></a>参照

- [保護されたホストとシールドされた Vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
