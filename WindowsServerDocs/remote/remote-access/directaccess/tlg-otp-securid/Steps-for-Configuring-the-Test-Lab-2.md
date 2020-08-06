---
title: OTP 認証と RSA SecurID を使用してテストラボを構成する手順
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 21a4fe4de5029c009594a0e8dc01dc4570e9e557
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769680"
---
# <a name="steps-for-configuring-the-test-lab-with-otp-authentication-and-rsa-securid"></a>OTP 認証と RSA SecurID を使用してテストラボを構成する手順

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順では、リモートアクセスインフラストラクチャを構成し、リモートアクセスサーバーとクライアントを構成し、Homenet およびインターネットサブネットからの DirectAccess 接続をテストする方法について説明します。

このテストラボガイドでは、次の手順を実行して、OTP 環境でリモートアクセスを構築します。

-   [手順 1: DirectAccess の構成を完了](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6)します。 [「テストラボガイド: 混在 IPv4 と IPv6 を使用した DirectAccess シングルサーバーセットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)」に記載されているすべての手順を完了します。

-   [手順 2:](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff)"1" を構成します。 EDGE1 で使用するために、OTP 証明書テンプレートを使用して、の構成を構成します。

-   [手順 3: DC1 を構成](assetId:///904a6edc-a771-45ed-9630-a34a680bb522)します。 DC1 に定義されているユーザープリンシパル名を確認してください。

-   [手順 7: RSA をインストールして構成する](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a)。 RSA、RADIUS および OTP サーバーをインストールして構成し、OTP 用に EDGE1 を構成します。

-   [手順 11: EDGE1 で OTP の正常性を確認](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba)します。 リモートアクセスサーバーで OTP の状態が正常であることを確認します。

-   [手順 8: Homenet サブネットからの DirectAccess 接続をテスト](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14)します。 NAT デバイスの背後から DirectAccess OTP 機能をテストします。

-   [手順 10: インターネットからの DirectAccess 接続をテスト](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9)します。 インターネットからの DirectAccess クライアント接続をテストします。

-   [手順 12: 構成のスナップショットを設定](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4)します。 テストラボを完了したら、OTP 構成を使用して動作する DirectAccess のスナップショットを作成します。これにより、後で追加のシナリオをテストすることができます。



