---
title: ファイル サービスのコンテンツ サーバーをインストールする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4fb9e40ce34a82a8797db1bf6d61c739f742c2d3
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319239"
---
# <a name="install-file-services-content-servers"></a>ファイル サービスのコンテンツ サーバーをインストールする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ファイル サービス サーバーの役割を実行しているコンテンツ サーバーを展開するには、ファイル サービス サーバー ロールのネットワーク ファイルのロール サービスの BranchCache をインストールしてください。 さらに、ニーズに合わせて、ファイル共有の BranchCache を有効する必要があります。  
  
コンテンツ サーバーの構成時にすべてのファイル共有のコンテンツの BranchCache の公開を許可することができます。 または発行するファイル共有のサブセットを選択することができます。  
  
> [!NOTE]  
> BranchCache の有効なファイル サーバーやコンテンツ サーバーと Web サーバーを展開するときにコンテンツ情報がここでオフラインで計算、BranchCache クライアントがファイルを要求する前にもします。 この機能強化のためする不要コンテンツ サーバーでは、ハッシュの発行を構成する BranchCache の以前のバージョンで実行したようです。  
>   
> この自動ハッシュの生成は、パフォーマンスが向上し、多くの帯域幅の節減コンテンツ情報は、コンテンツを要求する最初のクライアントの準備ができているため、計算は既に実行されています。  
  
コンテンツ サーバーを展開するには、以下のトピックを参照してください。  
  
-   [ファイル サービス サーバーの役割を構成する](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [ファイルサーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [ファイル共有&#40;で BranchCache を有効にする (省略可能)&#41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


