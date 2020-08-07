---
title: テスト ラボの構成手順
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7fc886d8b4f68c86885cbe5c032247722d88e269
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955208"
---
# <a name="steps-for-configuring-the-test-lab"></a>テスト ラボの構成手順

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順では、リモートアクセスインフラストラクチャを構成し、リモートアクセスサーバーとクライアントを構成して、インターネットおよび Homenet サブネットから DirectAccess 接続をテストする方法について説明します。

このテストラボガイドでは、次の手順を実行して、マルチサイトリモートアクセスの展開を作成します。

-   [手順 1: 基本構成を完了](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed)します。 [「テストラボガイド: 混在 IPv4 と IPv6 を使用した DirectAccess シングルサーバーセットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)」に記載されているすべての手順を完了します。

-   [手順 2: ROUTER1 をインストールし、構成](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9)します。 ROUTER1 は、企業ネットワークと2ネットワークのサブネット間のルーティングおよび転送機能を提供します。

-   [手順 3: すべての構成をインストールして構成](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee)します。 Windows 7 クライアントコンピューターは、windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 リモートアクセス展開の下位互換性を示すために使用されます。

-   [手順 4: 構成の構成](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810) 既定のゲートウェイとして ROUTER1 を使用し、代替 DNS サーバーとして 2-DC1 を構成します。

-   [手順 5: DC1 を構成](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a)します。 追加の Active Directory サイトと、Windows 7 クライアントコンピューター用の追加のセキュリティグループを使用して DC1 を構成します。

-   [手順 6: 2-DC1 をインストールし、構成](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127)します。 マルチサイト展開では、2つ以上のドメインとサイトがあります。 2-DC1 は、corp2.corp.contoso.com ドメインのドメインコントローラーと DNS サービスを提供します。

-   [手順 7: 2-3 をインストールし、構成](assetId:///7d04b54e-590a-4d33-9766-415789859f29)します。 2-"2" は、2つの企業ネットワークネットワーク内の web およびファイルサーバーです。

-   [手順 8: INET1 を構成する](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231) INET1 は、このテストラボガイドでインターネットをシミュレートします。 EDGE1 のパブリック IP アドレスに解決される DNS エントリを構成する必要があります。

-   [手順 9: EDGE1 を構成する](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e) EDGE1 で、2ネットワークの DNS サーバーとルーティングを構成します。

-   [手順 10: EDGE1 をインストールし、構成](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130)します。 マルチサイト展開では、2台のリモートアクセスサーバーが必要です。 2-EDGE1 は、2番目のドメインのリモートアクセスサービスを提供します。

-   [手順 11: マルチサイト展開を構成](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2)します。 両方のリモートアクセスサーバーを構成した後で、マルチサイト展開を構成することができます。

-   [手順 12: DirectAccess 接続をテスト](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c)します。 EDGE1 と EDGE1 を使用して、インターネットサブネットから両方のクライアントコンピューターからの DirectAccess 接続をテストします。

-   [手順 13: NAT デバイスの背後からの DirectAccess 接続をテスト](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c)します。 NAT デバイスの背後からの DirectAccess 接続をテストします。

-   [手順 14: 構成のスナップショットを設定](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84)します。 テストラボを完了したら、作業中のリモートアクセスマルチサイト展開のスナップショットを作成して、後で追加のシナリオをテストすることができるようにします。



