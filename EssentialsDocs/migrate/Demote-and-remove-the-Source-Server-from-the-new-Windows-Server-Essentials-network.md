---
title: 降格して新しい Windows Server Essentials network1 から移行元サーバーを削除
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e5bcdd58f4d88f7a555151d755bf427ecc9b5108
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433004"
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>降格して新しい Windows Server Essentials network1 から移行元サーバーを削除

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials のインストールが完了したら、移行ウィザードでタスクを完了して後、は、次のタスクを実行する必要があります。  
  

1.  [Exchange Server 2003 をアンインストール](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)します。  
  
2.  [移行元サーバーに直接接続されているプリンターを切断する](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)。  
  
3.  [移行元サーバーを降格する](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [移行元サーバーからルーターに DHCP サーバーの役割を移動](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)します。  
  
5.  [移行元サーバーを削除して用途変更する](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)。  

1.  [Exchange Server 2003 をアンインストール](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)します。  
  
2.  [移行元サーバーに直接接続されているプリンターを切断する](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)。  
  
3.  [移行元サーバーを降格する](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [移行元サーバーからルーターに DHCP サーバーの役割を移動](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)します。  
  
5.  [移行元サーバーを削除して用途変更する](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)。  

  
###  <a name="BKMK_UninstallExchangeServer2003"></a> Exchange Server 2003 をアンインストールします。  
  
> [!IMPORTANT]
>  移行元サーバーから Exchange Server 2003 をアンインストールする前に、移行先サーバーにメールボックスを移動した後にユーザー アカウントを追加する場合は、メールボックスが移行元サーバーで追加されます。 これは仕様です。 この間に追加されたすべてのユーザー アカウントについて、メールボックスを移行先サーバーに移動する必要があります。 Exchange Server 2003 をアンインストールする前に、Windows Server Essentials への移行の Exchange サーバーの移動のメールボックスと設定の手順を繰り返します。  
  
 降格する前に、移行元サーバーから Exchange Server 2003 をアンインストールする必要があります。 これには、Active Directory ドメイン サービス (AD DS) に移行元サーバー上の Exchange サーバーですべての参照が削除されます。 Windows Small Business Server 2003 メディアで Exchange Server 2003 を削除する必要があります。  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>移行元サーバーから Exchange Server 2003 をアンインストールするには  
  
1. 管理者として移行元サーバーにログオンします。  
  
2. **[スタート]** 、 **[コントロール パネル]** 、 **[プログラムの追加と削除]** の順にクリックします。  
  
3. プログラムの一覧で選択**Windows Small Business Server 2003**、 をクリックし、**変更/削除**します。  
  
4. セットアップ ウィザードで、 **[コンポーネントの選択]** ページが表示されるまで **[次へ]** をクリックします。  
  
5. コンポーネントの選択 ページで、**Exchange Server** を展開し、**削除** を選択します。  
  
   > [!NOTE]
   > 
   >  Exchange Server によって、メールボックスまたはパブリック フォルダーがサーバー上にないことが確認されます。 データが残っている場合は、 **[削除]** をクリックするとエラー メッセージが表示されます。 この問題を避けるためには、すべてのトピックの手順を完了したことを確認します[SBS 2003 の移動の設定と移行先サーバーにデータ](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  
   > 
   >  Exchange Server によって、メールボックスまたはパブリック フォルダーがサーバー上にないことが確認されます。 データが残っている場合は、 **[削除]** をクリックするとエラー メッセージが表示されます。 この問題を避けるためには、すべてのトピックの手順を完了したことを確認します[SBS 2003 の移動の設定と移行先サーバーにデータ](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  

  
6. **[次へ]** をクリックします。  
  
7. 入力を求められたら、Windows Small Business Server 2003 CD #3 を挿入し、画面の指示に従ってください。  
  
###  <a name="BKMK_PhysicallyDisconnect"></a> 移行元サーバーに直接接続されているプリンターを切断します。  
 移行元サーバーを降格する前に、移行元サーバーに直接接続されていて、移行元サーバーを通して共有されているすべてのプリンターを、物理的に切断します。 移行元サーバーに直接接続されていたプリンターの Active Directory オブジェクトが残っていないことを確認します。 プリンターが直接、移行先サーバーに接続されているし、Windows Server Essentials から共有し、ことができます。  
  
###  <a name="BKMK_DemoteTheSourceServer"></a> 移行元サーバーを降格します。  
 移行元サーバーを AD DS ドメイン コントローラーの役割からドメイン メンバー サーバーの役割に降格する前に、以下の手順で説明されているように、グループ ポリシーの設定がすべてのクライアント コンピューターに適用されていることを確認します。  
  
> [!IMPORTANT]
>  クライアント コンピューターでグループ ポリシーの変更が更新されている間、移行元サーバーと移行先サーバーはネットワークに接続されている必要があります。  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>クライアント コンピューターでグループ ポリシーの更新を強制するには  
  
1.  管理者としてクライアント コンピューターにログオンします。  
  
2.  [コマンド プロンプト] ウィンドウを管理者として開きます。  
  
3.  コマンド プロンプトで、「 **gpupdate /force**」と入力して Enter キーを押します。  
  
4.  処理を終了するには、いったんログオフしてログオンし直すことが必要な場合があります。 **[はい]** をクリックして確認します。  
  
##### <a name="to-demote-the-source-server"></a>移行元サーバーを降格するには  
  
1. 移行元サーバーで、 **[スタート]** 、 **[ファイル名を指定して実行]** の順にクリックし、「**dcpromo**」と入力して、 **[OK]** をクリックします。  
  
2. **[次へ]** を 2 回クリックします。  
  
   > [!NOTE]
   >  **[このサーバーはドメインの最後のドメイン コントローラーです]** をオンにしないでください。  
  
3. サーバーの新しい管理者アカウントのパスワードを入力し、 **[次へ]** をクリックします。  
  
4. **概要**ダイアログ ボックスで、AD DS がコンピューターから削除することと、サーバーがドメインのメンバーになることが示されます。 **[次へ]** をクリックします。  
  
5. **[Finish]** (完了) をクリックします。 移行元サーバーが再起動します。  
  
6. 移行元サーバーが再起動した後、ネットワークから切断する前に、移行元サーバーをワークグループのメンバーとして追加します。  
  
   移行元サーバーをワークグループのメンバーとして追加し、ネットワークから切断した後、移行先サーバーで AD DS から移行元サーバーを削除する必要があります。  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory から移行元サーバーを削除するには  
  
1.  移行先サーバーで、 **[Active Directory ユーザーとコンピューター]** を開きます。  
  
2.  **[Active Directory ユーザーとコンピューター]** ナビゲーション ウィンドウで、ドメイン名を展開し、 **[コンピューター]** を展開します。  
  
3.  サーバーの一覧に移行元サーバーがまだ存在する場合はそれを右クリックし、 **[削除]** をクリックして、 **[はい]** をクリックします。  
  
4.  移行元サーバーが一覧に表示されないことを確認した後、 **[Active Directory ユーザーとコンピューター]** を閉じます。  
  
###  <a name="BKMK_MoveTheDHCPRole"></a> 移行元サーバーから DHCP サーバーの役割をルーターに移動します。  
  
> [!NOTE]
> 
>  移行プロセスを開始する前にこのタスクを既に実行した場合は、「[移行元サーバーを削除して用途変更する](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)」セクションに進んでください。  
> 
>  移行プロセスを開始する前にこのタスクを既に実行した場合は、「[移行元サーバーを削除して用途変更する](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)」セクションに進んでください。  

  
 移行元サーバーが DHCP の役割を実行している場合、次の手順を実行して、DHCP の役割をルーターに移動します。  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>DHCP の役割を移行元サーバーからルーターに移動するには  
  
1.  次のようにして、移行元サーバーで DHCP サービスをオフにします。  
  
    1.  移行元サーバーをクリックし、 **[スタート]** 、 **[管理ツール]** 、 **[サービス]** の順にクリックします。  
  
    2.  現在実行しているサービスの一覧で、 **[Windows Server]** を右クリックし、 **[プロパティ]** をクリックします。  
  
    3.  **[開始の種類]** で、 **[無効]** を選択します。  
  
    4.  サービスを停止します。  
  
2.  ルーターで DHCP の役割を有効にします。  
  
    1.  ルーターで DHCP の役割を有効にするには、ルーターのドキュメントの手順に従います。  
  
    2.  移行元サーバーによって発行される IP アドレスが変わらないようにするには、ルーターのドキュメントの手順に従って、ルーターの DHCP 範囲を、移行元サーバーの DHCP 範囲と同じように構成します。  
  
    > [!IMPORTANT]
    >  ルーターで移行先サーバー用に静的 IP または DHCP 予約が設定されていず、DHCP 範囲が移行元サーバーと異なる場合は、ルーターが移行先サーバーの新しい IP アドレスを発行する可能性があります。 その場合は、ルーターのポート転送ルールを、移行先サーバーの新しい IP アドレスに転送するように設定しなおします。  
  
###  <a name="BKMK_RemoveTheSourceServer"></a> 削除して、移行元サーバーの用途を変更  
 移行元サーバーの電源を切り、ネットワークから切断します。 必要なデータを移行先サーバーに確実に移行するため、少なくとも 1 週間は移行元サーバーを再フォーマットしないことをお勧めします。 データがすべて移行されたことを確認した後、必要に応じて、他のタスク用のセカンダリ サーバーとしてこのサーバーをネットワークに再インストールできます。  
  
> [!NOTE]
>  移行元サーバーを降格して削除した後、移行先サーバーを再起動します。  
  
 降格した後の移行元サーバーは、正常な状態ではありません。 移行元サーバーの用途を変更する最も簡単な方法は、再フォーマットし、サーバー オペレーティング システムをインストールした後、追加サーバーとして使用するように設定することです。
