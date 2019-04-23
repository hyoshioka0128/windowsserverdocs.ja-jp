---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15e89b961d20b6f14065392553e413374358062d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865433"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この手順を使用すると、BranchCache のハッシュの発行グループ ポリシー オブジェクト (GPO) を作成します。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を実行する前に、BranchCache のファイル サーバー組織単位を作成し、ファイル サーバーを OU に移動する必要があります。 詳細については、次を参照してください。[ドメイン メンバーのファイル サーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)します。  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache のハッシュの発行のグループ ポリシー オブジェクトを作成するには  
  
1.  Windows PowerShell を開き、「 **mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC で、**[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。 **スナップインを追加または** ダイアログ ボックスが表示されます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、 をダブルクリックします**グループ ポリシーの管理**、順にクリックします**OK**します。  
  
4.  グループ ポリシーの管理 MMC では、BranchCache のファイル サーバーを以前に作成した OU にパスを展開します。 たとえば、example.com の名前は、フォレスト、ドメインの名前は、example1.com、および BranchCache ファイル サーバーの名前は、OU 場合、は、次のパスを展開します。**グループ ポリシー管理**、**フォレスト: example.com**、**ドメイン**、 **example1.com**、**ファイル サーバーの BranchCache**します。  
  
5.  右クリック**ファイル サーバーの BranchCache**、 をクリックし、**このドメインに GPO を作成し、リンクする**。 **新しい GPO**  ダイアログ ボックスが表示されます。 **名前**、新しい GPO の名前を入力します。 たとえば、オブジェクトのハッシュの発行を BranchCache に名前を付ける場合は、「**ハッシュ発行を BranchCache**します。 **[OK]** をクリックします。  
  


