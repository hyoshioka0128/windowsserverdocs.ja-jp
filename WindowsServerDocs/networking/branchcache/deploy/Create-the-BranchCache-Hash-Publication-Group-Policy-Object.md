---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ade42b3ff690e3c813c750609fb0b21b9999a85f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971879"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、BranchCache ハッシュパブリケーショングループポリシーオブジェクト (GPO) を作成できます。

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

> [!NOTE]
> この手順を実行する前に、BranchCache ファイルサーバーの組織単位を作成し、ファイルサーバーを OU に移動する必要があります。 詳細については、「 [Enable Hash Publication For Domain Member File Servers](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)」を参照してください。

### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュパブリケーショングループポリシーオブジェクトを作成するには

1.  Windows PowerShell を開き、「**mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。

2.  MMC の **[ファイル]** メニューで、**[スナップインの追加と削除]** をクリックします。 [**スナップインの追加と削除**] ダイアログボックスが表示されます。

3.  [**スナップインの追加と削除**] の **[使用できるスナップ**イン] で、[**グループポリシー管理**] をダブルクリックし、[ **OK**] をクリックします。

4.  [グループポリシー管理] MMC で、前に作成した BranchCache ファイルサーバー OU へのパスを展開します。 たとえば、フォレストに example.com という名前が付けられている場合、ドメインの名前は example1.com であり、OU の名前は BranchCache file servers で、次のパスを展開します:**グループポリシー Management**、 **forest: example.com**、 **Domains**、 **example1.com**、 **BranchCache ファイルサーバー**。

5.  [ **BranchCache ファイルサーバー**] を右クリックし、[**このドメインに GPO を作成し、この場所にリンク**します] をクリックします。 **新しい GPO** ] ダイアログ ボックスが表示されます。 [**名前**] に新しい GPO の名前を入力します。 たとえば、BranchCache ハッシュ発行オブジェクトに名前を付ける場合は、「 **Branchcache Hash publication**」と入力します。 **[OK]** をクリックします。



