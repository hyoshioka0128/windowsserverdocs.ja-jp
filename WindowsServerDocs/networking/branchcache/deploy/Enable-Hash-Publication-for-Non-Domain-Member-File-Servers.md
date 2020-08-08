---
title: 非ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 80c65b20dcbae89ecccb67af22e3f569cd0d5c31
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969659"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>非ドメイン メンバー ファイル サーバーでハッシュの発行を有効にする

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、Windows Server 2016 を実行しているファイルサーバーで、ファイルサービスサーバーの役割がインストールされている**ネットワークファイル用 branchcache**役割サービスを使用して、ローカルコンピューターグループポリシーを使用して BranchCache のハッシュの発行を構成できます。

この手順は、ドメインメンバー以外のファイルサーバーでの使用を目的としています。 ドメインメンバーファイルサーバーでこの手順を実行し、ドメイングループポリシーを使用して BranchCache を構成した場合、ドメイングループポリシーの設定はローカルのグループポリシー設定よりも優先されます。

この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

> [!NOTE]
> 1つ以上のドメインメンバーファイルサーバーがある場合は、それらを Active Directory Domain Services の組織単位 (OU) に追加し、グループポリシーを使用して、各ファイルサーバーを個別に構成するのではなく、一度にすべてのファイルサーバーに対してハッシュの発行を構成することができます。 詳細については、「 [Enable Hash Publication For Domain Member File Servers](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)」を参照してください。

### <a name="to-enable-hash-publication-for-one-file-server"></a>1つのファイルサーバーでハッシュの発行を有効にするには

1.  Windows PowerShell を開き、「**mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。

2.  MMC の **[ファイル]** メニューで、**[スナップインの追加と削除]** をクリックします。 [**スナップインの追加と削除**] ダイアログボックスが表示されます。

3.  [**スナップインの追加と削除**] の [**使用できるスナップ**イン] で、[**グループポリシーオブジェクトエディター**] をダブルクリックします。 [ローカルコンピューター] オブジェクトが選択された状態で、グループポリシーウィザードが開きます。 **[完了]** をクリックし、**[OK]** をクリックします。

4.  ローカルグループポリシーエディター MMC で、[**ローカルコンピューターポリシー**]、[**コンピューターの構成**]、[**管理用テンプレート**]、[**ネットワーク**]、[ **Lanman サーバー**] の順に展開します。 [ **Lanman サーバー**] をクリックします。

5.  詳細ウィンドウで、[ **BranchCache のハッシュの発行**] をダブルクリックします。 [ **BranchCache のハッシュの発行**] ダイアログボックスが開きます。

6.  [ **BranchCache のハッシュの発行**] ダイアログボックスで、[**有効**] をクリックします。

7.  [**オプション**] で、[**すべての共有フォルダーに対してハッシュの発行を許可する**] をクリックし、次のいずれかをクリックします。

    1.  このコンピューター上のすべての共有フォルダーに対してハッシュの発行を有効にするには、[**すべての共有フォルダーでハッシュの発行を許可**する] をクリックします。

    2.  BranchCache が有効になっている共有フォルダーに対してのみハッシュの発行を有効にするには、[ **branchcache が有効になっている共有フォルダーに対してのみハッシュの発行を許可**する] をクリックします。

    3.  ファイル共有で BranchCache が有効になっている場合でも、コンピューター上のすべての共有フォルダーでハッシュの発行を許可しない場合は、[**すべての共有フォルダーでハッシュの発行を許可**しない] をクリックします。

8.  **[OK]** をクリックします。



