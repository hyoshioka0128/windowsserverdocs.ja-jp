---
title: テナント - Windows Azure Pack を使用して、シールドされた VM を展開するためのシールドされた Vm
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 600ccd74c379daa281f438b1200179dcae210817
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447353"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>テナント - Windows Azure Pack を使用して、シールドされた VM を展開するためのシールドされた Vm

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

ホスティング サービス プロバイダーがサポートする場合は、シールドされた VM をデプロイする Windows Azure Pack を使用できます。

次の手順を完了するには。

<!-- When we have a link to the topic about how tenants subscribe, add that link as an indented item just under step 1 below. -->

1. Windows Azure Pack で提供される 1 つまたは複数のプランをサブスクライブします。

2. シールドされた VM を作成するには、Windows Azure Pack を使用します。

    [シールドされた仮想マシンを使用して](https://technet.microsoft.com/library/mt720674.aspx)、次のトピックに記載されています。

   - [シールド データの作成](https://technet.microsoft.com/library/mt720672.aspx)(とトピックの 2 番目の手順」の説明に従って、シールド データ ファイルをアップロード) します。
    
     > [!NOTE]
     > シールド データの作成の一環として、utf-8 形式で XML ファイルになりますガーディアン キー ファイルがダウンロードされます。 Utf-16 にファイルを変更しません。
    
   - [シールドされた仮想マシンを作成する](https://technet.microsoft.com/library/mt720673.aspx)-**簡易作成**、シールドされたテンプレートまたは通常のテンプレートを使用します。
    
       > [!WARNING]
       > 場合する[、標準のテンプレートを使用して、シールドされた仮想マシンを作成](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2)は、VM がプロビジョニングされたことに注意してください。*シールド*します。 これは、テンプレート ディスクは、シールド データ ファイル内の信頼されたディスクの一覧に照らし合わせて検証されないことは、VM のプロビジョニングに使用される、シールド データ ファイル内のシークレットを意味します。 シールドされたテンプレートを使用できる場合は、シールドされたテンプレートを使用して、シークレットのエンド ツー エンドの保護を提供するシールドされた VM をデプロイすることをお勧めします。
    
   - [第 2 世代仮想マシンをシールドされた仮想マシンに変換します。](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > 仮想マシンをシールドされた仮想マシンに変換する場合、既存のチェックポイントとバックアップは暗号化されません。 可能であれば、古い、復号化されたデータにアクセスできないように、古いチェックポイントを削除する必要があります。

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしています。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
