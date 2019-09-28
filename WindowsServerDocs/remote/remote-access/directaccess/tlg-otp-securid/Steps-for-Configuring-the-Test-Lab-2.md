---
title: テスト ラボの構成手順
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ef5ce37983b8565fab8287eeaae7423be0c269f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404723"
---
# <a name="steps-for-configuring-the-test-lab"></a>テスト ラボの構成手順

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順では、リモートアクセスインフラストラクチャを構成し、リモートアクセスサーバーとクライアントを構成し、Homenet およびインターネットサブネットからの DirectAccess 接続をテストする方法について説明します。  
  
このテストラボガイドでは、次の手順を実行して、OTP 環境でリモートアクセスを構築します。  
  
-   [手順 1:DirectAccess の構成 @ no__t-0 を完了します。 @No__t-0Test Lab Guide のすべての手順を完了します。IPv4 と IPv6 が混在する DirectAccess のシングルサーバーセットアップのデモンストレーション @ no__t-0  
  
-   [手順 2:No__t を構成します。 EDGE1 で使用するために、OTP 証明書テンプレートを使用して、の構成を構成します。  
  
-   [手順 3:DC1 @ no__t を構成します。 DC1 に定義されているユーザープリンシパル名を確認してください。  
  
-   [手順 7:RSA @ no__t をインストールして構成します。 RSA、RADIUS および OTP サーバーをインストールして構成し、OTP 用に EDGE1 を構成します。  
  
-   [手順 11:EDGE1 @ no__t-0 で OTP の正常性を確認します。 リモートアクセスサーバーで OTP の状態が正常であることを確認します。  
  
-   [手順 8:Homenet サブネット @ no__t からの DirectAccess 接続をテストします。 NAT デバイスの背後から DirectAccess OTP 機能をテストします。  
  
-   [手順 10:Internet @ no__t から DirectAccess 接続をテストします。 インターネットからの DirectAccess クライアント接続をテストします。  
  
-   [手順 12:構成 @ no__t-0 のスナップショットを設定します。 テストラボを完了したら、OTP 構成を使用して動作する DirectAccess のスナップショットを作成します。これにより、後で追加のシナリオをテストすることができます。  
  


