---
title: "カスタマー エクスペリエンスのテスト"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 223b0e1be3a53e9a7d198dc005fc8725e421db58
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="testing-the-customer-experience"></a>カスタマー エクスペリエンスのテスト

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

カスタマー エクスペリエンスを確認し、パートナーのカスタマイズを確認して、ターゲット コンピューターの初期構成を実行します。 完了している、初期構成に少なくとも 1 回手動でカスタマー エクスペリエンスを順番に処理をお勧めします。 ダッシュ ボードをブランド提携する場合は、ブランド化を確認する初期構成を完了する必要があります。 リモート Web アクセス サイトをブランド提携する場合 http://<servername\> にアクセスする必要があります。ブランド化を確認する (< servername\ > では、サーバーの名前です)。 Cfg.ini ファイルの初期構成セクションを使用するには、カスタマー エクスペリエンスのテストを自動化します。 Cfg.ini ファイルのこのセクションの作成の詳細については、次を参照してください。[Cfg.ini ファイルの作成](Create-the-Cfg.ini-File.md)します。  
  
> [!IMPORTANT]
>  初期構成エクスペリエンスをテストする前に、展開のイメージを準備して Sysprep.exe コマンドを実行する必要があります。 Sysprep.exe の実行に関する詳細については、次を参照してください。[イメージの展開の準備](Preparing-the-Image-for-Deployment.md)します。  
  
> [!IMPORTANT]
>  初期構成をテストするには、ネットワーク接続が必要です。 DHCP が構成されているまたはこれにより、干渉なしのネットワーク テスト サーバーにインストールできません。  
  
 ダッシュ ボードで、[パートナーのサポート情報を確認するには、[ヘルプ] ボタンの横にある下向き矢印をクリックします。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)