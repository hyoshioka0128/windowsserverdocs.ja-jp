---
title: Windows PowerShell を使用して、非ドメイン メンバー クライアント コンピューターを構成するには
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 57fbe66168ccf1db5f4136d805206036405b3848
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964298"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Windows PowerShell を使用して、非ドメイン メンバー クライアント コンピューターを構成するには

>適用先:Windows Server (半期チャネル)、Windows Server 2016

キャッシュ モードのホストまたは分散キャッシュ モードの BranchCache クライアント コンピューターを手動で構成するこの手順を使用できます。

> [!NOTE]
> グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、手動でクライアント コンピューターに適用されるポリシーの構成をオーバーライドします。

この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

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



