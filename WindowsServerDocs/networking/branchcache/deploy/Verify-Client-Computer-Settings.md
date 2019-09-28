---
title: クライアント コンピューターの設定を確認します。
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6d0adbf0db2d7888ca12ca49f50fc37baa8cbc16
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356508"
---
# <a name="verify-client-computer-settings"></a>クライアント コンピューターの設定を確認します。

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache のクライアント コンピューターが正しく構成されていることを確認します。  
  
> [!NOTE]  
> この手順には、BranchCache サービスを再起動して、グループ ポリシーを手動で更新するための手順が含まれています。 この状況では自動的に発生したが、コンピューターを再起動する場合、これらの操作を実行する必要はありません。  
  
メンバーである必要があります **管理者**, 、またはこの手順を実行に相当します。  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>BranchCache クライアント コンピューターの設定を確認するには  
  
1.  BranchCache 構成を確認するクライアント コンピューターのグループ ポリシーを更新するには、Windows PowerShell を管理者として実行を選択し、次のコマンドを入力し、ENTER キーを押します。  
  
    `gpupdate /force`  
  
2.  構成されているホスト型キャッシュ モードで構成されているクライアント コンピューターが自動的に検出キャッシュ サーバーによってホスト サービス接続ポイント、BranchCache サービス停止して再起動するには、次のコマンドを実行します。  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  次のコマンドを実行して、BranchCache の現在の操作モードを検査します。  
  
    `Get-BCStatus`  
  
4.  Windows PowerShell での出力を確認、 **Get BCStatus** コマンドです。  
  
    値 **BranchCacheIsEnabled** べき **True**します。  
  
    **ClientSettings**, の値 **CurrentClientMode** する必要があります **DistributedClient** または **HostedCacheClient**, 、このガイドを使用するように構成するモードによって異なります。  
  
    **ClientSettings**, または構成しているホスト型キャッシュ モードと構成では、中にホスト型キャッシュ サーバーの名前を指定したクライアントが自動的に配置されている場合にサービス接続ポイントを使用して、キャッシュ サーバーがホストされている場合は、 **HostedCacheServerList** 名またはホスト型キャッシュ サーバーの名前は、同じ値になります。 たとえば、HCS1 とドメインにホスト型キャッシュ サーバーがという名前の場合は、corp.contoso.com の値 **HostedCacheServerList** は **HCS1.corp.contoso.com**します。  
  
5.  BranchCache の設定が上記のいずれかのグループ ポリシーまたはローカル コンピューター ポリシーの設定とファイアウォールの例外を構成していることを確認する、このガイドの手順を使用していることを確認、適切な値があるない場合は、正しいはします。 さらに、コンピューターを再起動するか、グループ ポリシーを更新し、BranchCache サービスを再起動するには、この手順の手順に従います。  
  


