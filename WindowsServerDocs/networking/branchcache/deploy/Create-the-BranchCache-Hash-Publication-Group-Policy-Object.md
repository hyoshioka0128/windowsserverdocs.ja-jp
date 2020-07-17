---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e546705d022bbac2588ace5b3e2c6c807c96da63
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319308"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、BranchCache ハッシュパブリケーショングループポリシーオブジェクト (GPO) を作成できます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を実行する前に、BranchCache ファイルサーバーの組織単位を作成し、ファイルサーバーを OU に移動する必要があります。 詳細については、「 [Enable Hash Publication For Domain Member File Servers](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)」を参照してください。  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュパブリケーショングループポリシーオブジェクトを作成するには  
  
1.  Windows PowerShell を開き、「**mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC の **[ファイル]** メニューで、 **[スナップインの追加と削除]** をクリックします。 **[スナップインの追加と削除]** ダイアログボックスが表示されます。  
  
3.  **[スナップインの追加と削除]** の **[使用できるスナップ**イン] で、 **[グループポリシー管理]** をダブルクリックし、 **[OK]** をクリックします。  
  
4.  [グループポリシー管理] MMC で、前に作成した BranchCache ファイルサーバー OU へのパスを展開します。 たとえば、フォレストに example.com という名前が付けられている場合、ドメインの名前は example1.com であり、OU の名前は BranchCache file servers で、次のパスを展開します:**グループポリシー Management**、 **forest: example.com**、 **Domains**、 **example1.com**、 **BranchCache ファイルサーバー**。  
  
5.  **[BranchCache ファイルサーバー]** を右クリックし、 **[このドメインに GPO を作成し、この場所にリンク]** します をクリックします。 **新しい GPO**  ダイアログ ボックスが表示されます。 **[名前]** に新しい GPO の名前を入力します。 たとえば、BranchCache ハッシュ発行オブジェクトに名前を付ける場合は、「 **Branchcache Hash publication**」と入力します。 **[OK]** をクリックすると、  
  


