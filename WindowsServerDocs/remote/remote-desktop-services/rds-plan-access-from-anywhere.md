---
title: リモート デスクトップ サービスのどこからでもアクセス
description: RD ゲートウェイの計画に関する情報
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c38fab1-3586-4b7a-8bf0-7d85a8d5361d
author: lizap
ms.author: elizapo
ms.date: 11/03/2016
manager: dongill
ms.openlocfilehash: 0d3d8ed036b3befd81da6d5bbe8702ee866c6aa8
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63748826"
---
# <a name="remote-desktop-services---access-from-anywhere"></a>リモート デスクトップ サービスのどこからでもアクセス

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

エンドユーザーは、RD ゲートウェイを介して企業ファイアウォールの外側から安全に内部ネットワーク リソースに接続できます。

エンドユーザーのデスクトップを構成する方法に関係なく、RD ゲートウェイを高速でセキュリティで保護された接続の接続のフローに簡単に接続できます。 全体的な展開のプロパティを構成する場合に、エンドユーザー向けのパブリッシュされたフィードを通じて接続する RD ゲートウェイのプロパティを構成できます。 組織の RD ゲートウェイの名前に簡単にリモート デスクトップ クライアント アプリケーションが使用して接続プロパティとして、エンドユーザー向けのフィードせず自分のデスクトップへの接続を追加できます。

RD ゲートウェイの接続シーケンスの順序の 3 つの主な目的は次のとおりです。
1. **エンドユーザーのデバイスと RD ゲートウェイ サーバー間で暗号化された SSL トンネルを確立する**:任意の RD ゲートウェイ サーバー経由で接続するには、その RD ゲートウェイ サーバーに、エンドユーザーのデバイスが認識する証明書がインストールされている必要があります。 テストおよび概念実証のために、自己署名証明書を使用できますが、公的に信頼された証明機関から証明書がだけを運用環境で使用する必要があります。
2. **環境にユーザーを認証する**:RD ゲートウェイは、インボックス IIS サービスを使用して認証を実行し、RADIUS プロトコルを利用して Azure MFA などの[多要素認証](rds-plan-mfa.md)ソリューションを活用することもできます。 別に作成された既定のポリシー、セキュリティで保護された環境内でどのリソースより具体的にはアクセスを付与するユーザーを定義する、追加の RD リソース承認ポリシー (RD Rap) および RD 接続承認ポリシー (RD Cap) を作成できます。
3. **エンドユーザーのデバイスと、指定されたリソースの間で双方向にトラフィックを渡す**:RD ゲートウェイは、接続が確立される限り、このタスクの実行を続行します。 ユーザーがデバイスから離れる場合に環境のセキュリティを保持するため、RD ゲートウェイ サーバーでさまざまなタイムアウト プロパティを指定できます。

リモート デスクトップ サービス展開の全体的なアーキテクチャの詳細については、「[デスクトップ ホスティングの参照アーキテクチャ](desktop-hosting-reference-architecture.md)」を参照してください。