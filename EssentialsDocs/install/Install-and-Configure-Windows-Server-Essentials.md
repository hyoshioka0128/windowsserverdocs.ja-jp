---
title: Windows Server Essentials のインストールと構成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 06/17/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 48fa18d5baf7d4b48b14cbda5a513c487920d70a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433470"
---
# <a name="install-and-configure-windows-server-essentials"></a>Windows Server Essentials のインストールと構成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_InstallConfigure"></a>   

 このドキュメントのインストールと Windows Server Essentials の構成手順をについて説明します。 インストールを開始する前に確認し、記載されているタスクを完了[する前にする Windows Server Essentials のインストール](Before-You-Install-Windows-Server-Essentials.md)します。  

 このドキュメントのインストールと Windows Server Essentials の構成手順をについて説明します。 インストールを開始する前に確認し、記載されているタスクを完了[する前にする Windows Server Essentials のインストール](../install/Before-You-Install-Windows-Server-Essentials.md)します。  
  
 インストールし、2 つの手順で Windows Server Essentials を構成します。  
  

1.  [ステップ 1: Windows Server Essentials のオペレーティング システムをインストール](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation)この手順で、サーバーのオペレーティング システムをインストールします。  
  
2.  [手順 2:Windows Server Essentials のオペレーティング システムを構成する](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure)この手順で会社、ドメイン設定、ネットワーク管理者に関する情報を提供することで、インストールを完了します。 この情報は、サーバーの使用準備に使用されます。  

1.  [ステップ 1: Windows Server Essentials のオペレーティング システムをインストール](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation)この手順で、サーバーのオペレーティング システムをインストールします。  
  
2.  [手順 2:Windows Server Essentials のオペレーティング システムを構成する](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure)この手順で会社、ドメイン設定、ネットワーク管理者に関する情報を提供することで、インストールを完了します。 この情報は、サーバーの使用準備に使用されます。  

  
###  <a name="BKMK_ManualInstallation"></a> 手順 1:Windows Server Essentials オペレーティング システムをインストールします。  
  
> [!IMPORTANT]
>  オペレーティング システムのインストール後はサーバーをカスタマイズを完了するまで[手順 2。Windows Server Essentials のオペレーティング システムを構成する](#BKMK_Step2Configure)します。  
  
 **推定完了時間:** 約 30 分。  
  
> [!NOTE]
>  この手順全体の推定完了時間は、最小ハードウェア要件に基づいています。  
  
##### <a name="to-install-the-operating-system"></a>オペレーティング システムをインストールするには  
  
1. コンピューターをネットワークにネットワーク ケーブルで接続します。  
  
   > [!IMPORTANT]
   >  インストール中は、コンピューターをネットワークから切断しないでください。 切断すると、インストールに失敗する可能性があります。  
  
2. コンピューターに有効にして、Windows Server Essentials の DVD を DVD ドライブに挿入します。  
  
    無人インストールを実行している場合、応答ファイルを含むリムーバブル メディア (フロッピー ディスク、USB フラッシュ ドライブなど) を接続します。 応答ファイルの内容によっては、次のインストール画面の一部または全部が表示されない場合があります。  
  
3. コンピューターを再起動します。 「**CD または DVD から起動するには、いずれかのキーを押してください**」というメッセージが表示されたら、任意のキーを押します。  
  
   > [!NOTE]
   >  コンピューターが DVD から起動しない場合、CD-ROM ドライブが BIOS ブート シーケンスのリストの最初に表示されていることを確認します。 BIOS ブート シーケンスの詳細については、コンピューター製造元のマニュアルを参照してください。  
  
4. インストールする **[言語]** 、 **[時刻と通貨の形式]** 、 **[キーボードまたは入力方式]** を選択し、 **[次へ]** をクリックします。  
  
5. **[今すぐインストール]** をクリックします。  
  
6. **[プロダクト キーを入力してください]** に、プロダクト キーを入力します。  
  
7. **ライセンス条項**を読みます。 同意する場合、 **[ライセンス条項に同意します]** チェック ボックスをオンにし、 **[次へ]** をクリックします。  
  
   > [!NOTE]
   >  ライセンス条項に同意しない場合、インストールは続行されません。  
  
8. **インストールの種類が必要ですか?** 、 をクリックして**カスタム。Windows のインストールのみ (詳細)**  
  
9. **[Windows のインストール場所を選んでください。]** で、Windows オペレーティング システムのインストール先となるハード ドライブを選択します。 すべての内部ハード ドライブがインストールに使用できることを確認します。  
  
    > [!IMPORTANT]
    >   Windows Server Essentials は、c: ボリュームとしてインストールする必要があり、ボリューム サイズは 60 GB 以上である必要があります。 オペレーティング システム ディスクに 2 つのパーティションを作成し、ビジネス データの格納には C: (システム パーティション) を使用しないことをお勧めします。  
  
    > [!NOTE]
    >  ハード ドライブ (たとえば、Serial Advanced Technology Attachment (SATA) ハード ディスク) がリストにない場合、そのハード ディスクのデバイス ドライバーを読み込む必要があります。 製造元からデバイス ドライバーを入手し、リムーバブル メディア (フロッピー ディスク、USB フラッシュ ドライブなど) に保存します。 リムーバブル メディアをコンピューターに接続し、 **[ドライバーの読み込み]** をクリックします。  
  
     パーティションの削除や作成が必要な場合、次の手順を参照してください。  
  
    1.  パーティションを削除するには、パーティションを選択し、 **[ドライブ オプション (詳細)]** をクリックした後、 **[削除]** をクリックします。 システム パーティションを削除した後、新しいパーティションを作成するため、手順 **b** または手順 **c** の手順を使用します。  
  
        > [!NOTE]
        >  **[ドライブ オプション (詳細)]** をクリックした後、このオプションは二度と表示されません。 この場合、ドライブ オプションに関係する手順部分をスキップします。  
  
    2.  未使用の領域からパーティションを作成するには、パーティションを分割するハード ディスクをクリックし、 **[ドライブ オプション (詳細)]** をクリックし、 **[新規]** をクリックした後、 **[サイズ]** ボックスに、作成するパーティションのサイズを入力します。 たとえば、120 ギガバイト (GB) の推奨パーティション サイズを使用する場合、「 **122880**」と入力し、 **[適用]** をクリックします。 パーティションが作成されたら、 **[次へ]** をクリックします。 パーティションは、インストールが続行される前にフォーマットされます。  
  
    3.  すべての未使用の領域を使用するパーティションを作成するには、 **[ドライブ オプション (詳細)]** をクリックし、 **[新規]** をクリックした後、 **[適用]** をクリックして既定のパーティション サイズを受け入れます。 パーティションが作成されたら、 **[次へ]** をクリックします。 パーティションは、インストールが続行される前にフォーマットされます。  
  
        > [!IMPORTANT]
        >  この手順の完了後は、オペレーティング システムを別のパーティションに移動できません。  
  
   インストール中、一時ファイルがインストール フォルダーにコピーされます。これには約 30 分かかります。 Windows Server Essentials のオペレーティング システムのインストール後、コンピューターを再起動します。 ここで、Windows Server Essentials オペレーティング システムを構成する準備が完了したら。  
  
###  <a name="BKMK_Step2Configure"></a> 手順 2:Windows Server Essentials のオペレーティング システムを構成します。  
  
> [!IMPORTANT]
>  Windows Small Business Server の以前のバージョンから Windows Server Essentials に移行する場合、別のプロセスに従う必要があります。 移行インストールの詳細については、次を参照してください。  
> 
> - [Windows SBS 2003 から移行します。](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
>   -   [Windows SBS 2008 から移行します。](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 インストールのこの段階のあいだに、組織に関するいくつかの質問に答えるよう要求するメッセージが表示されます。 この情報は、オペレーティング システムの構成に使用されます。  
  
> [!IMPORTANT]
>  この手順を開始する前に、ローカル ネットワーク アダプターが、電源がオンで正常に機能しているルーターまたはスイッチに接続されていることを確認します。  
  
 **推定完了時間:** 約 30 分  
  
##### <a name="to-configure-the-operating-system"></a>オペレーティング システムを構成するには  
  
1.  **[日付と時刻の設定の確認]** ページで、 **[システム日付および時刻の設定の変更]** をクリックして、サーバーの日付、時刻、タイム ゾーン設定を選択します。 終了したら **[次へ]** をクリックします。  
  
    > [!IMPORTANT]
    >  仮想マシンに Windows Server Essentials をインストールする場合は、ホスト オペレーティング システムで使用されているタイム ゾーンの設定を選択することを確認します。 タイム ゾーン設定が異なると、サーバーのインストールが失敗する可能性があります。  
  
2.  **[サーバーのインストール モードの選択]** ページで、次のいずれかを実行します。  
  
    1.  選択**クリーン インストール**Windows Server Essentials サーバー ソフトウェアのフル新規インストールを設定します。  
  
    2.  選択**サーバーの移行**を Windows Server Essentials をインストールしてこのサーバーを既存の Windows ドメインに参加させます。  
  
3.  **[サーバーをカスタマイズします]** ページで、組織の名前、内部ドメイン名、サーバー名を入力します。  
  
    > [!IMPORTANT]
    >  サーバー名は、ネットワークで一意の名前にする必要があります。 この手順の終了後にサーバー名または内部ドメイン名を変更することはできません。  
  
4.  **[次へ]** をクリックします。  
  
5.  **[管理者アカウント情報を入力してください]** ページで、新しい管理者アカウントの情報を入力します。  
  
    > [!CAUTION]
    >  管理者またはネットワーク管理者は、ネットワーク管理者のアカウントを指定してはいません。 これらのアカウント名は、システムが使用するために予約されています。  
  
6.  **[標準のユーザー アカウント情報を入力してください]** ページで、新しい標準ユーザー アカウントの情報を入力し、 **[次へ]** をクリックします。  
  
7.  **[サーバーを自動的に最新の状態に保ちます]** ページで、サーバーに対する Windows Updates の受信方法を選択し、 **[次へ]** をクリックします。  
  
8.  **[サーバーを更新および準備しています]** ページに、最終インストール プロセスの進行状況が表示されます。 完了するまでには時間がかかり、コンピューターが 2 回ほど再起動します。  
  
9. サーバーの最後の再起動後に、 **[サーバーを使用する準備ができました]** ページが表示されます。 **[閉じる]** をクリックします。  
  
10. **[スタート]** 画面のダッシュボード タイトルをクリックし、ダッシュボード上で、 **[ホーム]** ページの **[サーバーのセットアップ]** タスクを完了します。 Windows Server Essentials のインストールが完了した直後に、これらのタスクを完了する必要があります。  
  
> [!NOTE]
>  インストールが終了すると、インストール中に追加した新しい管理者アカウントで、サーバーに自動的にログオンされます。 内蔵 Administrator アカウント パスワードが新しい管理者アカウントと同じパスワードに設定され、内蔵 Administrator アカウントが無効になります。  
  
 プロダクト キーを入力しなくても、一定の時間 (評価期間と呼ばれます) を新しくインストールされたサーバーを使用できます。 評価期間後、プロダクト キーを入力してサーバーをアクティブにするか、評価期間を延長します。 評価期間は、2 回まで延長できます。 評価期間として許可された最大日数に達すると、サーバーをプロダクト キーでアクティブにする必要があります。  
  
### <a name="customize-windows-server-essentials"></a>Windows Server Essentials をカスタマイズします。  
 **ホーム**、Windows Server Essentials ダッシュ ボードのページにリンク**セットアップ**直後後に完了する必要がありますタスクは、サーバーをインストールします。 これらのタスクを実行するには、サーバーに格納されている情報を保護し、Windows Server Essentials で利用できる機能を有効にするができます。  
  
 タスクの実行を選択しないと、ユーザーが一部のネットワーク機能にアクセスできない可能性があります。 後でこれらのタスクに戻るには、Windows Server Essentials ダッシュ ボードに戻り**ホーム**ページ。  
  
 次の表は、セットアップ タスクのリストに表示される可能性がある項目を定義しています。  
  
|タスク|説明
|----------|-----------------|  
|他のマイクロソフト製品の更新プログラムの入手|Microsoft Update を使用して、Windows Server Essentials と Office などの他の Microsoft 製品の更新プログラムを自動的に取得するかを指定するためのツールを実行しているリンクにアクセスするには、このタスクをクリックします。  
|ユーザー アカウントを追加する|このタスクをクリックすると、ユーザー アカウントの追加に関する簡単な情報が表示されます。 **ユーザー アカウントの追加ウィザード** を実行するためのリンクがあります。 詳細については、「 [Add a user account](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)」を参照してください。  
|サーバー フォルダーの追加|このタスクをクリックすると、サーバー フォルダーの追加に関する簡単な情報が表示されます。 **フォルダーの追加ウィザード** を実行するためのリンクがあります。 サーバー フォルダーの使用に関するオンライン ヘルプ トピックへのリンクも提供されています。 詳細については、「 [Add or move a server folder](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)」を参照してください。 
|サーバー バックアップのセットアップ|このタスクをクリックすると、サーバー バックアップを使用したデータの保護に関する簡単な情報が表示されます。 **サーバー バックアップのセットアップ ウィザード** を実行するためのリンクがあります。 詳細については、「[サーバー バックアップのセットアップまたはカスタマイズ](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)」を参照してください。 
|Anywhere Access のセットアップ|Windows Server Essentials で Anywhere Access 機能に関する簡単な情報を表示するには、このタスクをクリックします。 **[Anywhere Access の設定]** ページへのリンクがあります。 詳細については、次を参照してください。 [Manage Anywhere Access](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)します。 
|電子メール アラート通知のセットアップ|このタスクをクリックすると、電子メール アラート通知に関する簡単な情報が表示されます。 **[アラートの電子メール通知のセットアップ]** ツールを実行するためのリンクがあります。 詳細については、「[アラートの電子メール通知のセットアップ](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)」を参照してください。  
|メディア サーバーのセットアップ|このタスクをクリックすると、メディア サーバーを使用した音楽、ビデオ、イメージ ファイルの共有に関する簡単な情報が表示されます。 **[メディア設定]** ページへのリンクがあります。 メディア サーバーの詳細に関するオンライン ヘルプ トピックへのリンクも提供されています。 詳細については、次を参照してください。 [Manage Digital Media](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)します。 
|コンピューターの接続|このタスクをクリックすると、ネットワーク コンピューターをサーバーに接続する方法に関する簡単な情報が表示されます。 詳細については、「 [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials のインストール](Install-Windows-Server-Essentials.md)

