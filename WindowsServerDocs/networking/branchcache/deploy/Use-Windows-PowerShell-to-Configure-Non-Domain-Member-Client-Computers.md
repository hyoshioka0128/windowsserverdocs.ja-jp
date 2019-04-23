---
title: Windows PowerShell を使用して、非ドメイン メンバー クライアント コンピューターを構成するには
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9abb77e573d7b3f144ab831c655c81370a4a6af1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839953"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Windows PowerShell を使用して、非ドメイン メンバー クライアント コンピューターを構成するには

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

キャッシュ モードのホストまたは分散キャッシュ モードの BranchCache クライアント コンピューターを手動で構成するこの手順を使用できます。  
  
> [!NOTE]  
> グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、手動でクライアント コンピューターに適用されるポリシーの構成をオーバーライドします。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>BranchCache 分散またはホスト型キャッシュ モードを有効にするには  
  
1.  構成する BranchCache クライアント コンピューターで、管理者として Windows PowerShell を実行し、次のいずれかの操作を行います。  
  
    -   BranchCache 分散キャッシュ モードのクライアント コンピューターを構成するには、次のコマンドを入力し、ENTER キーを押します。  
  
        `Enable-BCDistributed`  
  
    -   BranchCache ホスト型キャッシュ モードのクライアント コンピューターを構成するには、次のコマンドを入力し、ENTER キーを押します。  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > 使用可能なホスト型キャッシュ サーバーを指定する場合を使用して、 `-ServerNames` パラメーターをコンマ区切りのパラメーター値として、ホスト型キャッシュ サーバーの一覧です。 たとえば、HCS1 と HCS2 という 2 つのホスト型キャッシュ サーバーがある場合は、次のコマンドでのホスト型キャッシュ モードのクライアント コンピューターを構成します。  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


