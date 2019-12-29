---
title: ホストされたキャッシュ サーバーを展開する (省略可能)
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 69dc525a093c86d57b665e26ff5acaf2679c81a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356435"
---
# <a name="deploy-hosted-cache-servers-optional"></a>ホストされたキャッシュ サーバーを展開する (省略可能)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

BranchCache ホスト型キャッシュモードを展開するブランチオフィスに配置されている BranchCache ホスト型キャッシュサーバーをインストールして構成するには、次の手順に従います。 Windows Server 2016 の BranchCache では、1つのブランチオフィスに複数のホスト型キャッシュサーバーを展開できます。  
  
> [!IMPORTANT]  
> 分散キャッシュモードではブランチオフィスにホスト型キャッシュサーバーコンピューターを必要としないため、この手順は省略可能です。 ブランチオフィスにホスト型キャッシュモードを展開する予定がない場合は、ホスト型キャッシュサーバーを配置する必要はありません。この手順を実行する必要はありません。  
  
メンバーである必要があります **管理者**, 、またはこの手順を実行に相当します。  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>ホスト型キャッシュサーバーをインストールして構成するには  
  
1.  ホスト型キャッシュサーバーとして構成するコンピューターで、Windows PowerShell プロンプトで次のコマンドを実行して BranchCache 機能をインストールします。  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  次のコマンドのいずれかを使用して、コンピューターをホスト型キャッシュサーバーとして構成します。  
  
    -   ドメインに参加していないコンピューターをホスト型キャッシュサーバーとして構成するには、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。  
  
        `Enable-BCHostedServer`  
  
    -   ドメインに参加しているコンピューターをホスト型キャッシュサーバーとして構成し、クライアントコンピューターによるホスト型キャッシュサーバーの自動検出のために Active Directory にサービス接続ポイントを登録するには、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  ホスト型キャッシュサーバーが正しく構成されていることを確認するには、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > このコマンドを実行すると、セクション**HostedCacheServerConfiguration**で、 **HostedCacheServerIsEnabled**の値が**True**になります。 Active Directory にサービス接続ポイント (SCP) を登録するように、ドメインに参加しているホスト型キャッシュサーバーを構成した場合、 **HostedCacheScpRegistrationEnabled**の値は**True**になります。  
  

