---
title: ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e450b9a2282cb4820b8802aa6d36e822f56ca12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356592"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

Active Directory Domain Services (AD DS) を使用している場合は、ドメイングループポリシーを使用して、複数のファイルサーバーに対して BranchCache ハッシュの発行を有効にすることができます。 これを行うには、組織単位 (OU) を作成し、ファイルサーバーを OU に追加して、BranchCache ハッシュ発行グループポリシーオブジェクト (GPO) を作成し、GPO を構成する必要があります。  
  
複数のファイルサーバーに対してハッシュの発行を有効にするには、次のトピックを参照してください。  
  
-   [BranchCache ファイルサーバーの組織単位を作成する](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [ファイルサーバーを BranchCache ファイルサーバーの組織単位に移動する](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [BranchCache ハッシュパブリケーショングループポリシーオブジェクトを作成する](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  
-   [BranchCache ハッシュ発行グループポリシーオブジェクトを構成する](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  


