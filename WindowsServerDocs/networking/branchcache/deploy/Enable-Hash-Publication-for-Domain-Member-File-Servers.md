---
title: ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: df03945a80ae86aad91a004ea710ac6eff10c3ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971859"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Active Directory Domain Services (AD DS) を使用している場合は、ドメイングループポリシーを使用して、複数のファイルサーバーに対して BranchCache ハッシュの発行を有効にすることができます。 これを行うには、組織単位 (OU) を作成し、ファイルサーバーを OU に追加して、BranchCache ハッシュ発行グループポリシーオブジェクト (GPO) を作成し、GPO を構成する必要があります。

複数のファイルサーバーに対してハッシュの発行を有効にするには、次のトピックを参照してください。

-   [BranchCache ファイル サーバー組織単位を作成する](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [ファイル サーバーを BranchCache ファイル サーバー組織単位に移動する](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)

-   [BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)



