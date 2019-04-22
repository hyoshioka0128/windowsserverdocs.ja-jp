---
title: ARM と Azure Marketplace を使った RDS のシームレスな展開
description: ARM テンプレートと Azure Marketplace を使用して Azure での小規模な RDS デプロイを作成する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f72ceb6-6f90-48f6-bfc3-bdad63984ce7
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 02/10/2017
ms.openlocfilehash: e4de3d4ac14a0dbc5500fd7ab8bd8f1568f3da53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823083"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>ARM と Azure Marketplace を使った RDS のシームレスな展開

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2

リモート デスクトップ サービス (RDS) は、コスト効率よく Windows デスクトップおよびアプリケーションをホストする任意のプラットフォームです。 使用することができます、 [Azure Marketplace サービス](#basic-rds-through-the-azure-marketplace)または[クイック スタート テンプレート](#Customized-RDS-using-Quickstart-templates)Azure IaaS のデプロイで、RDS をすばやく作成します。 Azure marketplace では、するため、シンプルで簡単なメカニズムは、テストや概念実証のテスト ドメインを作成します。 一方で、クイック スタート テンプレートを使用すると、運用環境を構築するための優れたツールにすること、既存のドメインを使用できます。 設定すると接続できます、パブリッシュされたデスクトップとアプリケーションをさまざまなプラットフォームやデバイスから Windows、Mac、iOS、および Android 用 Microsoft リモート デスクトップ アプリを使用します。

## <a name="basic-rds-through-the-azure-marketplace"></a>Azure Marketplace 経由で基本的な RDS

Azure Marketplace からデプロイを作成して取得する最も簡単な方法は、実行します。 すべてが完了したら、環境内の外観、[基本的な RDS アーキテクチャ](desktop-hosting-logical-architecture.md#basic-deployment)します。 サービス/データは、必要があります - 行う必要があるはいくつかの情報を指定するすべての RDS のコンポーネントを作成します。 

Marketplace のオファリングをデプロイするときに、次の情報を指定する必要があります。
- 管理者のユーザー名とパスワード。 これは、展開を管理する新しいユーザーです。
- DNS 名と AD ドメイン名。 これらは、作成される新しいリソースです。 名前が意味のあることを確認します。
- VM のサイズ。 RDSH エンドポイントに対して使用する Vm のサイズを選択できます。 手動で Vm をワークロードのコストを最適化するための初期デプロイ後、サイズを変更できます。

Azure Marketplace から、コンパクトな RDS 展開を作成するのにには、次の手順を使用します。 

1. Azure Marketplace の RDS の展開を起動します。
   1. [Azure ポータル](https://portal.azure.com)することができます。
   2. クリックして**新規**展開を追加します。
   3. 検索フィールドに"RDS"を入力し、Enter キーを押します。
   4. クリックして**リモート デスクトップ サービス (RDS) - Basic - 開発/テスト**、 をクリックし、**作成**。
   5. 作成し、rds. をデプロイするには、ポータルでの手順に従います 上記の情報など、キーの構成の詳細情報を追加します。 
2. 配置に接続します。 デプロイが完了したら、最後の手順を完了し、デプロイへの接続の outputs セクションを確認します。
   1. ダウンロードし、実行[この PowerShell スクリプト](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)テスト デバイスに RDS デプロイに接続するために必要なすべての証明書をインストールします。 
   
      この手順は、テスト フェーズ中にのみ必要です。 運用環境で Azure での RDS をデプロイする場合は、購入して、公的に信頼された SSL 証明書を使用して、web サーバー上のようなベスト プラクティスに従う確認します。

   2. 入力を求められたら、Azure アカウントにサインインします。 Azure サブスクリプション、リソース グループ、およびパブリック IP アドレスがこの新しいデプロイの作成を選択します。
   3. スクリプトが完了したら、RD Web ページは、既定のブラウザーで起動されます。 RD Web ページを再確認するには、デプロイ時に指定する DNS アドレスをページの URL を比較します。 
   
      自分に公開する既定のデスクトップを表示する展開中に作成した管理者の資格情報でサインインします。 ユーザーは、デスクトップやアプリケーションをテストする RD Web サイトも送信できます。

      > [!TIP]
      > ドメイン名または管理者のユーザーを忘れた場合 移動することができます、ポータルで新しいリソース グループを移動してクリックして**展開**、し、入力したパラメーターを表示します。

RDS のデプロイがあるに[を追加して、ユーザーを管理する](rds-user-management.md)します。

## <a name="customized-rds-using-quickstart-templates"></a>クイック スタート テンプレートを使用してカスタマイズされた RDS

Azure Resource Manager テンプレートを使用して、Azure での RDS をデプロイすることができます。 これは、基本的な RDS 展開を目的に使用する (AD) などの既存のコンポーネントがある場合に特に便利です。 Marketplace のサービスとは異なりには、RDSH 仮想マシンとの高可用性 RDS のコンポーネントの階層化のカスタム OS イメージを使用して、既存の AD を使用して、仮想ネットワークなど、さらにカスタマイズ作成できます。 高可用性の各コンポーネントに追加すると、環境内のようになります、[書き込める RDS アーキテクチャ高](desktop-hosting-logical-architecture.md#highly-available-deployment)します。

Azure の RDS のテンプレートを使用したコンパクトな RDS 展開を作成するのにには、次の手順を使用します。 

1. Azure クイック スタート テンプレートを選択します。
   1. 移動して、 [RDS Azure クイック スタート テンプレート](https://aka.ms/rdautomation)サイト。
   2. 何を行うと一致するテンプレートを選択します。 その特定のテンプレートの前提条件を満たしていることを確認します。 (たとえば、Vm のカスタム イメージを使用している場合を確認してください、Azure ストレージ アカウントにそのイメージを既にアップロード)
   3. クリックして**を Azure にデプロイ**します。
   4. Azure portal では、(管理者ユーザー名、AD ドメイン名) などのいくつかの詳細を提供する必要があります。 これは、選択したテンプレートに基づいて異なります。
   5. クリックして**購入**します。
2. 配置に接続します。 
   1. ダウンロードし、実行[この PowerShell スクリプト](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)テスト デバイスに RDS デプロイに接続するために必要なすべての証明書をインストールします。 
   
      この手順は、テスト フェーズ中にのみ必要です。 運用環境で Azure での RDS をデプロイする場合は、購入して、公的に信頼された SSL 証明書を使用して、web サーバー上のようなベスト プラクティスに従う確認します。

   2. 入力を求められたら、Azure アカウントにサインインします。 Azure サブスクリプション、リソース グループ、およびパブリック IP アドレスがこの新しいデプロイの作成を選択します。
   3. スクリプトが完了したら、RD Web ページは、既定のブラウザーで起動されます。 RD Web ページを再確認するには、デプロイ時に指定する DNS アドレスをページの URL を比較します。 
   
      自分に公開する既定のデスクトップを表示する展開中に作成した管理者の資格情報でサインインします。 ユーザーは、デスクトップやアプリケーションをテストする RD Web サイトも送信できます。

      > [!TIP]
      > ドメイン名または管理者のユーザーを忘れた場合 移動することができます、ポータルで新しいリソース グループを移動してクリックして**展開**、し、入力したパラメーターを表示します。

RDS のデプロイがあるに[を追加して、ユーザーを管理する](rds-user-management.md)します。
