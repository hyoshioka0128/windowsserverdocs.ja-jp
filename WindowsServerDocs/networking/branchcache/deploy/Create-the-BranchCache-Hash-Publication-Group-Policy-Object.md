---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4510d13c806adc2db46dfccce02a5a1b2814a2c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache ハッシュ発行グループ ポリシー オブジェクト (GPO) を作成します。  
  
メンバーシップ**Domain Admins**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> この手順を実行する前に、BranchCache ファイル サーバー組織単位を作成して、ファイル サーバーを OU に移動する必要があります。 詳細については、次を参照してください。[ドメイン メンバー ファイル サーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)します。  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成するには  
  
1.  Windows PowerShell を開き、「**mmc**、し、Enter キーを押します。 Microsoft 管理コンソール (MMC) を開きます。  
  
2.  MMC で、上、**ファイル**] メニューのをクリックして**スナップインの追加/削除**します。 **スナップインを追加または**] ダイアログ ボックスが開きます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、] をダブルクリック**グループ ポリシーの管理**、] をクリックし、**OK**します。  
  
4.  グループ ポリシーの管理] を BranchCache ファイル サーバーに以前に作成した OU のパスを展開します。 たとえば、example.com の名前は、フォレスト、ドメインの名前は example1.com、および BranchCache ファイル サーバーの名前は、OU 場合、は、次のパスを展開します。**グループ ポリシーの管理**、**フォレスト: example.com**、**ドメイン**、**example1.com**、**BranchCache ファイル サーバー**します。  
  
5.  右クリック**BranchCache ファイル サーバー**、] をクリックし、**このドメインに GPO を作成し、次のとおりにリンクする**します。 **新しい GPO** ] ダイアログ ボックスが開きます。 **名**、新しい GPO の名前を入力します。 たとえば、BranchCache のハッシュの発行、オブジェクトの名前を付ける場合は、入力**BranchCache のハッシュの発行**します。 をクリックして**OK**します。  
  


