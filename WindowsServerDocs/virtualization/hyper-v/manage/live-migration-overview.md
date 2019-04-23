---
title: ライブ マイグレーションの概要
description: Windows Server 2016 でのライブ マイグレーション機能の概要を示します。
ms.prod: windows-server-threshold
ms.service: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: 2bbe897ffb8b200a72fac5a662e518d4a4be1131
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887853"
---
# <a name="live-migration-overview"></a>ライブ マイグレーションの概要

ライブ マイグレーションは、Windows server、HYPER-V 機能です。  計画外のダウンタイムをしなくても別に 1 つの HYPER-V ホストから仮想マシンの実行を透過的に移動することができます。  ライブ マイグレーションの主な利点は柔軟性です。実行中の仮想マシンは 1 つのホスト マシンに関連付けられていません。  これにより、使用停止またはにアップグレードする前に仮想マシンの特定のホストのドレインなどのアクションができます。  Windows フェールオーバー クラスタ リングと組み合わせると、ライブ マイグレーションは、高可用性のフォールト トレラント システム。 

## <a name="related-technologies-and-documentation"></a>関連するテクノロジとドキュメント

ライブ移行はフェールオーバー クラスタ リングと System Center Virtual Machine Manager などのいくつかの関連テクノロジと共によく使用されます。  これらのテクノロジを使用してライブ マイグレーションを使用する場合、最新のドキュメントへのポインターを示します。
* [フェールオーバー クラスタ リング](../../../failover-clustering/failover-clustering-overview.md)(Windows Server 2016) 
* [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

Windows Server の以前のバージョンを使用しているか、または Windows Server の以前のバージョンで導入された機能についての詳細が必要な場合、履歴のドキュメントへのポインターを示します。 
* [ライブ マイグレーション](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx)(Windows Server 2008 R2)  
* [ライブ マイグレーション](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx)(Windows Server 2012 R2) 
* [フェールオーバー クラスタ リング](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx)(Windows Server 2012 R2)
* [フェールオーバー クラスタ リング](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx)(Windows Server 2008 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Windows Server 2016 でのライブ マイグレーション

Windows Server 2016 でのライブ マイグレーションの展開の数の制限があります。  これでフェールオーバー クラスタ リングのない動作します。  その他の機能は、ライブ マイグレーションの以前のリリースから変更されません。  構成とフェールオーバー クラスタ リングのないライブ マイグレーションの使用について詳しくは。 
* [フェールオーバー クラスタ リングのないライブ マイグレーションのホストの設定します。](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [フェールオーバー クラスタ リングのないライブ マイグレーションを使用して、仮想マシンを移動するには](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)