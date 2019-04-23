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
ms.openlocfilehash: 2b10428ff90c50c4d7e113552ddda3cca5447b06
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845833"
---
# <a name="remote-desktop-services---access-from-anywhere"></a>リモート デスクトップ サービスのどこからでもアクセス

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

エンドユーザーは、RD ゲートウェイを介して企業ファイアウォールの外側から安全に内部ネットワーク リソースに接続できます。

エンドユーザーのデスクトップを構成する方法に関係なく、RD ゲートウェイを高速でセキュリティで保護された接続の接続のフローに簡単に接続できます。 全体的な展開のプロパティを構成する場合に、エンドユーザー向けのパブリッシュされたフィードを通じて接続する RD ゲートウェイのプロパティを構成できます。 組織の RD ゲートウェイの名前に簡単にリモート デスクトップ クライアント アプリケーションが使用して接続プロパティとして、エンドユーザー向けのフィードせず自分のデスクトップへの接続を追加できます。

RD ゲートウェイの接続シーケンスの順序の 3 つの主な目的は次のとおりです。
1. **エンドユーザーのデバイスと RD ゲートウェイ サーバー間で暗号化された SSL トンネルを確立**:すべての RD ゲートウェイ サーバー経由で接続するには、RD ゲートウェイ サーバーが必要証明書をインストール、エンドユーザーのデバイスを認識します。 テストおよび概念実証のために、自己署名証明書を使用できますが、公的に信頼された証明機関から証明書がだけを運用環境で使用する必要があります。
2. **環境にユーザーを認証**:RD ゲートウェイは、IIS 認証を実行するサービスし、活用する RADIUS プロトコルを利用できるもの受信トレイを使用して[多要素認証](rds-plan-mfa.md)Azure MFA などのソリューションです。 別に作成された既定のポリシー、セキュリティで保護された環境内でどのリソースより具体的にはアクセスを付与するユーザーを定義する、追加の RD リソース承認ポリシー (RD Rap) および RD 接続承認ポリシー (RD Cap) を作成できます。
3. **エンドユーザーのデバイスと、指定されたリソースの間トラフィックを前後へ渡す**:RD ゲートウェイ接続が確立されている限り、このタスクを実行し続けます。 デバイスから離れている場合に、環境のセキュリティを維持するために RD ゲートウェイ サーバーでは、別のタイムアウト プロパティを指定できます。

リモート デスクトップ サービス展開の全体的なアーキテクチャの詳細が見つかります[デスクトップ ホスティング参照アーキテクチャで](desktop-hosting-reference-architecture.md)します。