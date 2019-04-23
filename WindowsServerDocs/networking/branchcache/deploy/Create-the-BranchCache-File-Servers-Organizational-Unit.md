---
title: BranchCache ファイル サーバー組織単位を作成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b7b26ec5808f5b11141e81dc5e738c83c94ef6b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874083"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>BranchCache ファイル サーバー組織単位を作成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Active Directory ドメイン サービス (AD DS) のファイル サーバーの BranchCache で、組織単位 (OU) を作成するのにこの手順を使用することができます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>BranchCache のファイル サーバー組織単位を作成するには  
  
1.  AD DS がインストールされている、サーバー マネージャーで、コンピューターで次のようにクリックします。**ツール**、 をクリックし、 **Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。  
  
2.  Active Directory ユーザーとコンピューター コンソールで、OU を追加するドメインを右クリックします。 たとえば場合は、ドメインが example.com という名前を右クリックして**example.com**します。 **[新規作成]** をポイントし、**[組織単位]** をクリックします。 **新しいオブジェクト - 組織単位** ダイアログ ボックスが表示されます。  
  
3.  **新しいオブジェクト - 組織単位** ダイアログ ボックスで**名前**、新しい OU の名前を入力します。 たとえば、OU の BranchCache のファイル サーバーの名前を付ける場合は、「**ファイル サーバーの BranchCache**順にクリックします**OK**します。  
  


