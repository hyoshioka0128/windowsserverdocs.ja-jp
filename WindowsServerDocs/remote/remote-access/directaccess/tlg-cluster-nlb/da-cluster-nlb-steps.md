---
title: DirectAccess クラスター/NLB テスト ラボの構成手順
description: このトピックは一部のテスト ラボ ガイド - Windows Server 2016 で Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2ebda017b41f27c2f69c7b850de44e771732415d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283328"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>DirectAccess クラスター/NLB テスト ラボの構成手順

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の手順では、リモート アクセス インフラストラクチャを構成、リモート アクセス サーバーとクライアントを構成、およびインターネットとホームネット サブネットからの DirectAccess 接続をテストする方法について説明します。  
  
このテスト ラボ ガイドのネットワーク負荷分散 (NLB) を作成では、次の手順を実行してリモート アクセス クラスターを有効になって。  
  
-   [手順 1 は、DirectAccess の構成を完了](STEP-1-Complete-the-DirectAccess-Configuration.md)します。 すべての手順を完了、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)します。  
  
-   [手順 2:EDGE1 構成](STEP-2-Configure-EDGE1.md)します。 負荷分散の EDGE1 のリモート アクセスの役割を構成します。  
  
-   [手順 3:インストールし、構成 EDGE2](STEP-3-Install-and-Configure-EDGE2.md)します。 EDGE2 は、リモート アクセス クラスター内の 2 つ目のリモート アクセス サーバーとして機能します。  
  
-   [手順 4:ネットワーク負荷分散のリモート アクセス クラスター作成](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)-EDGE1 リモート アクセス クラスターの最初のサーバーとして構成します。 EDGE2 がクラスターに参加しているし、NLB はクラスターを構成します。  
  
-   [手順 5:クラスターと、インターネットからの DirectAccess 接続をテストする](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md)します。 NLB とクラスターの構成が完了した後は、負荷分散されたクラスターによって、DirectAccess クライアント接続をテストできます。  
  
-   [手順 6:NAT デバイスの背後からの DirectAccess クライアント接続のテスト](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md)します。 ホーム ルーターの背後からの DirectAccess クライアント接続のテストをシミュレートするために、NAT デバイスの背後にあるクライアント コンピューターを移動します。  
  
-   [手順 7:接続をテストする、Corpnet に返すときに](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md)します。 クライアント コンピューターが企業ネットワークに返すときに会社のリソースをアクセスもことを確認します。  
  
-   [手順 8:構成のスナップショット](da-cluster-nlb-s8-snapshot.md)します。 テスト ラボを完了するには、その他のシナリオをテストするには、後で戻すことができるように作業用のリモート アクセスの NLB クラスターのスナップショットを取得します。  
  


