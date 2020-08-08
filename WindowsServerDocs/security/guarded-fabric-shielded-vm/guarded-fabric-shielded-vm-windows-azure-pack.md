---
title: テナント用のシールドされた Vm-Windows Azure Pack を使用したシールドされた VM のデプロイ
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 613082bcc5cfefa0c7abb0011762c3d283ea98aa
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989995"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>テナント用のシールドされた Vm-Windows Azure Pack を使用したシールドされた VM のデプロイ

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

ホスティングサービスプロバイダーがサポートしている場合は、Windows Azure Pack を使用して、シールドされた VM をデプロイできます。

次の手順を実行します。

1. Windows Azure Pack で提供される1つ以上のプランをサブスクライブします。

2. Windows Azure Pack を使用して、シールドされた VM を作成します。

    シールドされた[仮想マシンを使用](/previous-versions/azure/windows-server-azure-pack/mt720674(v=technet.10))します。これについては、次のトピックで説明します。

   - [シールドデータを作成](/previous-versions/azure/windows-server-azure-pack/mt720672(v=technet.10))します (「」トピックの2番目の手順で説明されているように、シールドデータファイルをアップロードします)。

     > [!NOTE]
     > シールドデータの作成の一環として、ガーディアンキーファイルがダウンロードされます。これは、UTF-8 形式の XML ファイルです。 ファイルを UTF-16 に変更しないでください。

   - シールドされたテンプレートを使用し**て、また**は通常のテンプレートを使用して、シールドされた[仮想マシンを作成](/previous-versions/azure/windows-server-azure-pack/mt720673(v=technet.10))します。

       > [!WARNING]
       > 通常の[テンプレートを使用してシールドされた仮想マシンを作成](/previous-versions/azure/windows-server-azure-pack/mt720673(v=technet.10)#Anchor_2)する場合は、VM が "*シールド*なし" としてプロビジョニングされていることに注意する必要があります。 これは、シールドデータファイル内の信頼されたディスクの一覧に対してテンプレートディスクが検証されないこと、また、VM のプロビジョニングに使用されるシールドデータファイル内のシークレットではないことを意味します。 シールドされたテンプレートを使用できる場合は、シールドされたテンプレートを使用してシールドされた VM をデプロイし、シークレットのエンドツーエンドの保護を提供することをお勧めします。

   - [第2世代バーチャルマシンをシールドされたバーチャルマシンに変換する](/previous-versions/azure/windows-server-azure-pack/mt720670(v=technet.10))

       > [!NOTE]
       > バーチャルマシンをシールドされたバーチャルマシンに変換する場合、既存のチェックポイントとバックアップは暗号化されません。 以前の暗号化解除されたデータにアクセスできないようにするには、可能であれば、古いチェックポイントを削除する必要があります。

## <a name="additional-references"></a>その他の参照情報

- [保護されたホストとシールドされた VM のためのホスティング サービス プロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)