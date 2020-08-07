---
title: ファイル サーバーを BranchCache ファイル サーバー組織単位に移動する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c44fb11a2935c11474abd3b3cc39cfd0eeb34734
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962346"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイル サーバーを BranchCache ファイル サーバー組織単位に移動する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、Active Directory Domain Services (AD DS) の組織単位 (OU) に BranchCache ファイルサーバーを追加できます。

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

> [!NOTE]
> この手順で OU にコンピューターアカウントを追加する前に、[Active Directory ユーザーとコンピューター] コンソールで BranchCache ファイルサーバー OU を作成する必要があります。 詳細については、「 [BranchCache ファイルサーバーの組織単位を作成](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)する」を参照してください。

### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイルサーバーを BranchCache ファイルサーバーの組織単位に移動するには

1.  AD DS がインストールされているコンピューターのサーバーマネージャーで、[**ツール**] をクリックし、[**ユーザーとコンピューターの Active Directory**] をクリックします。 Active Directory ユーザーとコンピューター] コンソールが開きます。

2.  [Active Directory ユーザーとコンピューター] コンソールで、BranchCache ファイルサーバーのコンピューターアカウントを見つけ、左クリックしてアカウントを選択します。次に、前に作成した BranchCache ファイルサーバー OU にコンピューターアカウントをドラッグアンドドロップします。 たとえば、以前に**branchcache ファイルサーバー**という名前の ou を作成した場合は、コンピューターアカウントを**branchcache ファイルサーバー** OU にドラッグアンドドロップします。

3.  OU に移動するドメイン内の各 BranchCache ファイルサーバーに対して、前の手順を繰り返します。



