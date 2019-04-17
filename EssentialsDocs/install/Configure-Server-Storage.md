---
title: "サーバー記憶域を構成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configure-server-storage"></a>サーバー記憶域を構成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

## <a name="sample-hard-disk-configurations"></a>ハード_ディスク構成例  
 次の表は、ハード_ディスク構成例を示しています。 見積もりは、一般的な使用状況と機能に基づいていますが、最適なパフォーマンスに影響する問題を記載していません。 任意の種類のサポートされているハード_ディスク (SATA、SCSI) など、これらの構成の基本設定と、顧客のニーズに基づいてを使用することができます。  
  
> [!IMPORTANT]
>   Windows Server Essentials は、c: ボリュームとしてインストールする必要があり、ボリュームのサイズは 60 GB 以上である必要があります。 オペレーティング システム ディスクに 2 つのパーティションを作成し、ビジネス データを格納する c: (システム パーティション) を使用していないことをお勧めします。  
  
|サーバー レベル|ディスクの構成|  
|------------------|------------------------|  
|エントリ|-2 つの物理ディスク<br /><br /> 以下を含む RAID 1 ミラーリング セットとして構成します。<br /><br /> C: ボリュームですか。 60 GB<br /><br /> -D: ボリュームですか。 1000 GB|  
|[中]|-3 台の物理ディスク<br /><br /> 以下を含む RAID 5 セットとして構成します。<br /><br /> C: ボリュームですか。 60 GB<br /><br /> -D: ボリュームですか。 1500 GB|  
|高|で合計 5 台以上の物理ディスク<br /><br /> の c: ボリュームを含む RAID 1 ミラーリング セット内 2 つのディスクですか。 100 GB<br /><br /> の以下を含む RAID 5 セットの残りすべてのディスク:<br /><br /> -D: ボリュームですか。 1500 GB<br /><br /> -E: ボリュームですか。 1500 GB|  
  
 これらの推奨事項は、インストールされているオペレーティング システムのサイズ、サーバーが使用するデータ記憶域とサーバーの稼働期間を通して予想されるデータの記憶域の増分の平均サイズを考慮します。 ボリュームが 1 つの物理ディスク上のパーティションにすることができますか、別の物理ディスク上に配置することができます。 サーバーは、お客様の重要なデータを保存するため、複数の物理ディスクを使用し、ハードウェア RAID または記憶域スペースを使用して、お客様のデータを保護することをお勧めします。  
  
## <a name="configuring-your-server-backup"></a>サーバー バックアップの構成  
 お客様は、サーバー上の内部のハード_ディスク、だけでなく、外部 USB ハード_ディスクを使用してバックアップ検討してください。 理想的には、お客様は、サーバー上のすべてのデータをバックアップするには、十分な容量の少なくとも 2 つの外部ハード ディスクがあります。 外部ハード _ ディスクを使用している場合、顧客がかかりますオフサイトの 1 つのディスク毎晩をさらに、データを保護します。  
  
## <a name="partition-configuration"></a>パーティションの構成  
 サーバーの初期構成中に、一連の共有フォルダーとクライアント コンピューターのバックアップ フォルダーを含む既定のサーバー フォルダーは、ディスク 0 の最大のデータ パーティションに作成されます。  
  
## <a name="see-also"></a>参照してください。  

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

