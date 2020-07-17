---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 660a4979aa5e29a6dd22cb2e0e6659966d077a8e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319335"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、OU に追加したすべてのファイルサーバーに同じハッシュ発行ポリシー設定が適用されるように、BranchCache ハッシュ発行グループポリシーオブジェクト (GPO) を構成できます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を実行する前に、BranchCache ファイルサーバーの組織単位を作成し、ファイルサーバーを OU に移動して、BranchCache ハッシュ発行の GPO を作成する必要があります。 詳細については、「 [Enable Hash Publication For Domain Member File Servers](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)」を参照してください。  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループポリシーオブジェクトを構成するには  
  
1.  管理者として Windows PowerShell を実行し、「 **mmc**」と入力して、enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC の **[ファイル]** メニューで、 **[スナップインの追加と削除]** をクリックします。 **[スナップインの追加と削除]** ダイアログボックスが表示されます。  
  
3.  **[スナップインの追加と削除]** の **[使用できるスナップ**イン] で、 **[グループポリシー管理]** をダブルクリックし、 **[OK]** をクリックします。  
  
4.  [グループポリシー管理] MMC で、前に作成した BranchCache ハッシュ発行 GPO のパスを展開します。 たとえば、フォレストに example.com という名前が付けられている場合、ドメインの名前は example1.com で、GPO の名前は**Branchcache Hash publication**で、次のパスを展開します。**グループポリシー管理**、**フォレスト: example.com**、**ドメイン**、 **example1.com**、**グループポリシーオブジェクト**、 **BranchCache ハッシュの発行**。  
  
5.  **[BranchCache ハッシュパブリケーション]** GPO を右クリックし、 **[編集]** をクリックします。 グループポリシー管理エディターコンソールが開きます。  
  
6.  グループポリシー管理エディターコンソールで、 **[コンピューターの構成]** 、 **[ポリシー]** 、 **[管理用テンプレート]** 、 **[ネットワーク]** 、 **[Lanman サーバー]** の順に展開します。  
  
7.  グループポリシー管理エディターコンソールで、 **[Lanman サーバー]** をクリックします。 詳細ウィンドウで、 **[BranchCache のハッシュの発行]** をダブルクリックします。 **[BranchCache のハッシュの発行]** ダイアログボックスが開きます。  
  
8.  **[BranchCache のハッシュの発行]** ダイアログボックスで、 **[有効]** をクリックします。  
  
9. **[オプション]** で、 **[すべての共有フォルダーに対してハッシュの発行を許可する]** をクリックし、次のいずれかをクリックします。  
  
    1.  OU に追加したすべてのファイルサーバーのすべての共有フォルダーに対してハッシュの発行を有効にするには、[**すべての共有フォルダーでハッシュの発行を許可**する] をクリックします。  
  
    2.  BranchCache が有効になっている共有フォルダーに対してのみハッシュの発行を有効にするには、[ **branchcache が有効になっている共有フォルダーに対してのみハッシュの発行を許可**する] をクリックします。  
  
    3.  ファイル共有で BranchCache が有効になっている場合でも、コンピューター上のすべての共有フォルダーでハッシュの発行を許可しない場合は、[**すべての共有フォルダーでハッシュの発行を許可**しない] をクリックします。  
  
10. **[OK]** をクリックすると、  
  
> [!NOTE]  
> ほとんどの場合、構成の変更を表示するには、MMC コンソールを保存し、表示を更新する必要があります。  
  


