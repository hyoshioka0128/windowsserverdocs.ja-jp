---
title: カスタマー エクスペリエンスのテスト
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838693"
---
# <a name="testing-the-customer-experience"></a>カスタマー エクスペリエンスのテスト

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

カスタマー エクスペリエンスを確認し、パートナーのカスタマイズをチェックするには、ターゲット コンピューターの初期構成を実行します。 カスタマー エクスペリエンスを確認するには、初期構成を少なくとも 1 回手動で完了することを推奨します。 ダッシュボードをブランド提携した場合、ブランド化を確認するには初期構成を完了する必要があります。 リモート Web アクセス サイトをブランド提携する場合は、 http://<servername をアクセスする必要があります\>、ブランド化を確認する (< servername\>サーバーの名前を指定します)。 cfg.ini ファイルの初期構成セクションを使用して、カスタマー エクスペリエンスのテストを自動化できます。 cfg.ini ファイルでのこのセクションの作成の詳細については、「[Cfg.ini ファイルの作成](Create-the-Cfg.ini-File.md)」を参照してください。  
  
> [!IMPORTANT]
>  初期構成エクスペリエンスをテストする前に、Sysprep.exe コマンドを実行して、イメージ展開を準備する必要があります。 Sysprep.exe の実行の詳細については、「[イメージの展開の準備](Preparing-the-Image-for-Deployment.md)」を参照してください。  
  
> [!IMPORTANT]
>  初期構成をテストするには、ネットワーク接続が必要です。 サーバー上で DHCP が構成されたり、インストールされていないと、干渉なしのネットワーク テストが可能です。  
  
 パートナーのサポート情報を確認するには、ダッシュボードで [ヘルプ] ボタンの隣にある下矢印をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)