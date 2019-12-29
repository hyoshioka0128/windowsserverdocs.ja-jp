---
title: ARM と Azure Marketplace を使った RDS のシームレスな展開
description: ARM テンプレートと Azure Marketplace を使用して、Azure 内に小規模な RDS の展開を作成する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9ada41e929c5e67cfcb1dcc5e7b4bc761c762d99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387454"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>ARM と Azure Marketplace を使った RDS のシームレスな展開

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

リモート デスクトップ サービス (RDS) は、コスト効率よく Windows デスクトップおよびアプリケーションをホストするために選択できるプラットフォームです。 [Azure Marketplace のオファリング](#basic-rds-through-the-azure-marketplace)または[クイックスタート テンプレート](#customized-rds-using-quickstart-templates)を使用して、Azure IaaS のデプロイ上に迅速に RDS を作成することができます。 Azure Marketplace では、ユーザー用にテスト ドメインを作成し、テストと概念実証に対応するシンプルかつ簡単なメカニズムを提供します。 一方、クイックスタート テンプレートでは、既存のドメインを使用でき、運用環境を構築するための優れたツールを提供します。 設定が終わったら、Windows、Mac、iOS、および Android 対応の Microsoft リモート デスクトップ アプリを使用して、さまざまなプラットフォームとデバイスから、公開されたデスクトップおよびアプリケーションに接続できます。

## <a name="basic-rds-through-the-azure-marketplace"></a>Azure Marketplace 経由での基本の RDS

Azure Marketplace 経由での展開の作成は、最も迅速に起動して実行できる方法です。 すべてが完了したら、お使いの環境は[基本の RDS アーキテクチャ](desktop-hosting-logical-architecture.md#basic-deployment)のような外観になります。 オファリングによって、必要なすべての RDS コンポーネントが作成されます。作業としては、一定の情報を指定するだけでかまいません。 

マーケットプレースのオファリングを展開する場合には、次の情報を指定する必要があります。
- 管理者ユーザー名とパスワード。 これは、展開を管理する新しいユーザーです。
- DNS 名と AD ドメイン名。 これらは、作成される新しいリソースです。 必ず、意味のある名前にします。
- VM のサイズ。 RDSH エンドポイントに対して使用する VM のサイズを選択できます。 初期展開の後にサイズを手動で変更して、ワークロードやコストに対応するように VM を最適化することも可能です。

Azure Marketplace からスモール フットプリント RDS の展開を作成するには、次の手順を使用します。 

1. Azure Marketplace の RDS の展開を起動します。
   1. サインイン、 [Azure ポータル](https://portal.azure.com)します。
   2. **[新規]** をクリックして、展開を追加します。
   3. 検索フィールドに "RDS" と入力し、Enter キーを押します。
   4. **[リモート デスクトップ サービス (RDS)]、[基本]、[開発/テスト]** の順にクリックして、 **[作成]** をクリックします。
   5. ポータル内の手順に従って、RDS を作成して展開します。 上述した情報のような、主要な構成の詳細を追加します。 
2. 展開に接続します。 展開が終了したら、最後の手順として自分の展開を完了して接続するために、出力の部分を確認します。
   1. テスト デバイス上に[この PowerShell スクリプト](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)をダウンロードして実行し、RDS 展開への接続に必要な証明書をすべてインストールします。 
   
      この手順は、テスト フェーズの間にのみ必要になります。 運用環境で Azure 内に RDS を展開する場合、お使いの Web サーバー上で公的に信頼済みの SSL 証明書を購入して使用するなど、常にベスト プラクティスに従ってください。

   2. プロンプトが表示されたら、お使いの Azure アカウントにサインインします。 この新しい展開のために作成された Azure サブスクリプション、リソース グループ、およびパブリック IP アドレスを選択します。
   3. スクリプトが終了したら、RD Web ページが既定のブラウザーに起動されます。 展開時に指定した DNS アドレスと該当のページの URL を比較することで、RD Web ページを再確認することができます。 
   
      展開時に作成した管理者資格情報を使ってサインインし、自分用に公開されている既定のデスクトップを確認します。 また、RD Web サイトにユーザーを送信して、デスクトップとアプリケーションをテストすることもできます。

      > [!TIP]
      > ドメイン名または管理者ユーザーを忘れた場合 ポータル内の新しいリソース グループに戻り、 **[展開]** をクリックして、入力したパラメーターを表示します。

これで、RDS の展開ができたので、[ユーザーを追加して管理する](rds-user-management.md)ことができます。

## <a name="customized-rds-using-quickstart-templates"></a>クイックスタート テンプレートを使用してカスタマイズされた RDS

Azure Resource Manager テンプレートを使用して、Azure 内に RDS を展開できます。 これは、基本の RDS 展開にしようと考えているが、使用したい既存のコンポーネント (AD など) がある場合に、特に便利です。 Marketplace のオファリングとは異なり、仮想ネットワーク上での既存の AD の使用、RDSH VM 用のカスタム OS イメージの使用、RDS コンポーネントに対する高可用性での階層化など、より詳細なカスタマイズを実現できます。 各コンポーネントに対する高可用性に追加すると、以降は、お使いの環境が[高可用性 RDS アーキテクチャ](desktop-hosting-logical-architecture.md#highly-available-deployment)のような外観になります。

Azure RDS テンプレートを利用してスモール フットプリント RDS の展開を作成するには、次の手順を使用します。 

1. Azure クイックスタート テンプレートを選びます。
   1. [RDS の Azure クイックスタート テンプレート](https://aka.ms/rdautomation)のサイトに移動します。
   2. 試行する作業と一致するテンプレートを選択します。 必ず、該当のテンプレートの前提条件をすべて満たすようにしてください (たとえば、VM 用にカスタム イメージを使用する場合、必ず、Azure ストレージ アカウントにそのイメージが既にアップロード済みになっているようにしてください)。
   3. **[Azure に配置する]** をクリックします。
   4. Azure portal 内で、一定の詳細情報 (管理者ユーザー名、AD ドメイン名など) を指定する必要があります。 これは、選択したテンプレートに基づいて異なります。
   5. **[購入]** をクリックします。
2. 展開に接続します。 
   1. テスト デバイス上に[この PowerShell スクリプト](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)をダウンロードして実行し、RDS 展開への接続に必要な証明書をすべてインストールします。 
   
      この手順は、テスト フェーズの間にのみ必要になります。 運用環境で Azure 内に RDS を展開する場合、お使いの Web サーバー上で公的に信頼済みの SSL 証明書を購入して使用するなど、常にベスト プラクティスに従ってください。

   2. プロンプトが表示されたら、お使いの Azure アカウントにサインインします。 この新しい展開のために作成された Azure サブスクリプション、リソース グループ、およびパブリック IP アドレスを選択します。
   3. スクリプトが終了したら、RD Web ページが既定のブラウザーに起動されます。 展開時に指定した DNS アドレスと該当のページの URL を比較することで、RD Web ページを再確認することができます。 
   
      展開時に作成した管理者資格情報を使ってサインインし、自分用に公開されている既定のデスクトップを確認します。 また、RD Web サイトにユーザーを送信して、デスクトップとアプリケーションをテストすることもできます。

      > [!TIP]
      > ドメイン名または管理者ユーザーを忘れた場合 ポータル内の新しいリソース グループに戻り、 **[展開]** をクリックして、入力したパラメーターを表示します。

これで、RDS の展開ができたので、[ユーザーを追加して管理する](rds-user-management.md)ことができます。
