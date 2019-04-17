---
title: BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6f528c9f0a8a39b286ad7ac4fa728d93c311f779
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、BranchCache ハッシュ発行グループ ポリシー オブジェクト (GPO) の構成を OU に追加したすべてのファイル サーバーがある、同じハッシュの発行ポリシー設定を適用できるようにします。  
  
メンバーシップ**Domain Admins**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> この手順を実行する前に ou、ファイル サーバーに移動する BranchCache ファイル サーバー組織単位を作成する必要があり、BranchCache のハッシュの発行 GPO を作成します。 詳細については、次を参照してください。[ドメイン メンバー ファイル サーバーのハッシュの発行を有効にする](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)します。  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache ハッシュ発行グループ ポリシー オブジェクトを構成するには  
  
1.  Windows PowerShell の種類、管理者として実行**mmc**、し、ENTER キーを押します。 Microsoft 管理コンソール (MMC) を開きます。  
  
2.  MMC で、上、**ファイル**] メニューのをクリックして**スナップインの追加/削除**します。 **スナップインを追加または**] ダイアログ ボックスが開きます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、] をダブルクリック**グループ ポリシーの管理**、] をクリックし、**OK**します。  
  
4.  グループ ポリシーの管理] では、BranchCache のハッシュの発行以前に作成した GPO にパスを展開します。 たとえば、フォレストが example.com という名前の場合、ドメインは、という名前 example1.com、GPO の名前は**BranchCache のハッシュの発行**、次のパスを展開:**グループ ポリシーの管理**、**フォレスト: example.com**、**ドメイン**、 **example1.com**、**グループ ポリシー オブジェクト**、 **BranchCache のハッシュの発行**します。  
  
5.  右クリックし、 **BranchCache のハッシュの発行**GPO とクリック**編集**します。 グループ ポリシー管理エディター コンソールが開きます。  
  
6.  グループ ポリシー管理エディター コンソールで、次のパスを展開します。**コンピューターの構成**、**ポリシー**、**管理用テンプレート**、**ネットワーク**、 **Lanman サーバー**します。  
  
7.  グループ ポリシー管理エディター コンソールで [ **Lanman サーバー**します。 詳細ウィンドウでダブルクリック**BranchCache のハッシュの発行**します。 **BranchCache のハッシュの発行**] ダイアログ ボックスが開きます。  
  
8.  **BranchCache のハッシュの発行**ダイアログ ボックスで、をクリックして**有効**します。  
  
9. **オプション**、] をクリックして**すべての共有フォルダーのハッシュの発行を許可する**、し、次のいずれかをクリックします。  
  
    1.  すべての OU に追加したサーバーのファイルをすべての共有フォルダーのハッシュの発行を有効にする] をクリックして**すべての共有フォルダーのハッシュの発行を許可する**します。  
  
    2.  ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを有効にする] をクリックして**ハッシュの発行を BranchCache が有効になっている共有フォルダーに対してのみを許可する**します。  
  
    3.  ファイル共有の BranchCache が有効になっている場合でも、すべての共有、コンピューター上のフォルダーのハッシュの発行を許可しないように、] をクリックして**ハッシュの発行をすべての共有フォルダーで許可しない**します。  
  
10. をクリックして**OK**します。  
  
> [!NOTE]  
> ほとんどの場合、MMC コンソールを保存し、対して行った構成の変更を表示するビューを更新し必要があります。  
  


