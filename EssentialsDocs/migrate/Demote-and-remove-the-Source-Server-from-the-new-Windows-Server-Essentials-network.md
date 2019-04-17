---
title: "降格して新しい Windows Server Essentials network1 から、移行元サーバーを削除します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 1545189732194ad5c0aba401f834b0102799e016
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>降格して新しい Windows Server Essentials network1 から、移行元サーバーを削除します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server Essentials のインストールが完了したら、移行ウィザードでタスクを完了すると、次のタスクを実行する必要があります。  
  

1.  [Exchange Server 2003 をアンインストール](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)します。  
  
2.  [移行元サーバーに直接接続されているプリンターを切断](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)します。  
  
3.  [移行元サーバーを降格](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)します。  
  
4.  [移行元サーバーから DHCP サーバーの役割をルーターに移動](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)します。  
  
5.  [削除して、移行元サーバーとして再利用](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)します。  

1.  [Exchange Server 2003 をアンインストール](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)します。  
  
2.  [移行元サーバーに直接接続されているプリンターを切断](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)します。  
  
3.  [移行元サーバーを降格](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)します。  
  
4.  [移行元サーバーから DHCP サーバーの役割をルーターに移動](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)します。  
  
5.  [削除して、移行元サーバーとして再利用](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)します。  

  
###  <a name="BKMK_UninstallExchangeServer2003"></a>Exchange Server 2003 をアンインストールします。  
  
> [!IMPORTANT]
>  移行先サーバーと移行元サーバーから Exchange Server 2003 をアンインストールする前に、メールボックスを移動した後にユーザー アカウントを追加する場合、移行元サーバー上のメールボックスが追加されます。 これは仕様です。 この期間中に追加されているすべてのユーザー アカウントの移行先サーバーに、メールボックスを移動する必要があります。 Exchange Server 2003 をアンインストールする前に、Windows Server Essentials 移行の Exchange Server の移動のメールボックスと設定、手順を繰り返します。  
  
 降格する前に、移行元サーバーから Exchange Server 2003 をアンインストールする必要があります。 これは、Active Directory ドメイン サービス (AD DS) に、移行元サーバーで、Exchange Server でのすべての参照を削除します。 Exchange Server 2003 を削除するには、Windows Small Business Server 2003 メディアが必要です。  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>移行元サーバーから Exchange Server 2003 をアンインストールするには  
  
1.  管理者として移行元サーバーにログオンします。  
  
2.  をクリックして**開始**、] をクリックして**コントロール パネルの [**、] をクリックし、**プログラム追加と削除**します。  
  
3.  プログラムの一覧で選択**Windows Small Business Server 2003**、] をクリックし、**変更と削除**します。  
  
4.  セットアップ ウィザードで、をクリックして**次**されるまで、**コンポーネントの選択**ページが表示されます。  
  
5.  コンポーネントの選択] ページで、展開**Exchange Server**、し、[**削除**します。  
  
    > [!NOTE]

    >  Exchange Server はメールボックスまたはサーバー上のパブリック フォルダーがないことを確認することを確認します。 クリックするとすべてのデータが残っている場合、エラー メッセージが表示されます**削除**します。 この問題を避けるためには、すべてのトピックの手順を完了したことを確認します[SBS 2003 の移動の設定とデータを移行先サーバーに](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  

    >  Exchange Server はメールボックスまたはサーバー上のパブリック フォルダーがないことを確認することを確認します。 クリックするとすべてのデータが残っている場合、エラー メッセージが表示されます**削除**します。 この問題を避けるためには、すべてのトピックの手順を完了したことを確認します[SBS 2003 の移動の設定とデータを移行先サーバーに](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  

  
6.  をクリックして**次**します。  
  
7.  されたら、Windows Small Business Server 2003 CD #3 を挿入し、画面の指示に従ってください。  
  
###  <a name="BKMK_PhysicallyDisconnect"></a>移行元サーバーに直接接続されているプリンターを切断します。  
 移行元サーバーを降格する前に物理的には、移行元サーバーに直接接続し、移行元サーバーを通して共有されているすべてのプリンターを切断します。 移行元サーバーに直接接続されているプリンターを Active Directory オブジェクトが残っていないことを確認します。 プリンターが直接、移行先サーバーに接続されているし、Windows Server Essentials から共有し、ことができます。  
  
###  <a name="BKMK_DemoteTheSourceServer"></a>移行元サーバーを降格します。  
 AD DS ドメイン コントローラーの役割からドメイン メンバー サーバーの役割を移行元サーバーを降格する前にことを確認するすべてのクライアント コンピューターのグループ ポリシー設定が適用されているように、次の手順で説明されています。  
  
> [!IMPORTANT]
>  クライアント コンピューターでグループ ポリシーの変更が更新されたときに、移行元サーバーと移行先サーバーがネットワークに接続する必要があります。  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>クライアント コンピューターでグループ ポリシーの更新を強制するには  
  
1.  管理者としてクライアント コンピューターにログオンします。  
  
2.  管理者としてコマンド プロンプト ウィンドウを開きます。  
  
3.  コマンド プロンプトで、次のように入力します。**gpupdate/force**、し、Enter キーを押します。  
  
4.  プロセスは、ログオフし、[完了] をもう一度ログオンする必要があります。 をクリックして**はい**ことを確認します。  
  
##### <a name="to-demote-the-source-server"></a>移行元サーバーを降格するには  
  
1.  移行元サーバーで、をクリックして**開始**、] をクリックして**実行**、種類**dcpromo**、] をクリックし、**[OK]**します。  
  
2.  をクリックして**次**2 回クリックします。  
  
    > [!NOTE]
    >  選択しないでください**このサーバーは、ドメイン内の最後のドメイン コントローラー**します。  
  
3.  サーバーで、新しい管理者アカウントのパスワードを入力し、クリックして**次**します。  
  
4.  **概要**ダイアログ ボックスで、AD DS をコンピューターから削除することと、サーバーがドメインのメンバーになることが示されます。 をクリックして**次**します。  
  
5.  をクリックして**完了**します。 移行元サーバーを再起動します。  
  
6.  移行元サーバーが再起動したら、ネットワークから切断する前に、ワークグループのメンバーとして、移行元サーバーを追加します。  
  
 ワークグループのメンバーとして、移行元サーバーを追加し、ネットワークから切断した後は、移行先サーバーで AD DS から削除する必要があります。  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory から移行元サーバーを削除するには  
  
1.  移行先サーバーで、開く**Active Directory ユーザーとコンピューター**します。  
  
2.  **Active Directory ユーザーとコンピューター**のナビゲーション ウィンドウで、ドメイン名を展開し、展開**コンピューター**します。  
  
3.  右クリックして、移行元サーバー名、サーバーの一覧にまだ存在する場合**削除**、] をクリックし、**はい**します。  
  
4.  いないことを確認、移行元サーバーの一覧とし、[閉じる**Active Directory ユーザーとコンピューター**します。  
  
###  <a name="BKMK_MoveTheDHCPRole"></a>移行元サーバーから DHCP サーバーの役割をルーターに移動します。  
  
> [!NOTE]

>  既に移行プロセスを開始する前に、このタスクが実行された場合、は、」セクションに進んで[を削除して、移行元サーバーとして再利用](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)します。  

>  既に移行プロセスを開始する前に、このタスクが実行された場合、は、」セクションに進んで[を削除して、移行元サーバーとして再利用](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)します。  

  
 移行元サーバーが DHCP の役割を実行中の場合は、DHCP の役割をルーターに移動するには、次の手順を実行します。  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>DHCP の役割を移行元サーバーからルーターに移動するには  
  
1.  次のように、移行元サーバーで DHCP サービスをオフにします。  
  
    1.  移行元サーバーで、をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、**サービス**します。  
  
    2.  サービスが現在実行中の一覧で、右クリックし、**Windows Server**、] をクリックし、**プロパティ**します。  
  
    3.  **開始の種類**[**無効になっている**します。  
  
    4.  サービスを停止します。  
  
2.  ルーターで DHCP の役割を有効にします。  
  
    1.  指示に従って、ルーターのドキュメントをルーターで DHCP の役割をオンにします。  
  
    2.  されないようにする、移行元サーバーで発行される IP アドレスと同じ、指示に従って、ルーターのドキュメントを移行元サーバー上の DHCP 範囲と同じであるルーターで DHCP 範囲を構成します。  
  
    > [!IMPORTANT]
    >  移行先サーバーの場合、ルーター上での静的 IP アドレスまたは DHCP 予約を設定していないと、DHCP 範囲は、移行元サーバーと同じではない、ルーターが移行先サーバーの新しい IP アドレスを発行する可能性があります。 この場合、転送ルールを移行先サーバーの新しい IP アドレスに転送するようにルーターのポートをリセットします。  
  
###  <a name="BKMK_RemoveTheSourceServer"></a>削除して、移行元サーバーとして再利用  
 移行元サーバーをオフにして、ネットワークから切断します。 移行元サーバーを移行先サーバーに必要なすべてのデータが移行されたことを確認するには、少なくとも 1 週間を再フォーマットしないことをお勧めします。 すべてのデータが移行されたことを確認したら、再インストールできますこのサーバー、ネットワーク上、他のタスクのセカンダリ サーバーとして必要な場合です。  
  
> [!NOTE]
>  降格して、移行元サーバーを削除した後は、移行先サーバーを再起動します。  
  
 移行元サーバーを降格した後は、正常な状態 移行元サーバーの用途を変更する場合は、最も簡単な方法が、再フォーマットし、サーバーのオペレーティング システムをインストールし、その他のサーバーとして使用するために設定します。
