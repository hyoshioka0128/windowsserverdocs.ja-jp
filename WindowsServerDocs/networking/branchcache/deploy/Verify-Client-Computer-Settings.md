---
title: クライアント コンピューターの設定を確認します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d507f2097a9349cbefba520ad0dc143e0dd7452e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="verify-client-computer-settings"></a>クライアント コンピューターの設定を確認します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache のクライアント コンピューターが正しく構成されていることを確認します。  
  
> [!NOTE]  
> この手順には、BranchCache サービスを再起動して、グループ ポリシーを手動で更新するための手順が含まれています。 このような状況で自動的に発生すると、コンピューターを再起動する場合、これらの操作を実行する必要はありません。  
  
メンバーである必要がある**管理者**、またはこの手順を実行することに相当します。  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>BranchCache クライアント コンピューターの設定を確認するには  
  
1.  クライアント コンピューターの BranchCache 構成を確認するには、グループ ポリシーを更新するに管理者として Windows PowerShell を実行、次のコマンドを入力し、ENTER キーを押します。  
  
    `gpupdate /force`  
  
2.  ホスト型キャッシュ モードで構成され、が構成されているクライアント コンピューターを自動的に検出キャッシュ サーバーによってホスト サービス接続ポイント、BranchCache サービス停止して再起動するには、次のコマンドを実行します。  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  次のコマンドを実行して現在の BranchCache の動作モードを検査します。  
  
    `Get-BCStatus`  
  
4.  Windows PowerShell での出力を確認、 **Get BCStatus**コマンド。  
  
    値は、 **BranchCacheIsEnabled**する必要があります**True**します。  
  
    **ClientSettings**の値は、 **CurrentClientMode**する必要があります**DistributedClient**または**HostedCacheClient**このガイドを使用するように構成するモードに応じて、します。  
  
    **ClientSettings**ホスト型キャッシュ モードに構成されていると、構成中に、ホスト型キャッシュ サーバーの名前を指定したまたはホスト型キャッシュ サーバーのサービス接続ポイントを使用しての場合は、クライアントが自動的に配置する場合は、 **HostedCacheServerList**またはホスト型キャッシュ サーバーの名前と同じである値を持っている必要があります。 たとえば、HCS1 とドメインの名前は、ホスト型キャッシュ サーバーの場合は、corp.contoso.com の値の**HostedCacheServerList**は**HCS1.corp.contoso.com**します。  
  
5.  BranchCache の設定が上記のいずれかのグループ ポリシーまたはローカル コンピューター ポリシーの設定だけでなく、ファイアウォールの例外を構成したことを確認する、このガイドの手順を使用していることを確認、適切な値があるない場合、それらが正しいします。 さらに、コンピューターを再起動またはグループ ポリシーを更新し、BranchCache サービスを再起動するには、この手順の手順に従います。  
  


