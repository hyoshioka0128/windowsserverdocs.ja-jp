---
title: ライブ マイグレーションの概要
description: Windows Server 2016 のライブマイグレーション機能の概要を示します。
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: 11fd67f5b4b3c9ce6a8aebe7dac4008f38d0f08e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815175"
---
# <a name="live-migration-overview"></a>ライブ マイグレーションの概要

ライブマイグレーションは、Windows Server の Hyper-v 機能です。  これにより、ダウンタイムを認識することなく、Hyper-v ホスト間で実行中の Virtual Machines を透過的に移動できます。  ライブマイグレーションの主な利点は柔軟性です。Virtual Machines の実行は、1つのホストコンピューターに関連付けられていません。  これにより、特定のホスト Virtual Machines のドレインなどの操作を、使用停止またはアップグレードする前に行うことができます。  Windows フェールオーバークラスタリングと組み合わせて使用すると、ライブマイグレーションにより、高可用性とフォールトトレラントなシステムを作成できます。 

## <a name="related-technologies-and-documentation"></a>関連テクノロジとドキュメント

ライブマイグレーションは、フェールオーバークラスタリングや System Center Virtual Machine Manager など、いくつかの関連テクノロジと組み合わせて使用されることがよくあります。  これらのテクノロジを使用してライブマイグレーションを使用している場合は、最新のドキュメントを参照してください。
* [フェールオーバークラスタリング](../../../failover-clustering/failover-clustering-overview.md)(Windows Server 2016) 
* [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

以前のバージョンの Windows Server を使用している場合、または以前のバージョンの Windows Server で導入された機能の詳細が必要な場合は、次のドキュメントを参照してください。 
* [ライブマイグレーション](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx)(Windows Server 2008 R2)  
* [ライブマイグレーション](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx)(Windows Server 2012 R2) 
* [フェールオーバークラスタリング](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx)(Windows Server 2012 R2)
* [フェールオーバークラスタリング](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx)(Windows Server 2008 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Windows Server 2016 のライブマイグレーション

Windows Server 2016 では、ライブマイグレーションの展開に制限がありません。  フェールオーバークラスタリングなしで動作するようになりました。  その他の機能は、以前のリリースのライブマイグレーションから変更されていません。  フェールオーバークラスタリングを使用しないライブマイグレーションの構成と使用の詳細については、次のとおりです。 
* [フェールオーバークラスタリングを使用しないライブマイグレーションのホストの設定](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [フェールオーバークラスタリングを使用せずにライブマイグレーションを使用して仮想マシンを移動する](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)