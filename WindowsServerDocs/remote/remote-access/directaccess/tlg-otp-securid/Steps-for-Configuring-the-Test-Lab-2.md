---
title: テスト ラボの構成手順
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 991f06568a16f7e8bcce3bc6c86eef3467ea31e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826293"
---
# <a name="steps-for-configuring-the-test-lab"></a>テスト ラボの構成手順

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の手順では、リモート アクセス インフラストラクチャを構成し、リモート アクセス サーバーとクライアントを構成して、ホームネットとインターネットのサブネットからの DirectAccess の接続をテストする方法について説明します。  
  
このテスト ラボ ガイドでは、次の手順を実行して OTP 環境とリモート アクセスを作成します。  
  
-   [手順 1:DirectAccess の構成を完了](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6)します。 すべての手順を完了、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)します。  
  
-   [手順 2:APP1 を構成する](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff)します。 EDGE1 で使用するための OTP 証明書テンプレートでは、APP1 を構成します。  
  
-   [手順 3:DC1 を構成する](assetId:///904a6edc-a771-45ed-9630-a34a680bb522)します。 DC1 でユーザー プリンシパル名が定義されていることを確認します。  
  
-   [手順 7:インストールし、構成の RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a)します。 インストールして、RSA、RADIUS、OTP サーバーを構成し、OTP 用 EDGE1 を構成します。  
  
-   [手順 11:EDGE1 で OTP の正常性を確認します。](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba)します。 OTP の状態がリモート アクセス サーバーで正常な状態を確認します。  
  
-   [手順 8:ホームネット サブネットからの DirectAccess 接続をテスト](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14)します。 NAT デバイスの背後からの DirectAccess の OTP の機能をテストします。  
  
-   [手順 10:インターネットから DirectAccess 接続をテスト](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9)します。 インターネットから DirectAccess クライアントの接続をテストします。  
  
-   [手順 12:構成のスナップショット](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4)します。 テスト ラボを完了するには、その他のシナリオをテストするには、後で戻すことができるように DirectAccess OTP の構成での作業のスナップショットを取得します。  
  


