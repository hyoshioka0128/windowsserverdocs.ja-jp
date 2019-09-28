---
title: テスト ラボの構成手順
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dd8b8864dff98e51bf55aad9307523df4a0c30bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404696"
---
# <a name="steps-for-configuring-the-test-lab"></a>テスト ラボの構成手順

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順では、リモートアクセスインフラストラクチャを構成し、リモートアクセスサーバーとクライアントを構成して、インターネットおよび Homenet サブネットから DirectAccess 接続をテストする方法について説明します。  
  
このテストラボガイドでは、次の手順を実行して、マルチサイトリモートアクセスの展開を作成します。  
  
-   [手順 1:基本構成 @ no__t-0 を完了します。 @No__t-0Test Lab Guide のすべての手順を完了します。IPv4 と IPv6 が混在する DirectAccess のシングルサーバーセットアップのデモンストレーション @ no__t-0  
  
-   [手順 2:ROUTER1 @ no__t をインストールして構成します。 ROUTER1 は、企業ネットワークと2ネットワークのサブネット間のルーティングおよび転送機能を提供します。  
  
-   [手順 3:No__t をインストールして構成します。 Windows 7 クライアントコンピューターは、windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 リモートアクセス展開の下位互換性を示すために使用されます。  
  
-   [手順 4:No__t を構成します。 既定のゲートウェイとして ROUTER1 を使用し、代替 DNS サーバーとして 2-DC1 を構成します。  
  
-   [手順 5:DC1 @ no__t を構成します。 追加の Active Directory サイトと、Windows 7 クライアントコンピューター用の追加のセキュリティグループを使用して DC1 を構成します。  
  
-   [手順 6:2-DC1 @ no__t をインストールして構成します。 マルチサイト展開では、2つ以上のドメインとサイトがあります。 2-DC1 は、corp2.corp.contoso.com ドメインのドメインコントローラーと DNS サービスを提供します。  
  
-   [手順 7:2つの no__t をインストールして構成します。 2-"2" は、2つの企業ネットワークネットワーク内の web およびファイルサーバーです。  
  
-   [手順 8:INET1 @ no__t-0 を構成します。 INET1 は、このテストラボガイドでインターネットをシミュレートします。 EDGE1 のパブリック IP アドレスに解決される DNS エントリを構成する必要があります。  
  
-   [手順 9:EDGE1 @ no__t-0 を構成します。 EDGE1 で、2ネットワークの DNS サーバーとルーティングを構成します。  
  
-   [手順 10:2-EDGE1 @ no__t をインストールして構成します。 マルチサイト展開では、2台のリモートアクセスサーバーが必要です。 2-EDGE1 は、2番目のドメインのリモートアクセスサービスを提供します。  
  
-   [手順 11:マルチサイト展開 @ no__t を構成します。 両方のリモートアクセスサーバーを構成した後で、マルチサイト展開を構成することができます。  
  
-   [手順 12:DirectAccess 接続をテストします @ no__t-0。 EDGE1 と EDGE1 を使用して、インターネットサブネットから両方のクライアントコンピューターからの DirectAccess 接続をテストします。  
  
-   [手順 13:NAT デバイスの背後からの DirectAccess 接続をテストする @ no__t ~ 0 NAT デバイスの背後からの DirectAccess 接続をテストします。  
  
-   [手順 14:構成 @ no__t-0 のスナップショットを設定します。 テストラボを完了したら、作業中のリモートアクセスマルチサイト展開のスナップショットを作成して、後で追加のシナリオをテストすることができるようにします。  
  


