---
title: カスタマー エクスペリエンスのテスト
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 40590d50441013ebc1dad5e3e52b3aac07419f91
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311511"
---
# <a name="testing-the-customer-experience"></a>カスタマー エクスペリエンスのテスト

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

カスタマー エクスペリエンスを確認し、パートナーのカスタマイズをチェックするには、ターゲット コンピューターの初期構成を実行します。 カスタマー エクスペリエンスを確認するには、初期構成を少なくとも 1 回手動で完了することを推奨します。 ダッシュボードをブランド提携した場合、ブランド化を確認するには初期構成を完了する必要があります。 リモート Web アクセスサイトをブランド化している場合は、 http://< servername\> にアクセスして、ブランド化を確認する必要があります (< servername\> はサーバーの名前です)。 cfg.ini ファイルの初期構成セクションを使用して、カスタマー エクスペリエンスのテストを自動化できます。 cfg.ini ファイルでのこのセクションの作成の詳細については、「[Cfg.ini ファイルの作成](Create-the-Cfg.ini-File.md)」を参照してください。  
  
> [!IMPORTANT]
>  初期構成エクスペリエンスをテストする前に、Sysprep.exe コマンドを実行して、イメージ展開を準備する必要があります。 Sysprep.exe の実行の詳細については、「[イメージの展開の準備](Preparing-the-Image-for-Deployment.md)」を参照してください。  
  
> [!IMPORTANT]
>  初期構成をテストするには、ネットワーク接続が必要です。 サーバー上で DHCP が構成されたり、インストールされていないと、干渉なしのネットワーク テストが可能です。  
  
 パートナーのサポート情報を確認するには、ダッシュボードで [ヘルプ] ボタンの隣にある下矢印をクリックします。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)