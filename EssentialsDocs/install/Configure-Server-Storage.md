---
title: サーバー記憶域の構成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef7ddcdd-3a74-40ca-9487-c3a6fc5155a5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6de485f6fd46464ba707bc0871f60ac2fec5a1db
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433745"
---
# <a name="configure-server-storage"></a>サーバー記憶域の構成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

## <a name="sample-hard-disk-configurations"></a>ハード ディスク構成例  
 次の表では、ハード ディスク構成例を示します。 見積もりは、標準的な使用量と機能をベースにしていますが、最適なパフォーマンスに影響を与える問題については記載していません。 顧客の好みとニーズに合わせて、構成でサポートされているどのような種類のハード ディスク (SATA、SCSI など) でも使用できます。  
  
> [!IMPORTANT]
>   Windows Server Essentials は、c: ボリュームとしてインストールする必要があり、ボリューム サイズは 60 GB 以上である必要があります。 オペレーティング システム ディスクに 2 つのパーティションを作成し、ビジネス データの格納には C: (システム パーティション) を使用しないことをお勧めします。  
  
|サーバーのレベル|ディスク構成|  
|------------------|------------------------|  
|入力|-2 つの物理ディスク<br /><br /> 次を含む RAID 1 ミラーリング セットとして構成します。<br /><br /> C: ボリュームでしょうか。 60 GB<br /><br /> -D: ボリュームでしょうか。 1000 GB|  
|中|-次の 3 つの物理ディスク<br /><br /> 次を含む RAID 5 セットとして構成します。<br /><br /> C: ボリュームでしょうか。 60 GB<br /><br /> -D: ボリュームでしょうか。 1500 GB|  
|高|で合計 5 つ以上の物理ディスク<br /><br /> -RAID 1 2 つのディスクには、c: ボリュームを含むセットがミラー化しますか。 100 GB<br /><br /> の以下を含む RAID 5 セット内の残りのすべてディスク:<br /><br /> -D: ボリュームでしょうか。 1500 GB<br /><br /> -E: ボリュームでしょうか。 1500 GB|  
  
 これらの推奨値は、インストールされたオペレーティング システムのサイズ、サーバーが使用するデータ記憶域の標準的なサイズ、およびサーバーの稼働期間を通して予想されるデータ記憶域の増分を考慮に入れています。 ボリュームは、1 台の物理ディスク上のパーティションでも、または個別の物理ディスク上に作られたものでもかまいません。 サーバーは、お客様の重要なデータを保存するため、複数の物理ディスクを使用してハードウェア RAID または記憶域スペースを使用して、顧客データを保護することをお勧めします。  
  
## <a name="configuring-your-server-backup"></a>サーバー バックアップの構成  
 サーバーの内部ハード ディスクに加えて、顧客は外部 USB ハード ディスクをバックアップに使用することを考慮する必要があります。 顧客は、少なくとも 2 台の十分な容量の外部ハード ディスクで、サーバーのすべてのデータをバックアップすることが理想です。 外部ハード ディスクを使用すると、顧客は毎晩 1 台を離れた場所に置くことで、よりいっそうのデータ保護がはかれます。  
  
## <a name="partition-configuration"></a>パーティション構成  
 サーバーの初期構成中に、共有フォルダーとクライアント コンピューターのバックアップ フォルダーを含む一連の既定のサーバー フォルダーが、ディスク 0 の最大のデータ パーティションに作成されます。  
  
## <a name="see-also"></a>関連項目  

 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK の概要](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

