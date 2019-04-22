---
title: ホストされたキャッシュ サーバーを展開する (省略可能)
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b19680e933e7a33871816578b63c5a141db0ce00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826213"
---
# <a name="deploy-hosted-cache-servers-optional"></a>ホストされたキャッシュ サーバーを展開する (省略可能)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

インストールして構成する BranchCache ホスト型キャッシュ モードを展開するブランチ オフィスに配置されている BranchCache ホスト型キャッシュ サーバーは、この手順を使用することができます。 Windows Server 2016 での branchcache では、1 つのブランチ オフィス内の複数のホスト型キャッシュ サーバーをデプロイできます。  
  
> [!IMPORTANT]  
> 分散キャッシュ モードでブランチ オフィスでホスト型キャッシュ サーバーのコンピューターが必要ないために、この手順は省略可能です。 予定がない場合は、ブランチ オフィスのキャッシュ モードがホストされているを展開して、ホスト型キャッシュ サーバーを展開する必要はありませんこの手順の手順を実行する必要はありません。  
  
メンバーである必要があります **管理者**, 、またはこの手順を実行に相当します。  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>インストールしてホスト型キャッシュ サーバーを構成するには  
  
1.  をホスト型キャッシュ サーバーとして構成するコンピューターには、BranchCache 機能をインストールする Windows PowerShell プロンプトで次のコマンドを実行します。  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  ホスト型キャッシュ サーバーとしてコンピューターを構成するには、次のコマンドのいずれかを使用します。  
  
    -   ドメイン非参加しているコンピューターでホスト型キャッシュ サーバーとして構成するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
  
        `Enable-BCHostedServer`  
  
    -   ホスト型キャッシュ サーバーとドメイン参加済みコンピューターを構成し、クライアント コンピューターで自動ホスト型キャッシュ サーバーの検出用の Active Directory でサービス接続ポイントを登録するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  ホスト型キャッシュ サーバーの適切な構成を確認し、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > セクションで、このコマンドを実行した後**HostedCacheServerConfiguration**の値は、 **HostedCacheServerIsEnabled**は**True**します。 Active directory での値は、サービス接続ポイント (SCP) を登録するドメイン参加しているホスト型キャッシュ サーバーを構成した場合**HostedCacheScpRegistrationEnabled**は**True**します。  
  

