---
title: "Windows Server Essentials をメンバー サーバーとして追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d09dd82f-f7d2-47ce-862d-fd9869f2021c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8fb73f8186d3984c9e93f7a6e39cb72a54db1e58
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials をメンバー サーバーとして追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このトピックは、Windows Server Essentials エクスペリエンス役割がインストールされていると、Windows Server 2012 R2 Standard、Windows Server 2012 R2 Datacenter、または Windows Server 2016 を実行しているサーバーに適用されます。 このドキュメントの残りの部分で、Windows Server Essentials Experience 役割と呼ばれる Windows Server Essentials します。  
  
> [!NOTE]
>   Windows Server Essentials は、ドメイン コント ローラーとしてのみ展開できます。 このドキュメントでは、Windows Server Essentials では、Windows Server Essentials は含まれません。  
  
 Windows Server Essentials は、Windows ドメイン内でプライマリ サーバーにする必要はありません。 Windows Server Essentials をメンバー サーバーとして既存の Active Directory ドメイン環境に追加し、単純なデータ保護、リモート アクセスのセキュリティ保護、およびクラウド統合機能を利用できます。 さらに、ドメイン コント ローラーをしなくても、既存の Active Directory 環境で Windows Server Essentials を展開できます。 これにより、記憶域を拡張またはローカルの記憶域と管理のブランチ オフィスを使用することができます。  
  
 次のシナリオでは、Windows Server Essentials を追加できます。  
  
-   ブランチ オフィスの場所で Windows Server Essentials を追加し、ネイティブ ツールを使用して別の場所にあるメイン オフィスに配置されているドメイン コント ローラーに参加させます。 このメンバー サーバーでの最適な帯域幅の使用率の BranchCache 機能をオンにすることができます。  
  
-   メンバー サーバー上の他のサーバー フォルダーを追加することで、ネットワーク上の記憶域を拡張するため、Windows Server Essentials ネットワーク内のメンバー サーバーとして Windows Server Essentials を追加します。  
  
-   Windows Server Essentials を実行しているプライマリ サーバーが Microsoft Azure でホストされている場合、ローカル オフィス内のメンバー サーバーとして Windows Server Essentials を追加またはサードパーティ ホストによってホストされています。 帯域幅の使用を最適化するために、ローカル オフィス サイトにより、メンバー サーバーとして Windows Server Essentials が発生します。  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials をメンバー サーバーとして追加する方法  
 Windows Server Essentials をメンバー サーバーとして既存の Active Directory 環境で Windows Server 2012 R2 または Windows Server Essentials を実行しているプライマリ サーバーに追加するには、次の手順を実行する必要があります。  
  
1.  ワークグループに Windows Server Essentials を実行しているサーバーに参加します。  
  
2.  プライマリ Windows Server Essentials サーバーのドメインに Windows Server Essentials を実行しているサーバーに参加します。  
  
3.  Windows Server Essentials Experience サーバー マネージャーからを構成します。  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Windows Server Essentials をワークグループまたはドメインに参加させる  
  
1.  2 番目のサーバーで Windows Server Essentials のインストールを完了した後は、Windows Server Essentials の構成ウィザードを閉じます。  
  
2.  **検索**ボックスに、入力**システム設定**、し、検索結果] をクリックして**システム設定の詳細の表示**します。  
  
3.  **システム プロパティ**、] をクリックして、**コンピューター名**] タブ。  
  
4.  **コンピューター名**で、**ドメイン**セクションで、をクリックして**変更**します。  
  
5.  **コンピューター名/ドメイン名の変更**で、**メンバー**セクションで、選択を Windows Server Essentials を実行しているサーバーに参加するかどうか、**ワークグループ**や、**ドメイン**します。  
  
    -   サーバーをワークグループに追加するに次のように入力します。**ワークグループ**、] をクリックし、 **OK**します。  
  
    -   このサーバーを既存の Active Directory ドメインに参加させる、ドメインの名前を入力し、をクリックして**OK**します。  
  
6.  サーバーを再起動して変更を適用します。  
  
 サーバーは、プライマリ サーバーのドメインに参加させたらは、サーバー マネージャーから Windows Server Essentials の構成ウィザードを実行して Windows Server Essentials の構成を続行することができます。  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>メンバ サーバーで Windows Server Essentials エクスペリエンスを構成するには  
  
1.  (省略可能)必要な場合は、サーバーの名前を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials エクスペリエンスを構成した後、サーバーの名前を変更することはできません。  
  
2.  ドメイン管理者アカウントを使用して、サーバーにサインインします。  
  
3.  サーバー マネージャーを開きます。  
  
4.  フラグ通知領域に**サーバー マネージャー**、フラグをクリックし、[クリックして**Windows Server Essentials の構成**します。  
  
5.  サーバーをメンバー サーバーとして構成することを選択し、をクリックして**次**します。  
  
6.  をクリックして**構成**、構成を開始します。 構成プロセスは、約 10 分です。  
  
7.  デスクトップには、サーバー ダッシュ ボードを起動するダッシュ ボード アイコンをクリックします。 [ホーム] ページで、完了、 **Getting Started**に記載されているタスク、**セットアップ**] タブ。  
  
## <a name="see-also"></a>参照してください。  
  

-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)

-   [Windows Server Essentials をインストールします。](../install/Install-Windows-Server-Essentials.md)

