---
title: BranchCache ファイル サーバー組織単位を作成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f058dbec42997f22106666b014508191a8861694
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406484"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>BranchCache ファイル サーバー組織単位を作成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、BranchCache ファイルサーバーの Active Directory Domain Services (AD DS) に組織単位 (OU) を作成できます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>BranchCache ファイルサーバーの組織単位を作成するには  
  
1.  AD DS がインストールされているコンピューターのサーバーマネージャーで、 **[ツール]** をクリックし、 **[ユーザーとコンピューターの Active Directory]** をクリックします。 Active Directory ユーザーとコンピューター コンソールが開きます。  
  
2.  [Active Directory ユーザーとコンピューター] コンソールで、OU を追加するドメインを右クリックします。 たとえば、ドメインに example.com という名前が付いている場合は、 **[example.com]** を右クリックします。 **[新規作成]** をポイントし、 **[組織単位]** をクリックします。 **[新しいオブジェクト-組織単位]** ダイアログボックスが表示されます。  
  
3.  **[新しいオブジェクト-組織単位]** ダイアログボックスの **[名前]** に、新しい OU の名前を入力します。 たとえば、OU BranchCache ファイルサーバーに名前を付ける場合は、「 **branchcache ファイルサーバー**」と入力し、[ **OK]** をクリックします。  
  


