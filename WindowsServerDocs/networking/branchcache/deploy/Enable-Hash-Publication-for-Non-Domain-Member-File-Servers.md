---
title: 非ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00be97abbd583e4c5e762775ea563ba0720d5142
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814953"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>非ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 を実行しているファイル サーバーでローカル コンピューターのグループ ポリシーを使用して BranchCache のハッシュの発行を構成するこの手順を使用することができます、**ネットワーク ファイル用 BranchCache**ファイル サービスの役割サービスサーバーの役割がインストールされています。  
  
この手順は、非ドメイン メンバーのファイル サーバー上の使用を対象としています。 ドメイン メンバーのファイル サーバーにこの手順を実行して、ドメイン グループ ポリシーを使用して BranchCache を構成することも場合、ドメインのグループ ポリシー設定は、ローカル グループ ポリシー設定をオーバーライドします。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 1 つまたは複数のドメインのメンバー ファイル サーバーがある場合は、Active Directory Domain Services では、組織単位 (OU) に追加し、グループ ポリシーを使用して個別に構成するのではなくハッシュの発行のすべてのファイル サーバーを一度に 1 つを構成するには各ファイル サーバー。 詳細については、次を参照してください。[ドメイン メンバーのファイル サーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)します。  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>1 つのファイル サーバーのハッシュの発行を有効にするには  
  
1.  Windows PowerShell を開き、「 **mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC で、**[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。 **スナップインを追加または** ダイアログ ボックスが表示されます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、ダブルクリックして**グループ ポリシー オブジェクト エディター**します。 ローカル コンピューター オブジェクトを選択したグループ ポリシー ウィザードを開きます。 **[完了]** をクリックし、**[OK]** をクリックします。  
  
4.  ローカル グループ ポリシー エディター mmc で、次のパスを展開します。**ローカル コンピューター ポリシー**、**コンピューターの構成**、**管理用テンプレート**、**ネットワーク**、 **Lanman Server**します。 クリックして**Lanman Server**します。  
  
5.  詳細ウィンドウでダブルクリック**BranchCache のハッシュの発行**します。 **BranchCache のハッシュの発行** ダイアログ ボックスが表示されます。  
  
6.  **BranchCache のハッシュの発行**ダイアログ ボックスで、をクリックして**有効**します。  
  
7.  **オプション**、 をクリックして**すべての共有フォルダーのハッシュの発行を許可する**、次のいずれかをクリックします。  
  
    1.  このコンピューター上のすべての共有フォルダーのハッシュの発行を有効にするには、**すべての共有フォルダーのハッシュの発行を許可する**します。  
  
    2.  ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを有効にするには、**ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを許可する**します。  
  
    3.  ファイル共有の BranchCache が有効になっている場合でも、すべての共有、コンピューター上のフォルダーには、ハッシュの発行を許可しないかをクリックします。**ハッシュの発行をすべての共有フォルダーで許可しないように**します。  
  
8.  **[OK]** をクリックします。  
  


