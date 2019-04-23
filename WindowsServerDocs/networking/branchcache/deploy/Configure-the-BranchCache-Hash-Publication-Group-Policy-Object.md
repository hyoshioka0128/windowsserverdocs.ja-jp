---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6e9a338dfebfb1dfadb258bcbdfcc8d75bd3ea86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862963"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この手順を使用するには、OU に追加したすべてのファイル サーバーがそれらに適用される同じハッシュ パブリケーション ポリシー設定を使用できるように、BranchCache のハッシュの発行グループ ポリシー オブジェクト (GPO) を構成します。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を実行する前に OU、ファイル サーバーに移動 BranchCache ファイル サーバーの組織単位を作成する必要があり、BranchCache のハッシュの発行の GPO を作成します。 詳細については、次を参照してください。[ドメイン メンバーのファイル サーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)します。  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache のハッシュの発行のグループ ポリシー オブジェクトを構成するには  
  
1.  管理者は、種類として Windows PowerShell を実行**mmc**、し、ENTER キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC で、**[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。 **スナップインを追加または** ダイアログ ボックスが表示されます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、 をダブルクリックします**グループ ポリシーの管理**、順にクリックします**OK**します。  
  
4.  グループ ポリシーの管理 MMC では、BranchCache のハッシュの発行前に作成した GPO にパスを展開します。 たとえば、example.com、フォレストの名前が場合、ドメインの名前は、example1.com、し、GPO の名前は**ハッシュの発行を BranchCache**、順に展開します。**グループ ポリシー管理**、**フォレスト: example.com**、**ドメイン**、 **example1.com**、**グループ ポリシー オブジェクト**、 **BranchCache のハッシュの発行**します。  
  
5.  右クリックし、**ハッシュの発行を BranchCache** GPO とクリック**編集**。 グループ ポリシー管理エディター コンソールを開きます。  
  
6.  グループ ポリシー管理エディター コンソールでは、次のパスを展開します。**コンピューターの構成**、**ポリシー**、**管理用テンプレート**、**ネットワーク**、 **Lanman Server**します。  
  
7.  グループ ポリシー管理エディター コンソールで、クリックして**Lanman Server**します。 詳細ウィンドウでダブルクリック**BranchCache のハッシュの発行**します。 **BranchCache のハッシュの発行** ダイアログ ボックスが表示されます。  
  
8.  **BranchCache のハッシュの発行**ダイアログ ボックスで、をクリックして**有効**します。  
  
9. **オプション**、 をクリックして**すべての共有フォルダーのハッシュの発行を許可する**、次のいずれかをクリックします。  
  
    1.  すべてのファイルの OU に追加したサーバーのすべての共有フォルダーのハッシュの発行を有効にするには、**すべての共有フォルダーのハッシュの発行を許可する**します。  
  
    2.  ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを有効にするには、**ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを許可する**します。  
  
    3.  ファイル共有の BranchCache が有効になっている場合でも、すべての共有、コンピューター上のフォルダーには、ハッシュの発行を許可しないかをクリックします。**ハッシュの発行をすべての共有フォルダーで許可しないように**します。  
  
10. **[OK]** をクリックします。  
  
> [!NOTE]  
> ほとんどの場合では、MMC コンソールを保存して、行った構成の変更を表示するビューを更新する必要があります。  
  


