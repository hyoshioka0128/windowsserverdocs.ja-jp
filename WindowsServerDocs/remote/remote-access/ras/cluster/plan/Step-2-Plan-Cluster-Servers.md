---
title: 手順 2. 計画クラスター サーバー
description: このトピックでは、Windows Server 2016 でのクラスターでのリモート アクセスの展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0dcb14a03f02f931d59743f1b1b8b24b84ba8351
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282865"
---
# <a name="step-2-plan-cluster-servers"></a>手順 2. 計画クラスター サーバー

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

単一のリモート アクセス サーバーをデプロイした後は、クラスターにサーバーを追加する予定です。  
  
|タスク|説明|  
|----|--------|  
|[2.1 インストール役割と機能の](#BKMK_Install)します。|サーバー クラスターに追加されるごとに、(必要な) 場合は、リモート アクセスの役割と Windows NLB の機能のインストールの計画、計画のトポロジ、IP アドレス指定、ルーティングおよび転送します。|  
|[2.2 サーバー設定を構成します。](#BKMK_Config)|クラスターに追加される各サーバーの設定を構成します。 仮想マシンを使用してサーバーの負荷分散されたクラスターを構成できることに注意してください。 正常に動作するのにルーティングおよび接続の順序では、MAC アドレスのスプーフィングを使用する仮想マシンを構成する必要があります。|  
  
## <a name="BKMK_Install"></a>2.1 役割と機能のインストール  
クラスターに参加する各サーバーに対しては、リモート アクセスの役割をインストールする予定です。 さらに、Windows NLB を使用して、クラスターへのトラフィック分散をロードする場合は、ネットワーク負荷分散 (NLB) 機能をインストールする予定です。 詳細については、次を参照してください。[ネットワーク負荷分散](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing)します。  
  
## <a name="BKMK_Config"></a>2.2 サーバー設定を構成します。  
クラスターに追加される各サーバーの IP アドレスとドメインの設定を計画します。 次のことを考慮してください。  
  
1.  クラスター内のサーバーは、すべて同じドメインに属する必要があります。  
  
2.  クラスター内のサーバーは、同じサブネット上になければなりません。  
  
3.  クラスター内の各サーバーは、同じネットワーク アダプター数を DirectAccess の展開用に使用が必要です。  
  
負荷分散クラスターの Windows NLB を使用すると、次の Windows NLB 設定が適用されます。  
  
1.  ユニキャストの操作モード。 これは、NLB マネージャーを使用してマルチキャストに変更できます。 この設定は、リモート アクセス管理コンソールで変更できません。  
  
2.  すべてのクラスター サーバーが負荷が均等にある要素定義と等しいと、重みを読み込みます。  
  
3.  モード トラフィックをフィルター処理は、負荷分散複数のホスト。  
  
4.  1 つのアフィニティの関係が定義されます。  
  
5.  プロトコルの両方  

