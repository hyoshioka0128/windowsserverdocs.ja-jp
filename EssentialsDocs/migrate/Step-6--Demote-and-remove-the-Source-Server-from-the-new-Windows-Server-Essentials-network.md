---
title: '手順 6: 移行元サーバーを降格して新しい Windows Server Essentials ネットワークから削除する'
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86244c66-2c5e-488d-adb8-112e1ca3e2e1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3df8b2901ca2ca3d38066c592aaeb326d7471ba0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318735"
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>手順 6: 移行元サーバーを降格して新しい Windows Server Essentials ネットワークから削除する

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials のインストールが完了し、移行が完了したら、次のタスクを実行する必要があります。  
  
1.  [Active Directory 証明書サービスの削除](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)  
  
2.  [移行元サーバーに直接接続されているプリンターを切断する](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)  
  
3.  [移行元サーバーを降格する](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)  
  
4.  [移行元サーバーの削除と転用](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)  
  
##  <a name="remove-active-directory-certificate-services"></a><a name="BKMK_ADCS"></a>Active Directory 証明書サービスの削除  
 複数の Active Directory 証明書サービス (AD CS) の役割サービスが 1 台のサーバーにインストールされている場合、手順は若干異なります。 以下の手順を使用すると、1 つの AD CS 役割サービスをアンインストールし、他の AD CS 役割サービスは残しておくことができます。  
  
 この手順を完了するには、証明機関 (CA) をインストールしたユーザーと同じアクセス許可でログオンする必要があります。 エンタープライズ CA をアンインストールする場合、この手順を実行するための最小要件は、Enterprise Admins のメンバーシップまたはそれと同等のものです。  
  
#### <a name="to-remove-ad-cs"></a>AD CS を削除するには  
  
1.  移行元サーバーにドメイン管理者としてログオンします。  
  
2.  **[スタート]** 、 **[管理ツール]** 、 **[サーバー マネージャー]** の順にクリックします。  
  
3.  **[ユーザー アカウント制御]** ダイアログ ボックスの **[続行]** をクリックします。  
  
4.  **[役割の概要]** セクションで、 **[役割の削除]** をクリックします。  
  
5.  役割の削除ウィザードで、 **[次へ]** をクリックします。  
  
6.  **[Active Directory 証明書サービス]** チェック ボックスをオフにして、 **[次へ]** をクリックします。  
  
7.  **[削除オプションの確認]** ページで、情報を確認し、 **[削除]** をクリックします。  
  
    > [!NOTE]
    >  インターネット インフォメーション サービス (IIS) が実行中の場合は、続行する前にサービスを停止するよう求められます。 **[OK]** をクリックすると、  
  
    > [!NOTE]
    >  **[証明機関 Web 登録]** がインストールされている場合、最初に削除する必要がある場合があります。  
  
8.  役割の削除ウィザードが終了したら、サーバーを再起動してアンインストール プロセスを完了します。  
  
    > [!IMPORTANT]
    >  そうするように要求されない場合でも、サーバーを再起動します。  
  
##  <a name="disconnect-printers-that-are-directly-connected-to-the-source-server"></a><a name="BKMK_PhysicallyDisconnect"></a>移行元サーバーに直接接続されているプリンターを切断する  
 移行元サーバーを降格する前に、移行元サーバーに直接接続されていて、移行元サーバーを通して共有されているすべてのプリンターを、物理的に切断します。 移行元サーバーに直接接続されていたプリンターの Active Directory オブジェクトが残っていないことを確認します。 その後、プリンターを移行先サーバーに直接接続し、Windows Server Essentials から共有することができます。  
  
##  <a name="demote-the-source-server"></a><a name="BKMK_DemoteTheSourceServer"></a>移行元サーバーを降格する  
 移行元サーバーを AD DS ドメイン コントローラーの役割からドメイン メンバー サーバーの役割に降格する前に、以下の手順で説明されているように、グループ ポリシーの設定がすべてのクライアント コンピューターに適用されていることを確認します。  
  
> [!IMPORTANT]
>  クライアント コンピューターでグループ ポリシーの変更が更新されている間、移行元サーバーと移行先サーバーはネットワークに接続されている必要があります。  
  
#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>クライアント コンピューターでグループ ポリシーの更新を強制するには  
  
1. 管理者としてクライアント コンピューターにサインインします。  
  
2. [コマンド プロンプト] ウィンドウを管理者として開きます。  
  
3. コマンド プロンプトで、「**gpupdate /force**」と入力して Enter キーを押します。  
  
4. 処理を終了するには、いったんログオフしてログオンし直すことが必要な場合があります。 **[はい]** をクリックして確認します。  
  
   Windows Server Essentials またはそれ以前のバージョンから移行する場合、サーバーを降格するには、「 [Active Directory Domain Services の削除](https://technet.microsoft.com/library/hh472163.aspx)」を参照してください。 移行元サーバーをワークグループのメンバーとして追加し、ネットワークから切断した後、移行先サーバーで AD DS から移行元サーバーを削除する必要があります。  
  
   Windows Server Essentials から移行する場合は、サーバーマネージャーを使用して Active Directory Domain Services の役割を削除し、その結果、次の手順に従って移行元サーバーのドメインコントローラーを降格します。  
  
#### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory から移行元サーバーを削除するには  
  
1.  移行先サーバーで、 **[Active Directory ユーザーとコンピューター]** を開きます。  
  
2.  **[Active Directory ユーザーとコンピューター]** ナビゲーション ウィンドウで、ドメイン名を展開し、 **[コンピューター]** を展開します。  
  
3.  サーバーのリストに移行元サーバーがまだ存在する場合は、移行元サーバーの名前を右クリックし、 **[削除]** をクリックして、 **[はい]** をクリックします。  
  
4.  移行元サーバーが一覧に表示されないことを確認した後、 **[Active Directory ユーザーとコンピューター]** を閉じます。  
  
##  <a name="remove-and-repurpose-the-source-server"></a><a name="BKMK_RemoveTheSourceServer"></a>移行元サーバーの削除と転用  
 移行元サーバーの電源を切り、ネットワークから切断します。 必要なデータを移行先サーバーに確実に移行するため、少なくとも 1 週間は移行元サーバーを再フォーマットしないことをお勧めします。 データがすべて移行されたことを確認した後、必要に応じて、他のタスク用のセカンダリ サーバーとしてこのサーバーをネットワークに再インストールできます。  
  
> [!NOTE]
>  移行元サーバーを降格して削除した後、移行先サーバーを再起動します。  
  
 降格した後の移行元サーバーは、正常な状態ではありません。 移行元サーバーの用途を変更する最も簡単な方法は、再フォーマットし、サーバー オペレーティング システムをインストールした後、追加サーバーとして使用するように設定することです。  
  
## <a name="next-steps"></a>次のステップ:  
 新しい Windows Server Essentials ネットワークから移行元サーバーを降格し、削除しました。 [次に、「手順 7: Windows Server Essentials への移行のために移行後のタスクを実行](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)する」に進みます。  
  

すべての手順を表示するには、「 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)」を参照してください。

