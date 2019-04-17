---
title: ファイル サービスのコンテンツ サーバーをインストールします。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7036323e7cc31bd14be8025b6064a806fb45ef19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-file-services-content-servers"></a>ファイル サービスのコンテンツ サーバーをインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ファイル サービス サーバーの役割を実行しているコンテンツ サーバーを展開するには、ファイル サービス サーバーの役割のネットワーク ファイルのロール サービスの BranchCache をインストールする必要があります。 さらに、ニーズに合わせて、ファイル共有に対して BranchCache を有効する必要があります。  
  
コンテンツ サーバーの構成時にすべてのファイル共有のコンテンツの BranchCache の公開を許可するまたは発行するファイル共有のサブセットを選択することができます。  
  
> [!NOTE]  
> 展開すると、BranchCache の有効なファイル サーバーまたは Web サーバーをコンテンツ サーバーとして、コンテンツ情報ができるようになりました計算オフラインで、BranchCache クライアントがファイルを要求する前にもされます。 この改善により、ため必要はありませんをコンテンツ サーバーでは、ハッシュの発行を構成する BranchCache の以前のバージョンで行ったようです。  
>   
> この自動ハッシュの生成は、高速なパフォーマンスと帯域幅が節約、コンテンツ情報は、コンテンツを要求する最初のクライアントの準備ができているためと計算は既に実行されています。  
  
コンテンツ サーバーを展開する次のトピックを参照してください。  
  
-   [ファイル サービス サーバーの役割を構成します。](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [ファイル サーバーのハッシュの発行を有効にします。](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [ファイル共有 (&) #40; で BranchCache を有効にするオプション (& a) #41 です。](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


