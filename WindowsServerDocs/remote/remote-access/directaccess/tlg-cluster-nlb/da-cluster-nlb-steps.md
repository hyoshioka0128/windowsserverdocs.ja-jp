---
title: DirectAccess クラスター/NLB テスト ラボの構成手順
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 108c63298ad3382f5ece790258f2d278bb03b78b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388404"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>DirectAccess クラスター/NLB テスト ラボの構成手順

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順では、リモートアクセスインフラストラクチャを構成し、リモートアクセスサーバーとクライアントを構成し、インターネットおよび Homenet サブネットから DirectAccess 接続をテストする方法について説明します。  
  
このテストラボガイドでは、次の手順を実行して、ネットワーク負荷分散 (NLB) が有効になっているリモートアクセスクラスターを構築します。  
  
-   [手順 1 DirectAccess の構成を完了](STEP-1-Complete-the-DirectAccess-Configuration.md)します。 @No__t-0Test Lab Guide のすべての手順を完了します。IPv4 と IPv6 が混在する DirectAccess のシングルサーバーセットアップのデモンストレーション @ no__t-0  
  
-   [手順 2:EDGE1 @ no__t-0 を構成します。 負荷分散のために EDGE1 でリモートアクセスの役割を構成します。  
  
-   [手順 3:EDGE2 @ no__t-0 をインストールして構成します。 EDGE2 は、リモートアクセスクラスターの2番目のリモートアクセスサーバーとして機能します。  
  
-   [手順 4:ネットワーク負荷分散リモートアクセスクラスターを作成する @ no__t-EDGE1 は、リモートアクセスクラスターの最初のサーバーとして構成されます。 EDGE2 がクラスターに参加し、NLB がクラスター用に構成されています。  
  
-   [手順 5:インターネットおよびクラスター @ no__t からの DirectAccess 接続をテストします。 NLB とクラスターの構成が完了したら、負荷分散されたクラスターを使用して DirectAccess クライアントの接続をテストできます。  
  
-   [手順 6:NAT デバイスの背後からの DirectAccess クライアント接続をテストする @ no__t ~ 0 NAT デバイスの背後にあるクライアントコンピューターを移動して、ホームルーターの背後からの DirectAccess クライアント接続のテストをシミュレートします。  
  
-   [手順 7:ネットワーク接続 @ no__t-0 に戻るときに接続をテストします。 企業ネットワークに戻るときに、クライアントコンピューターが会社のリソースに引き続きアクセスできることを確認します。  
  
-   [手順 8:構成 @ no__t-0 のスナップショットを設定します。 テストラボを完了したら、作業中のリモートアクセス NLB クラスターのスナップショットを作成して、後で追加のシナリオをテストすることができるようにします。  
  


