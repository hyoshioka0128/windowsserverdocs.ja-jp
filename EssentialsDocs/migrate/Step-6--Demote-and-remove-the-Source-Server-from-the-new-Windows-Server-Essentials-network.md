---
title: "手順 6: を降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86244c66-2c5e-488d-adb8-112e1ca3e2e1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 24a1f2da2333c7e6854e9efd9d996391d0fcb3b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>手順 6: を降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server Essentials のインストールが完了したら、移行が完了すると、次のタスクを実行する必要があります。  
  
1.  [Active Directory 証明書サービスを削除します。](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)  
  
2.  [移行元サーバーに直接接続されているプリンターを切断します。](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)  
  
3.  [移行元サーバーを降格します。](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)  
  
4.  [削除して、移行元サーバーとして再利用](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)  
  
##  <a name="BKMK_ADCS"></a>Active Directory 証明書サービスを削除します。  
 手順は、1 台のサーバーにインストールされている複数の Active Directory 証明書サービス (AD CS) 役割サービスがある場合は若干異なります。 AD CS 役割サービスをアンインストールし、その他の AD CS 役割サービスを保持する、次の手順を使用することができます。  
  
 この手順を完了するには、証明機関 (CA) をインストールしたユーザーと同じアクセス許可でログオンする必要があります。 エンタープライズ CA をアンインストールする場合は、この手順を完了するために必要な最低限は Enterprise Admins グループまたはそれと同等のメンバーシップです。  
  
#### <a name="to-remove-ad-cs"></a>AD CS を削除するには  
  
1.  移行元サーバーにドメイン管理者としてログオンします。  
  
2.  をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、**サーバー マネージャー**します。  
  
3.  をクリックして**続行**で、**ユーザー アカウント制御**] ダイアログ ボックス。  
  
4.  **役割の概要**セクションで、をクリックして**役割の削除**します。  
  
5.  役割の削除ウィザード] をクリックして**次**します。  
  
6.  クリア、**Active Directory Certificate Services**チェック ボックスをオンにし**次**します。  
  
7.  **削除オプションの確認**] ページで、情報を確認してをクリックして**削除**します。  
  
    > [!NOTE]
    >  インターネット インフォメーション サービス (IIS) が実行されている場合は、続行する前にサービスを停止するように求められます。 をクリックして**OK**します。  
  
    > [!NOTE]
    >  最初に、削除する必要があります**証明機関 Web 登録**がインストールされている場合は、します。  
  
8.  役割の削除ウィザードが完了したら、サーバーを再起動してアンインストール プロセスを完了します。  
  
    > [!IMPORTANT]
    >  そのためには要求されない場合でも、サーバーを再起動します。  
  
##  <a name="BKMK_PhysicallyDisconnect"></a>移行元サーバーに直接接続されているプリンターを切断します。  
 移行元サーバーを降格する前に物理的には、移行元サーバーに直接接続し、移行元サーバーを通して共有されているすべてのプリンターを切断します。 移行元サーバーに直接接続されているプリンターを Active Directory オブジェクトが残っていないことを確認します。 プリンターが直接、移行先サーバーに接続されているし、Windows Server Essentials から共有し、ことができます。  
  
##  <a name="BKMK_DemoteTheSourceServer"></a>移行元サーバーを降格します。  
 AD DS ドメイン コントローラーの役割からドメイン メンバー サーバーの役割を移行元サーバーを降格する前にことを確認するすべてのクライアント コンピューターのグループ ポリシー設定が適用されているように、次の手順で説明されています。  
  
> [!IMPORTANT]
>  クライアント コンピューターでグループ ポリシーの変更が更新されたときに、移行元サーバーと移行先サーバーがネットワークに接続する必要があります。  
  
#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>クライアント コンピューターでグループ ポリシーの更新を強制するには  
  
1.  クライアント コンピューターに管理者としてログオンします。  
  
2.  管理者としてコマンド プロンプト ウィンドウを開きます。  
  
3.  コマンド プロンプトで、次のように入力します。**gpupdate/force**、し、Enter キーを押します。  
  
4.  プロセスは、ログオフし、[完了] をもう一度ログオンする必要があります。 をクリックして**はい**ことを確認します。  
  
 Windows Server Essentials または、以前のバージョンから移行する場合、サーバーを降格するを参照してください[Active Directory Domain Services の削除](https://technet.microsoft.com/library/hh472163.aspx)します。 ワークグループのメンバーとして、移行元サーバーを追加し、ネットワークから切断した後は、移行先サーバーで AD DS から削除する必要があります。  
  
 Windows Server Essentials から移行する場合は、サーバー マネージャーを使用して、それによって、次の手順を使用して、移行元サーバーのドメイン コントローラーを降格、Active Directory ドメイン サービスの役割を削除します。  
  
#### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory から移行元サーバーを削除するには  
  
1.  移行先サーバーで、開く**Active Directory ユーザーとコンピューター**します。  
  
2.  **Active Directory ユーザーとコンピューター**のナビゲーション ウィンドウで、ドメイン名を展開し、展開**コンピューター**します。  
  
3.  サーバーの一覧で、移行元サーバーがまだ存在する場合は、移行元サーバーの名前を右クリックし、] をクリックして**削除**、] をクリックし、**はい**します。  
  
4.  いないことを確認、移行元サーバーの一覧とし、[閉じる**Active Directory ユーザーとコンピューター**します。  
  
##  <a name="BKMK_RemoveTheSourceServer"></a>削除して、移行元サーバーとして再利用  
 移行元サーバーをオフにして、ネットワークから切断します。 移行元サーバーを移行先サーバーに必要なすべてのデータが移行されたことを確認するには、少なくとも 1 週間を再フォーマットしないことをお勧めします。 すべてのデータが移行されたことを確認したら、再インストールできますこのサーバー、ネットワーク上、他のタスクのセカンダリ サーバーとして必要な場合です。  
  
> [!NOTE]
>  降格して、移行元サーバーを削除した後は、移行先サーバーを再起動します。  
  
 移行元サーバーを降格した後は、正常な状態 移行元サーバーの用途を変更する場合は、最も簡単な方法が、再フォーマットし、サーバーのオペレーティング システムをインストールし、その他のサーバーとして使用するために設定します。  
  
## <a name="next-steps"></a>次の手順  
 降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除します。 移動できるようになりました[手順 7: Windows Server Essentials 移行の移行後のタスクを実行](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)します。  
  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

