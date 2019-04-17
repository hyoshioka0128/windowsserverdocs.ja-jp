---
title: Windows PowerShell を使用して非ドメイン メンバー クライアント コンピューターを構成するには
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a5415d9fa5a4af806f23a1af9c907b1f02e9627b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Windows PowerShell を使用して非ドメイン メンバー クライアント コンピューターを構成するには

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

キャッシュ モードのホストまたは分散キャッシュ モードの BranchCache クライアント コンピューターを手動で構成するこの手順を使用できます。  
  
> [!NOTE]  
> グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、ポリシーが適用されるクライアント コンピューターが手動で構成をオーバーライドします。  
  
メンバーシップ**管理者**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>BranchCache 分散またはホスト型キャッシュ モードを有効にするには  
  
1.  構成する BranchCache クライアント コンピューターで、管理者として Windows PowerShell を実行し、次のいずれかを実行します。  
  
    -   BranchCache 分散キャッシュ モードのクライアント コンピューターを構成するのには、次のコマンドを入力し、し、ENTER キーを押します。  
  
        `Enable-BCDistributed`  
  
    -   BranchCache ホスト型キャッシュ モードのクライアント コンピューターを構成するのには、次のコマンドを入力し、し、ENTER キーを押します。  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > 使用可能なホスト型キャッシュ サーバーを指定する場合は、使用、`-ServerNames`パラメーターをコンマ区切りのパラメーターの値として、ホスト型キャッシュ サーバーの一覧です。 たとえば、HCS1 と HCS2 という 2 つのホスト型キャッシュ サーバーがある場合は、次のコマンドでのホスト型キャッシュ モードのクライアント コンピューターを構成します。  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


