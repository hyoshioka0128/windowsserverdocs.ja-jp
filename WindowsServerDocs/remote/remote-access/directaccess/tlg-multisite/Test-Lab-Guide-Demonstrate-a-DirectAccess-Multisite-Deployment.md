---
title: テストラボガイド-DirectAccess マルチサイト展開のデモンストレーション
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1980923d0ed29caa60efa012342ef52c93970dfe
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314501"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>テスト ラボ ガイド: DirectAccess マルチサイト展開のデモンストレーション

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

リモートアクセスは、リモートユーザーが DirectAccess または RRAS VPN を使用して内部ネットワークリソースに安全にアクセスできるようにする、windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 オペレーティングシステムのサーバーの役割です。 このガイドでは、マルチサイトシナリオでのリモートアクセスをデモンストレーションするための、 [「IPv4 と IPv6 が混在する DirectAccess シングルサーバーセットアップのテストラボガイド](https://go.microsoft.com/fwlink/p/?LinkId=237004)」を拡張する手順について説明します。  
  
マルチサイトシナリオでリモートアクセスを展開すると、地理的に多様な場所にリモートアクセスサーバーを構成できます。 以前は、リモートユーザーは、常に特定の DirectAccess サーバーを介して企業ネットワークに接続する必要がありました。 Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 と Windows 10 または windows 8 を使用して、展開内の各地理的な場所のエントリポイントを構成できます。 各エントリポイントは、単一のリモートアクセスサーバーまたはリモートアクセスサーバーのクラスターにすることができます。 リモートユーザーは、任意の組織のリモートアクセスエントリポイントに接続することができます。 たとえば、リモートユーザーが、通常、アジアにあるリモートアクセスエントリポイントに接続し、次にヨーロッパへの出張を行う場合、クライアントコンピューターは最も近いリモートアクセスエントリポイントに自動的に接続します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドでは、9台のサーバーと3台のクライアントコンピューターを使用してリモートアクセスを構成およびデモンストレーションする手順について説明します。 「完了したリモートアクセスマルチサイトのテストラボ」では、イントラネット、インターネット、ホームネットワークをシミュレートし、さまざまなインターネット接続シナリオでリモートアクセス機能を示します。  
  
> [!IMPORTANT]  
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。  
  


