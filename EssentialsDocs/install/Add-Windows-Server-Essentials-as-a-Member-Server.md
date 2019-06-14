---
title: Windows Server Essentials をメンバー サーバーとして追加
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: 502e54cf719895dd11030cf163159f6cdda47164
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433731"
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials をメンバー サーバーとして追加

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 Standard、Windows Server 2012 R2 Datacenter、または Windows Server 2016 を実行するサーバーに適用されます。 このドキュメントの残りの部分では、Windows Server Essentials Experience 役割を Windows Server Essentials と呼んでいます。  
  
> [!NOTE]
>   Windows Server Essentials は、ドメイン コント ローラーとしてのみデプロイできます。 このドキュメントでは、Windows Server Essentials には Windows Server Essentials は含まれません。  
  
 Windows Server Essentials は、Windows ドメイン内でプライマリ サーバーになる必要はありません。 Windows Server Essentials をメンバー サーバーとして、既存の Active Directory ドメイン環境に追加し、その簡単なデータ保護、セキュリティ保護されたリモート アクセス、およびクラウド統合機能を利用できます。 さらに、Windows Server Essentials はドメイン コントローラーになる必要なく、既存の Active Directory 環境に展開できます。 これにより、ローカル記憶域と管理のために、記憶域を拡張したり、ブランチ オフィスを使用したりすることができます。  
  
 次のシナリオで、Windows Server Essentials を追加できます。  
  
-   ネイティブ ツールを使用して、Windows Server Essentials をブランチ オフィスの場所に追加し、別の場所にあるメイン オフィスに置かれているドメイン コントローラーに参加させます。 このメンバー サーバーで、最適な帯域幅使用のための BranchCache 機能を有効にすることができます。  
  
-   Windows Server Essentials をメンバー サーバーで追加のサーバー フォルダーを追加することで、ネットワーク上の記憶域の拡張に役立つ Windows Server Essentials ネットワーク内のメンバー サーバーとして追加します。  
  
-   Windows Server Essentials を実行しているプライマリ サーバーが Microsoft Azure でホストされている場合は、ローカル オフィス内のメンバー サーバーとして Windows Server Essentials を追加またはサードパーティ ホストによってホストされています。 ローカル オフィス サイトで、メンバー サーバーとして Windows Server Essentials を使用すると、帯域幅の使用を最適化するために役立ちます。  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials のメンバー サーバーとしての追加  
 Windows Server Essentials をメンバー サーバーとして既存の Active Directory 環境で Windows Server 2012 R2 または Windows Server Essentials を実行するプライマリ サーバーに追加するには、次の手順を行う必要があります。  
  
1.  Windows Server Essentials を実行するサーバーをワークグループに参加させます。  
  
2.  プライマリの Windows Server Essentials サーバーのドメインに Windows Server Essentials を実行しているサーバーを参加させます。  
  
3.  Windows Server Essentials Experience サーバー マネージャーを構成します。  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Windows Server Essentials をワークグループまたはドメインに参加させるには  
  
1. 2 台目のサーバーへの Windows Server Essentials のインストールが完了したら、Windows Server Essentials の構成ウィザードを閉じます。  
  
2. **検索** ボックスに **System Settings** と入力し、検索結果で **システムの詳細設定の表示** をクリックします。  
  
3. **[システムのプロパティ]** で、 **[コンピューター名]** タブをクリックします。  
  
4. **[コンピューター名]** の **[ドメイン]** セクションで **[変更]** をクリックします。  
  
5. **コンピューター名/ドメイン名変更**の**メンバー**セクションで、Windows Server Essentials を実行しているサーバーに参加させるかを選択、**ワークグループ**または、 **ドメイン**します。  
  
   -   サーバーをワークグループに追加するには、「 **workgroup**」と入力し、 **[OK]** をクリックします。  
  
   -   このサーバーを既存の Active Directory ドメインに参加させるには、ドメインの名前を入力して、 **[OK]** をクリックします。  
  
6. サーバーを再起動して、変更を適用します。  
  
   サーバーは、プライマリ サーバーのドメインに参加させたら、サーバー マネージャーから Windows Server Essentials の構成ウィザードを実行して、Windows Server Essentials を構成することもできます。  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>メンバー サーバーで Windows Server Essentials エクスペリエンスを構成するには  
  
1.  (省略可能) 必要に応じて、サーバー名を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials エクスペリエンスを構成した後、サーバー名を変更することはできません。  
  
2.  ドメイン管理者アカウントを使用して、サーバーにサインインします。  
  
3.  サーバー マネージャーを開きます。  
  
4.  **サーバー マネージャー**のフラグ通知領域で、フラグをクリックし、 **[Windows Server Essentials の構成]** をクリックします。  
  
5.  サーバーをメンバー サーバーとして構成することを選択して、 **[次へ]** をクリックします。  
  
6.  **[構成]** をクリックして、構成を開始します。 構成プロセスが完了するまで、約 10 分かかります。  
  
7.  デスクトップで、ダッシュボード アイコンをクリックし、サーバーを起動します。 ホーム ページで、 **[セットアップ]** タブに示されている **[作業の開始]** タスクを実行します。  
  
## <a name="see-also"></a>関連項目  
  

-   [Windows Server Essentials のインストール](Install-Windows-Server-Essentials.md)

-   [Windows Server Essentials のインストール](../install/Install-Windows-Server-Essentials.md)

