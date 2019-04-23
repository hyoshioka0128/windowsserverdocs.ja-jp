---
title: テスト ラボの構成手順
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2bda808336624a5d80ed44cbadf543fc134c6190
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827883"
---
# <a name="steps-for-configuring-the-test-lab"></a>テスト ラボの構成手順

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の手順では、リモート アクセス インフラストラクチャを構成し、リモート アクセス サーバーとクライアントを構成して、インターネットとホームネット サブネットからの DirectAccess の接続をテストする方法について説明します。  
  
このテスト ラボ ガイドでは、次の手順を実行することによって、リモート アクセスのマルチサイト展開を作成します。  
  
-   [手順 1:基本構成を完了](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed)します。 すべての手順を完了、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)します。  
  
-   [手順 2:インストールし、構成 ROUTER1](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9)します。 ROUTER1 ルーティングおよび転送の企業ネットワークと 2 Corpnet サブネット間の機能を提供します。  
  
-   [手順 3:インストールし、CLIENT2 を構成する](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee)します。 CLIENT2 は Windows 7 クライアント コンピューターを示すために使用される、旧バージョンと Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 のリモート アクセスの展開との互換性。  
  
-   [手順 4:APP1 を構成する](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810)します。 デフォルト ゲートウェイと代替の DNS サーバーとして 2 DC1 として ROUTER1 に APP1 を構成します。  
  
-   [手順 5:DC1 を構成する](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a)します。 追加の Active Directory サイトと Windows 7 クライアント コンピューターの追加のセキュリティ グループには、DC1 を構成します。  
  
-   [手順 6:インストールし、構成 2 DC1](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127)します。 マルチサイト展開では、2 つ以上のドメインとサイトがあります。 2 DC1 は、ドメイン コント ローラーと corp2.corp.contoso.com ドメインの DNS サービスを提供します。  
  
-   [手順 7:インストールおよび 2 APP1 を構成する](assetId:///7d04b54e-590a-4d33-9766-415789859f29)します。 2 APP1 は、2-企業ネットワークのネットワーク上の web サービスとファイル サーバーです。  
  
-   [手順 8:構成 INET1](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231)します。 INET1 は、このテスト ラボ ガイドでインターネットをシミュレートします。 2 EDGE1 のパブリック IP アドレスに解決される DNS エントリを構成する必要があります。  
  
-   [手順 9:EDGE1 構成](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e)します。 2-企業ネットワークの DNS サーバーと EDGE1 上のルーティングを構成します。  
  
-   [手順 10:インストールし、構成 2 EDGE1](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130)します。 マルチサイト展開では、2 つのリモート アクセス サーバーが必要です。 2 EDGE1 では、2 番目のドメインのリモート アクセス サービスを提供します。  
  
-   [手順 11:マルチサイト展開を構成する](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2)します。 両方のリモート アクセス サーバーを構成した後、マルチサイト展開を構成できます。  
  
-   [手順 12:DirectAccess 接続をテストする](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c)します。 EDGE1 と 2 EDGE1 でインターネット サブネットからの両方のクライアント コンピューターから DirectAccess の接続をテストします。  
  
-   [手順 13:NAT デバイスの背後からの DirectAccess 接続をテストする](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c)します。 NAT デバイスの背後からの DirectAccess の接続をテストします。  
  
-   [手順 14:構成のスナップショット](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84)します。 テスト ラボを完了するには、その他のシナリオをテストするには、後で戻すことができるように作業用のリモート アクセスのマルチサイト展開のスナップショットを取得します。  
  


