---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bae0d3dff22205f3311020e233a26835527186f5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406495"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、OU に追加したすべてのファイルサーバーに同じハッシュ発行ポリシー設定が適用されるように、BranchCache ハッシュ発行グループポリシーオブジェクト (GPO) を構成できます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を実行する前に、BranchCache ファイルサーバーの組織単位を作成し、ファイルサーバーを OU に移動して、BranchCache ハッシュ発行の GPO を作成する必要があります。 詳細については、「 [ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)」を参照してください。  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループポリシーオブジェクトを構成するには  
  
1.  管理者として Windows PowerShell を実行し、「 **mmc**」と入力して、enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC で、 **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。 **[スナップインの追加と削除]** ダイアログボックスが表示されます。  
  
3.  **[スナップインの追加と削除]** の **[使用できるスナップ**イン] で、 **[グループポリシー管理]** をダブルクリックし、 **[OK]** をクリックします。  
  
4.  [グループポリシー管理] MMC で、前に作成した BranchCache ハッシュ発行 GPO のパスを展開します。 たとえば、フォレストに example.com という名前が付けられている場合、ドメインの名前は example1.com で、GPO の名前は**BranchCache Hash Publication**で、次のパスを展開します。**グループポリシー管理**、**フォレスト: example.com**、**ドメイン**、 **example1.com**、**グループポリシーオブジェクト**、 **BranchCache ハッシュの発行**。  
  
5.  **[BranchCache ハッシュパブリケーション]** GPO を右クリックし、 **[編集]** をクリックします。 グループポリシー管理エディターコンソールが開きます。  
  
6.  グループポリシー管理エディターコンソールで、次のパスを展開します。**コンピューターの構成**、**ポリシー**、**管理用テンプレート**、**ネットワーク**、 **Lanman サーバー**。  
  
7.  グループポリシー管理エディターコンソールで、 **[Lanman サーバー]** をクリックします。 詳細ウィンドウで、 **[BranchCache のハッシュの発行]** をダブルクリックします。 **[BranchCache のハッシュの発行]** ダイアログボックスが開きます。  
  
8.  **[BranchCache のハッシュの発行]** ダイアログボックスで、 **[有効]** をクリックします。  
  
9. **[オプション]** で、 **[すべての共有フォルダーに対してハッシュの発行を許可する]** をクリックし、次のいずれかをクリックします。  
  
    1.  OU に追加したすべてのファイルサーバーのすべての共有フォルダーに対してハッシュの発行を有効にするには、[**すべての共有フォルダーでハッシュの発行を許可**する] をクリックします。  
  
    2.  BranchCache が有効になっている共有フォルダーに対してのみハッシュの発行を有効にするには、[ **branchcache が有効になっている共有フォルダーに対してのみハッシュの発行を許可**する] をクリックします。  
  
    3.  ファイル共有で BranchCache が有効になっている場合でも、コンピューター上のすべての共有フォルダーでハッシュの発行を許可しない場合は、[**すべての共有フォルダーでハッシュの発行を許可**しない] をクリックします。  
  
10. **[OK]** をクリックします。  
  
> [!NOTE]  
> ほとんどの場合、構成の変更を表示するには、MMC コンソールを保存し、表示を更新する必要があります。  
  


