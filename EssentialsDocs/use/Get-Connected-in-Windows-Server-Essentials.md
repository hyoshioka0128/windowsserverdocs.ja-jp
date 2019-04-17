---
title: "Windows Server Essentials で接続します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 05/07/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 149a5d34-43b7-4b9e-99e7-9f2294ab9ddb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1d7f3c33f1254c8dbe4af8bdf5baa4144c134248
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="get-connected-in-windows-server-essentials"></a>Windows Server Essentials で接続します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:
  
 コネクタ ソフトウェアを使用して、Windows Server Essentials サーバーにコンピューターを接続できます。 サーバー ウィザードへのコンピューターの接続を使用して、サーバーにコンピューターを接続すると、コネクタ ソフトウェアがインストールされます。 」と入力して、このウィザードを開始することができます**http://<servername\>/connect**ここで、 **< servername\ >**は、サーバーの名前です。  
  
 このトピックの「します。  
  

-   [コンピューターをサーバーに接続するための準備します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  
  
-   [コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  
  
-   [スタート パッドを使用します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

-   [コンピューターをサーバーに接続するための準備します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  
  
-   [コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  
  
-   [スタート パッドを使用します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

  
##  <a name="BKMK_A"></a>コンピューターをサーバーに接続するための準備します。  
 このセクションでは、コネクタ ソフトウェア、Windows Server Essentials、コンピューターをサーバーに接続する前に完了する必要がある前提条件となるタスク、およびサーバーが実行するコンピューターにコネクタ ソフトウェアを実行すると、変更によってサポートされるオペレーティング システムについて説明します。  
  

-   [コネクタ ソフトウェアの概要](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [コンピューターをサーバーに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Mac コンピューターをネットワークに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [クライアント コンピューターのサポートされるオペレーティング システム](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [サーバーが実行するクライアント コンピューターへの変更](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [ネットワーク ユーザー名とパスワード情報](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [サーバー管理者のアカウント](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Windows ドメインからコンピューターを削除します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  
  
###  <a name="BKMK_1"></a>コネクタ ソフトウェアの概要  
 Windows Server Essentials オペレーティング システム用のコネクタ ソフトウェアは、Windows Server Essentials サーバーに、ネットワーク内のコンピューターを接続します。 コンピューターをサーバーに接続するときに、コネクタ ソフトウェアでは、自動的にコンピューターをバックアップし、正常性を監視することができます。 コネクタ ソフトウェアを構成し、Windows Server Essentials サーバーをリモートで管理することもできます。 クライアント コンピューターをサーバーに接続するときに、コネクタ ソフトウェアがインストールされます。 クライアント コンピューターを Windows Server Essentials サーバーに接続する詳細については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)このトピックで後述します。  

-   [コネクタ ソフトウェアの概要](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [コンピューターをサーバーに接続するための前提条件](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Mac コンピューターをネットワークに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [クライアント コンピューターのサポートされるオペレーティング システム](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [サーバーが実行するクライアント コンピューターへの変更](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [ネットワーク ユーザー名とパスワード情報](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [サーバー管理者のアカウント](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Windows ドメインからコンピューターを削除します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  
  
###  <a name="BKMK_1"></a>コネクタ ソフトウェアの概要  
 Windows Server Essentials オペレーティング システム用のコネクタ ソフトウェアは、Windows Server Essentials サーバーに、ネットワーク内のコンピューターを接続します。 コンピューターをサーバーに接続するときに、コネクタ ソフトウェアでは、自動的にコンピューターをバックアップし、正常性を監視することができます。 コネクタ ソフトウェアを構成し、Windows Server Essentials サーバーをリモートで管理することもできます。 クライアント コンピューターをサーバーに接続するときに、コネクタ ソフトウェアがインストールされます。 クライアント コンピューターを Windows Server Essentials サーバーに接続する詳細については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)このトピックで後述します。  

  
###  <a name="BKMK_2"></a>コンピューターをサーバーに接続するための前提条件  
 コンピューターをネットワークに接続する前に、次の要件を満たす必要があります。  
  
-   Windows Server Essentials のインストールが完了し、サーバーが実行されています。 サーバーと通信できない場合、コネクタ ソフトウェアは、インストールを終了します。  
  

-   クライアント コンピューターは、サポートされるオペレーティング システムを実行しています。 詳細については、次を参照してください。[サポートされるクライアント コンピューターのオペレーティング システム](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)します。

  
-   クライアント コンピューターは、インターネットへの接続を有効が必要です。  
  
-   クライアント コンピューターでは、クライアント コンピューターが、サーバーと同じネットワーク上のときに、Windows Server Essentials を実行しているサーバーと同じ IP サブネット上です。  
  
-   クライアント コンピューターは、.NET Framework 4.5 がインストールされています。 コネクタ ソフトウェアを自動的のコンピューターにインストールします。  
  
-   クライアント コンピューターは、次の最小システム要件を満たしています。  
  
    -   1.4 GHz 以上のプロセッサ  
  
    -   1 GB RAM 以上  
  
    -   1 GB の利用可能なハード ドライブ容量 (この容量の一部はインストール後に解放)  
  
-   ブート パーティション (つまり、Windows オペレーティング システムがインストールされているディスク パーティション) は、NTFS ファイル システムでフォーマットされました。  
  
-   コンピューター名では、15 文字以内は含まれません。  
  
-   コンピューター名では、アンダー スコア (_) は含まれません。  
  
-   S のコンピューターの日付と時刻の設定は、設定、サーバーに配置されます。  
  
-   クライアント コンピューターは、特定の時点で 1 つだけの Windows Server Essentials サーバーに接続できます。  
  
-   既に別の Active Directory ドメインに参加しているクライアント コンピューターは、Windows Server Essentials ドメインに参加できません。  
  
> [!NOTE]

>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加せず、サーバーにコンピューターを接続できます。 この方法がすべてのサポートされるクライアント オペレーティング システム、およびグループ ポリシーなどの機能を利用できないと仮想プライベート ネットワーク (Vpn)、コンピューターがドメインに接続することが必要ながご利用いただけません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  
  
 Windows Server Essentials を実行しているサーバーにコンピューターを接続する手順については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  

>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加せず、サーバーにコンピューターを接続できます。 この方法がすべてのサポートされるクライアント オペレーティング システム、およびグループ ポリシーなどの機能を利用できないと仮想プライベート ネットワーク (Vpn)、コンピューターがドメインに接続することが必要ながご利用いただけません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  
  
 Windows Server Essentials を実行しているサーバーにコンピューターを接続する手順については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  

  
###  <a name="BKMK_3"></a>Mac コンピューターをネットワークに接続するための前提条件  
 Mac コンピューターをネットワークに接続する前に、次の要件を満たす必要があります。  
  
-   サーバーのオペレーティング システムのインストールが完了し、サーバーが実行されています。 サーバーと通信できない場合は、コネクタ ソフトウェアはインストールされません。  
  
-   コンピューターは、X 10.5 (Leopard) 以降、Mac OS を実行しています。  
  
-   コンピューターは、サーバーと同じ IP サブネット上にあります。  
  
-   インターネットへの接続を有効なコンピューターが必要です。  
  
-   コンピューターが、次の最小システム要件を満たしていることを確認します。  
  
    -   1.4 GHz 以上のプロセッサ  
  
    -   1 GB RAM 以上  
  
    -   1 GB の利用可能なハード ドライブ容量 (この容量の一部はインストール後に解放)  
  
-   クライアント コンピューターは、特定の時点で 1 つだけのサーバーに接続できます。  
  
###  <a name="BKMK_4"></a>クライアント コンピューターのサポートされるオペレーティング システム  
 Windows Server Essentials では、すべてのサポートされているクライアント コンピューターの同じ機能セットを提供します。 これらの機能には、ドメインに参加、スタート パッド、およびクライアント側の正常性通知が含まれます。  
  
> [!IMPORTANT]
>  Windows Server Essentials は、Home、Starter、または Media Center のバージョンの Windows を実行して、ドメインに参加するコンピューターをサポートしていません。 さらに、リモート Web アクセスを使用して、これらのコンピュータに接続することはできません。  
  
#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  このセクションでは、またはインストールされている Windows Server Essentials エクスペリエンスの役割を持つ Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter を実行しているサーバーに、Windows Server Essentials を実行するサーバーに適用されます。 次のコンピューターのオペレーティング システムがサポートされています。  
  
 **Windows 7 オペレーティング システム**  
  
-    Windows 7 ホーム基本的な SP1 (x86 および x64)  
  
-    Windows 7 ホーム Premium SP1 (x86 および x64)  
  
-    Windows 7 Professional SP1 (x86 および x64)  
  
-    Windows 7 Ultimate SP1 (x86 および x64)  
  
-    Windows 7 Enterprise SP1 (x86 および x64)  
  
-    Windows 7 のスターター SP1 (x86)  
  
 **Windows 8 オペレーティング システム**  
  
-   Windows 8  
  
-   Windows 8 Professional  
  
-   Windows 8 Enterprise  
  
 **Windows 8.1 オペレーティング システム**  
  
-   Windows 8.1  
  
-   Windows 8.1 の Professional  
  
-   Windows 8.1 Enterprise  
  
 **Windows 10 オペレーティング システム**  
  
-   Windows 10  
  
-   Windows 10 Professional  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Education  
  
 **Mac クライアント コンピューター**  
  
-   Mac OS X v10.5 Leopard  
  
-   Mac OS X v10.6 雪 Leopard  
  
-   Mac OS X v10.7 Lion  
  
-   Mac OS X v10.8 山 Lion  
  
> [!NOTE]
>  正常性と Windows Server Essentials ダッシュ ボードから、Mac コンピューターのバックアップ ステータスを表示することができます。 ただし、コンピューターのバックアップを構成またはダッシュ ボードからバックアップを開始することはできません。 さらに、リモート Web アクセスを使用して、Mac コンピューターに接続することはできません。  
  
#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  このセクションでは、Windows Server Essentials を実行しているサーバーに適用されます。 次のコンピューターのオペレーティング システムがサポートされています。  
  
 **Windows 7 オペレーティング システム**  
  
-    Windows 7 Home Basic (x86 および x64)  
  
-    Windows 7 ホーム Premium (x86 および x64)  
  
-    Windows 7 Professional (x86 および x64)  
  
-    Windows 7 Ultimate (x86 および x64)  
  
-    Windows 7 Enterprise (x86 および x64)  
  
-    Windows 7 スターター (x86)  
  
 **Windows 8 オペレーティング システム**  
  
-   Windows 8  
  
-   Windows 8 Professional  
  
-   Windows 8 Enterprise  
  
 **Windows 10 オペレーティング システム**  
  
-   Windows 10  
  
-   Windows 10 Professional  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Education  
  
 **Mac クライアント コンピューター**  
  
-   Mac OS X v10.5 Leopard  
  
-   Mac OS X v10.6 雪 Leopard  
  
-   Mac OS X v10.7 Lion  
  
> [!NOTE]
>  正常性と Windows Server Essentials ダッシュ ボードから、Mac コンピューターのバックアップ ステータスを表示することができます。 ただし、コンピューターのバックアップを構成またはダッシュ ボードからバックアップを開始することはできません。 さらに、リモート Web アクセスを使用して、Mac コンピューターに接続することはできません。  
  
###  <a name="BKMK_5"></a>サーバーが実行するクライアント コンピューターへの変更  
 コンピューターをサーバーに接続するときに、Windows Server Essentials ソフトウェアにより、いくつかの変更、コンピューターに、コンピューターとサーバーが連携できるようにします。  
  
 ソフトウェアは、次を処理します。  
  
-   コンピューターにコネクタ ソフトウェアをインストールします。  
  
-   インストールされていない場合は、コンピューターに Microsoft .NET Framework 4.5 をインストールします。  
  
-   ダッシュ ボードとスタート パッドをコンピューターのデスクトップにショートカットを作成します。  
  
-   作業には、次の機能を許可するようにコンピューターで Windows ファイアウォールのポートを構成します。  
  
    -   コア ネットワー キング  
  
    -   リモート デスクトップ サービス  
  
-   コンピューターのバックアップを容易にするために次のような変更を加えます。  
  
    -   自動バックアップを実行するスケジュールされたタスクを作成します。  
  
    -   バックアップ操作、サーバーを管理するサービスをインストールします。  
  
    -   中に使用される仮想デバイス ドライバーをインストール ファイルとフォルダーの復元プロセス  
  
-   問題を検出して、対応するアラートの通知を作成する正常性エージェントのインストールします。  
  
-   定期的な正常性評価の正常性アラート定義を同期して、コンピューター上のスケジュールされたタスクを作成します。  
  
-   サービスをコンピューター、サーバーとその他の Windows Server Essentials 機能の通信に使用すると、コンピューターに追加します。  
  
-   実行するリモート デスクトップ サービスを許可するように Windows クライアントを実行しているクライアント コンピューターで TCP ポート 3389 を開く  
  
-   クライアント コンピューター上に VPN を展開し、VPN 機能が Windows Server essentials では、有効になってまたは Windows Server Essentials で VPN 機能が有効にした場合、ワン エクスペリエンスを提供する場合、1 回のクリック エクスペリエンスを提供  
  

 お使いのコンピューターをサーバーに接続する方法については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  
  
###  <a name="BKMK_6"></a>ネットワーク ユーザー名とパスワード情報  
 サーバーの管理担当者から、ネットワーク ユーザー名とパスワード情報を取得できます。 これらの資格情報を使用して、サーバーから、サーバーとの情報にアクセスするコンピューターに接続することができます。  
  
###  <a name="BKMK_6"></a>ネットワーク ユーザー名とパスワード情報  
 サーバーの管理担当者から、ネットワーク ユーザー名とパスワード情報を取得できます。 これらの資格情報を使用して、サーバーから、サーバーとの情報にアクセスするコンピューターに接続することができます。 

  
 ユーザー アカウントを追加することで、ネットワーク資格情報を作成するには、サーバー管理者の場合は、**ユーザー**ダッシュ ボードのタブ。 ユーザー アカウントの詳細については、次を参照してください。[ダッシュ ボードを使用してユーザー アカウントの管理](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)します。  
  
###  <a name="BKMK_7"></a>サーバー管理者のアカウント  
 ネットワーク管理者アカウント名と、コネクタ ソフトウェアをインストールするためのパスワードを提供できる必要があります。 ネットワーク管理者アカウントを組織のローカル エリア ネットワークを管理するユーザーを有効にして管理し、スイッチやルーターなどネットワーク デバイスの維持に役立ちます。  
  
 ネットワーク管理者アカウントを使用して実行できるタスクを含めることができます。  
  
-   ネットワークに接続されたアプリケーションおよびその他のソフトウェアのインストール  
  
-   サーバー上の記憶域を管理します。  
  
-   ソフトウェア更新プログラムの配布  
  
-   定期的なバックアップを実行します。  
  
-   ネットワーク上の毎日のアクティビティの監視  
  
 Windows Server Essentials、Windows Server Essentials では、および Windows Server 2012 R2、Windows Server Essentials エクスペリエンス役割がインストールされて、ネットワーク管理者を割り当てることができますレベルを任意のユーザー アカウントにアクセスします。 これには、ネットワーク管理者タスクを実行する必要なアクセス許可が与えられます。 ときに、ユーザーが割り当てられている、ネットワーク管理者のアクセス レベルを**ユーザー アクセス制御**管理者のアクセス許可が必要なすべてのタスクのプロンプトを開きます。  
  
###  <a name="BKMK_8"></a>Windows ドメインからコンピューターを削除します。  
 ドメインからコンピューターを削除するには、ユーザー名とドメイン アカウントのパスワードのように求められます。  
  
##### <a name="to-remove-a-computer-from-a-windows-domain"></a>Windows ドメインからコンピューターを削除するには  
  
1.  をクリックして**開始**、右クリック**コンピューター**、] をクリックし、**プロパティ**します。  
  
2.  [**コンピューター名、ドメインおよびワークグループの設定**、] をクリックして**設定を変更する**します。  
  
    > [!NOTE]
    >  管理者のパスワードまたは確認のメッセージが表示されたら、ドメイン パスワードを入力または確認を提供します。  
  
3.  **システムのプロパティ**ダイアログ ボックスで、をクリックして、**コンピューター名**タブをクリックし、をクリックして**変更**します。  
  
4.  **コンピューター名/ドメイン名の変更**ダイアログ ボックスで、**のメンバー**、] をクリックして**ワークグループ**、次のいずれかの操作を実行します。  
  
    1.  既存のワークグループに参加させるにクリックして、参加するワークグループの名前を入力**OK**します。  
  
    2.  ワークグループを作成するには、作成、およびをクリックするワークグループの名前を入力**OK**します。  
  
        > [!NOTE]
        >  お使いのコンピューターをドメインから削除され、そのドメイン内のコンピューター アカウントが無効になります。  
  
##  <a name="BKMK_B"></a>コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。  
 このセクションでは、手順と、コネクタ ソフトウェアをインストール、コンピューターをサーバーに接続およびコンピューターをサーバーに接続のトラブルシューティングに役立つ情報へのアクセスを提供します。  
  

-   [コンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [コネクタ ソフトウェアをインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [コンピューターのデータと設定を移動手動で](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [コンピューターの展開時に複数のユーザー プロファイルを転送します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  
  
-   [コネクタ ソフトウェアをアンインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [コンピューターからの切断やコンピューターをサーバーに再接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [バックアップのスリープ状態での動作方法と、休止モード](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

-   [コンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [コネクタ ソフトウェアをインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [コンピューターのデータと設定を移動手動で](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [コンピューターの展開時に複数のユーザー プロファイルを転送します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  
  
-   [コネクタ ソフトウェアをアンインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [コンピューターからの切断やコンピューターをサーバーに再接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [バックアップのスリープ状態での動作方法と、休止モード](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

  
###  <a name="BKMK_9"></a>コンピューターをサーバーに接続します。  
 Windows Server 2012 R2 または Windows Server Essentials を実行しているサーバーにインストールされている Windows Server Essentials エクスペリエンスの役割を持つコンピューターを接続するときに、クライアント コンピューターがインターネットへの接続を有効であることを確認します。  
  
 すべてのクライアント コンピューターをサーバーに接続するには、次の手順を実行します。  
  
 手順を完了するには、次の情報が必要です。  
  
-   ユーザー名とコンピューターを新しいネットワーク上を使用する、ユーザーのパスワード  
  
-   ユーザー名とコンピューターのローカル管理者アカウントのパスワード  
  
> [!NOTE]

>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加せず、サーバーにコンピューターを接続できます。 この方法がすべてのサポートされるクライアント オペレーティング システム、およびグループ ポリシーなどの機能を利用できないと仮想プライベート ネットワーク (Vpn)、コンピューターがドメインに接続することが必要ながご利用いただけません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  

>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加せず、サーバーにコンピューターを接続できます。 この方法がすべてのサポートされるクライアント オペレーティング システム、およびグループ ポリシーなどの機能を利用できないと仮想プライベート ネットワーク (Vpn)、コンピューターがドメインに接続することが必要ながご利用いただけません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  

  
##### <a name="to-connect-a-client-computer-to-the-server"></a>クライアント コンピューターをサーバーに接続するには  
  
1.  サーバーに接続するコンピューターにログオンします。  
  
    > [!NOTE]
    >  このコンピューターに複数のユーザー アカウントがある場合は、ドキュメント、画像、およびコンピューターをサーバーに接続した後に保持する個人設定のあるユーザー アカウントを使用してログオンします。  
  
2.  Internet Explorer などのインターネット ブラウザーを開きます。  
  
3.  アドレス バーで、次のように入力します。 **http://<servername\>/Connect**、し、Enter キーを押します。  
  
    > [!NOTE]
    >  コンピューターが Windows Server Essentials ネットワークの外部のリモートの場所にある場合、サーバー ウィザードへの接続、コンピューターを実行するように入力**http://<domainname\>/connect** (< domain \ > は組織のドメイン名です)、web ブラウザーのアドレス バーにします。 ネットワーク管理者からドメイン名の情報を取得できます。  
  
4.  **コンピューターをサーバーに接続**ページが表示されます。 次のいずれかの操作を行います。  
  
    -   Windows オペレーティング システムを実行するコンピューターをクリックして**Windows 用ソフトウェアをダウンロード**します。  
  
    -   コンピューターの Mac OS X を実行しているか、後で、をクリックして**Mac 用ソフトウェアをダウンロード**します。  
  
5.  [ファイル ダウンロード セキュリティ警告メッセージ**実行**します。  
  
6.  ユーザー アカウント制御] メッセージが表示されたら、クリックして**はい**または要求された場合、ローカルのユーザー名とパスワードを入力します。  
  
7.  接続サーバー ウィザードへのコンピューターが表示されます。 ウィザードを完了するのには、次の操作を行います。  
  
    1.  使用許諾契約書をそのまま使用します。  
  
    2.  **マイ サーバーを検索**] ページで、ローカル ネットワーク内のサーバーの自動検出して、サーバーに接続するを選択します。 または、情報を使っている場合、サーバー名またはドメイン アドレスを手動で入力できます。  
  
    3.  **新しいネットワーク ユーザー名とパスワードを入力**] ページで、次の操作します。  
  
        -   これは、最初のコンピューター、サーバーに接続している場合、これは、コンピューターをサーバーの管理に使用する場合は、セットアップ中に作成した管理者アカウントを使用します。  
  
        -   その他のすべてのコンピューターに対して最初ネットワーク ユーザー アカウントを作成、サーバー上で、ダッシュ ボードを使用しています。 管理者または標準のユーザー アカウントを作成するコンピューターを使用してユーザーによって実行されるタスクに基づいて、ユーザー権限。  
  
    4.  コンピューターが Windows 8、Windows 8.1 または Windows 10 を実行している場合は、この手順をスキップします。 お使いのコンピューターには、Windows 7 が実行されていると、ドキュメントがあれば、ピクチャ、またはした後も保持する個人設定 (デスクトップの背景、スクリーン セーバー、Internet Explorer のお気に入りなど) での参加、新しいネットワークにコンピューターの場合、 **、既存のデータと設定を移動するかどうかを選択**、ウィザードのページ、**自分のデータと設定を [新しいネットワーク ユーザー アカウントに移動**します。  
  
    5.  選択でバックアップを作成するコンピューターを自動的にスリープ解除するかどうか、**バックアップ作成時にこのコンピューターをスリープ解除するかを選択**ページ。  
  
    6.  ネットワークにコンピューターを参加させるウィザードの残りの指示に従います。  
  
8.  お使いのコンピューターをネットワークに参加させた後、コンピューターにログオンする、新しいユーザー名とパスワードを使用します。  
  
    > [!NOTE]
    >  Windows 8 を初めて実行して、サーバーに接続した後、ネットワーク アカウントを使用しているコンピューターにログオンするときに、ファイルと、古いユーザー アカウントからのアプリケーションを移行する命令が表示されます。 上の指示に従って、**移行する方法はファイルやアプリケーション古いユーザー アカウントからか?**ページはすべてのファイルと、ネットワーク ユーザー アカウントにアプリケーションを移行します。  
  
9. コンピューターがサーバーに接続が正常に、スタート メニューで、(Windows 8、Windows 8.1 を実行しているコンピューターまたは Windows 10 では、ダッシュ ボードとコネクタ TrayApp は、コンピューターのスタート画面から利用可能ななります) 場合は、次のように使用できる、コネクタ TrayApp とサーバーのダッシュ ボードへのショートカットが表示されます。  
  
    -   コンピューターが Windows 8、Windows 8.1 または Windows 10 を実行している場合、ダッシュ ボードとコネクタ TrayApp なりますアプリとして検索可能。  
  
    -   コネクタ TrayApp から有効または無効にすることができます、**リモートで接続しない]**機能します。 スタート パッドを起動する TrayApp をダブルクリックすることもできます。 スタート パッドから共有フォルダーのショートカットにアクセス、コンピューターのバックアップ、アドレスのアラートを構成してリモート Web アクセス web サイトを開きます。  
  
    -   **ダッシュ ボード**、リンク サーバーを管理することができます。  
  
###  <a name="BKMK_10"></a>ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続します。  
 このトピックでは、Windows Server Essentials ネットワークにコンピューターをオンプレミス クライアント展開で Windows Server Essentials ドメインに参加させることがなく Windows 7、Windows 8、Windows 8.1 または Windows 10 コンピューターを追加する方法について説明します。 この接続方法は、Windows Server Essentials と Windows Server Essentials でサポートされます。  
  
 これは、代わりに通常の方法は、コンピューターを Windows Server Essentials ドメインに参加させる必要があります。 その方法を使用するコンピューターが別のドメイン内にある場合に削除しなければなりませんそのドメインから、Windows Server Essentials ドメインに追加する前にします。  
  
#### <a name="feature-limits"></a>機能の制限  
 クライアント コンピューターが Windows Server Essentials ドメインに追加されていないときに、一部の機能は制限されます。  
  
-   コンピューターがドメインに参加していることを必要とするすべての機能ですか? ドメイン資格情報、グループ ポリシー、および仮想プライベート ネットワーク (Vpn) を含むですか? は使用できません。  
  
-   コンピューターがドメインに参加していることを必要とするサード パーティ製のアドオンは正しく機能しません。  
  
-   このメソッドは、社外設置のコンピューターをサーバーに接続するためにことはできません。  
  
#### <a name="prerequisites"></a>前提条件  
  
-   物理ネットワークへの接続、ローカル コンピューターが必要です。  
  
-   次のオペレーティング システムのいずれかは、コンピューターにインストールする必要があります。  
  
    -   Windows 10 Pro、Windows 10 Enterprise  
  
    -    Windows 8.1 Pro、Windows 8.1 Enterprise、Windows 8 Pro、Windows 8 Enterprise  
  
    -    Windows 7 Professional (x86 および x64)、Windows 7 Enterprise (x86 および x64)、Windows 7 Ultimate (x86 および x64)  
  

-   コンピューターは、Windows Server Essentials でのクライアント コンピュータの他のすべての要件を満たす必要があります。 詳細については、次を参照してください。[コンピューターをサーバーに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)します。  

  
-   ドメインに参加せず、接続を有効にする、ローカルの Administrators グループのメンバーであるアカウントでコンピュータにサインオンする必要があります。  
  
-   Windows Server Essentials サーバーにコンピューターを接続するには、次のアカウント情報する必要があります。  
  
    -   Windows Server Essentials (ユーザーのアカウント) の管理者権限を持つアカウントです。  
  
    -   ユーザー名とコンピューターを使用したユーザーのドメイン アカウントのパスワード。 Windows Server Essentials サーバー上で、ドメイン アカウントもが管理者権限が必要です。  
  
#### <a name="connect-to-a-windows-server-essentials-network"></a>Windows Server Essentials ネットワークに接続します。  
 すべての前提条件が満たされていることを確認したら、コンピューターを Windows Server Essentials ネットワークに接続します。  
  
###### <a name="to-connect-a-computer-in-a-different-domain-to-a-windows-server-essentials-network"></a>別のドメイン内のコンピューターを Windows Server Essentials ネットワークに接続するには  
  
1.  ローカルの Administrators グループのメンバーであるアカウントを使用してクライアント コンピューターにサインオンします。  
  
2.  管理者権限を持つコマンド プロンプトを開きます。  
  
    -   Windows 10 をクリックして、**開始**ボタンを選び、**すべてのアプリ** -> **Windows システム ツール** -> **コマンド プロンプト**コマンド プロンプトで、右クリックし、[クリックして**管理者として実行**します。  
  
    -   Windows 8 での**開始**] ページで、入力**コマンド**し、Enter キーを押します。 右クリックし、結果から**コマンド プロンプト**、] をクリックし、**管理者として実行**します。  
  
    -   Windows 7、上、**開始**] メニューの [入力**コマンド**で検索ボックスに、右クリック**コマンド プロンプト**、] をクリックし、**管理者として実行**します。  
  
3.  コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    reg add "HKLM\SOFTWARE\Microsoft\Windows Server\ClientDeployment" /v SkipDomainJoin /t REG_DWORD /d 1  
    ```  
  

4.  手順を完了[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  

  
####  <a name="BKMK_SecondServer"></a>2 番目のサーバーをネットワークに参加させる  
  
###### <a name="to-join-a-second-server-to-the-network"></a>2 番目のサーバーをネットワークに参加させる  
  
1.  Windows Server Essentials ネットワークに接続するサーバーにログオンします。  
  
2.  インターネット ブラウザーを開き、アドレス バーで、次のように入力します。 **http://<servername\>/Connect**ここで、 *< servername\ >* 、Windows Server Essentials を実行しているサーバーの名前とし、Enter キーを押します。  
  
3.  Windows Server Essentials ネットワークに接続し、完了します。 しようとしているサーバー上で Internet Explorer セキュリティ強化の構成が有効になっている場合それ以外の場合、この手順をスキップします。  
  
    1.  ブロックしているメッセージを受け入れるようにクリックして**閉じる**します。  
  
    2.  追加、 **http://<servername\>/Connect**次のように信頼済み web サイトに web サイト。  
  
        1.  ブラウザー ナビゲーション ウィンドウで、をクリックして**ツール**、] をクリックし、**インターネット オプション**します。  
  
        2.  をクリックして、**セキュリティ**タブをクリックし、をクリックして**信頼済みサイト**します。  
  
        3.  をクリックして**サイト**します。  
  
        4.  Web サイトを表示する、**この web サイトをゾーンに追加**フィールド。 をクリックして**追加**します。  
  
        5.  をクリックして**閉じる**、] をクリックし、 **OK**します。  
  
    3.  Web ページを更新します。  
  

    4.  2 番目のサーバーを Windows Server Essentials を実行しているサーバーに接続するの指示に従います[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  

  
    > [!NOTE]
    >  2 番目のサーバーを Windows Server Essentials を実行しているサーバーに接続するは、次のようにクライアント コンピューターに接続しているかによって異なります。  
    >   
    >  -   ユーザー プロファイルの移行はありません。そのため、現在のプロファイルは移行されません。  
    > -   クライアント コンピューター バックアップを使用して 2 番目のサーバーをバックアップすることはできませんし、バックアップ用にコンピューターを起動するためのオプションはありません。  
  
 2 番目のサーバーを Windows Server Essentials を実行しているサーバーに参加させた後、接続されているサーバーには、次の機能が用意されています。  
  
-   更新プログラムとアラート ステータス機能は、他のクライアント コンピューターと同様に動作します。  
  
-   オンラインとオフラインの機能では、その他のクライアント コンピューターと同じ動作します。  
  
-   リモート Web アクセスを使用して、2 番目のサーバーに接続することができます。  
  
-   2 番目のサーバーは、Windows Server Essentials がこのサーバーに関連するアラートを生成するために、正常性レポートに含まれます。  
  
 Windows Server Essentials を実行しているサーバーから 2 つ目のサーバーの管理、次のように他のクライアント コンピューターの管理とは異なります。  
  
-   TrayApp、スタート パッド、およびダッシュ ボード クライアントの開始ポイントされません。  
  
-   2 番目のサーバーが内で表示されている、**サーバー**グループで、**デバイス**] タブ。  
  
-   2 番目のサーバーのクライアント コンピューターのバックアップはサポートされないために、としてバックアップの状態が表示されます。**サポートされていません**します。 さらに、2 つ目のサーバーと右クリックして選択するがない場合のバックアップおよび復元関連のタスクが 2 番目のサーバーに対して表示されます。  
  
-   2 番目のサーバーを選択し、をクリックしてかどうか、**サーバー プロパティの表示**タスクは、ない**バックアップ**] タブの [サーバーのプロパティ] ページが表示されます。  
  
-   として 2 つ目のサーバーのセキュリティの状態が表示されます、Windows Server オペレーティング システムでセキュリティ センターがないため、**該当なし**します。  
  
-   2 番目のサーバーのグループ ポリシーの状態の表示として**該当なし**します。  
  
###  <a name="BKMK_11"></a>コネクタ ソフトウェアをインストールします。  
 サーバー ウィザードへのコンピューターの接続を使用して、コンピューターをサーバーに接続すると、Windows Server essentials コネクタ ソフトウェアがインストールされます。 」と入力して、このウィザードを起動できます**http://<ServerName\>/connect** 、web ブラウザーのアドレス バーに (ここで*< ServerName\ >*は、サーバーの名前です)。  
  
> [!NOTE]
>  コンピューターがリモートの場所にある場合、サーバー ウィザードへの接続、コンピューターを実行するように入力**http://<domainname\>/connect** 、web ブラウザーのアドレス バーに (ここで*< domain > \*は、組織のドメイン名です)。 ネットワーク管理者からドメイン名の情報を取得できます。  
  
 コネクタ ソフトウェアは、次を処理します。  
  
-   コンピューターを Windows Server Essentials に接続します。  
  
-   (クライアント バックアップを作成するサーバーを構成する) 場合は毎晩、コンピューターが自動的にバックアップします。  
  
-   お使いのコンピューターのヘルスを監視する管理者に役立ちます  
  
-   構成して、自宅のコンピューターから Windows Server Essentials をリモートで管理することができます。  
  

 Windows Server Essentials サーバーにコンピューターを接続する詳細な手順については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。   

  
###  <a name="BKMK_12"></a>コンピューターのデータと設定を移動手動で  
  Windows Server Essentials と Windows Server Essentials は、Windows 7 オペレーティング システムを実行しているクライアント コンピューターに対してのみユーザー プロファイルの移行をサポートします。 Windows 7 ベースのコンピューターをサーバーに接続するときにサーバー ウィザードへのコンピューターの接続は、ユーザー プロファイルを自動的に移行することができます。  
  
 ユーザー プロファイルは、Windows 8、Windows 8.1 または Windows 10 コンピューターをサーバーに接続するときに自動的に転送できません。 ただし、Windows 8 コンピューターで、ドメインに参加しているコンピューターに、元のローカル ユーザーからのデータと設定を転送するのに Windows Easy Transfer を使用できます。 そのためには、Windows 8 の移行元コンピューターと Windows 8 展開先コンピューターの両方で、管理者があります。 Windows Easy Transfer を使用して、ファイルと設定を転送する方法については、次を参照してください。[記事 2735227](https://support.microsoft.com/kb/2735227) 、Microsoft サポート技術情報でします。  
  
###  <a name="BKMK_Transfer"></a>コンピューターの展開時に複数のユーザー プロファイルを転送します。  
 Windows Server Essentials サーバーに Windows 7 または Windows 7 SP1 オペレーティング システムを実行しているコンピューターを接続する前に転送するためにするには複数のローカル ユーザー プロファイル、ネットワーク ユーザー アカウントに対応サーバー上に作成します。 ネットワーク ユーザー アカウントの作成の詳細については、次を参照してください。[ユーザー アカウントを追加](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)します。  
  
 ユーザー プロファイルの移行は (Windows Server Essentials) 用 Windows 7 または Windows 7 SP1 (Windows Server Essentials) を実行するコンピューターでのみサポートされます。 コンピューターをサーバー ウィザードへの接続、コンピューターを使用して、Windows Server Essentials サーバーに接続するときに、新しいネットワーク ユーザー アカウントにユーザー データと古いユーザー ローカル アカウントの設定を移動するオプションが提供されます。 そのためには、上、**既存のユーザー データと設定を移動**ページ、ウィザードのクライアント コンピューター上にある複数のユーザー プロファイルを転送するコンピューター上に存在するローカル ユーザー アカウントに、ネットワーク ユーザー アカウントにマップします。  
  
###  <a name="BKMK_13"></a>コネクタ ソフトウェアをアンインストールします。  
 コンピューターからコネクタ ソフトウェアをアンインストールするには、コントロール パネルを使用します。 コネクタ ソフトウェアに問題がある場合、または新しいバージョンのコネクタ ソフトウェアをインストールする必要がある場合、これを行う通常されます。 この手順を実行する管理者としてコンピューターにログオンする必要があります。  
  
> [!IMPORTANT]
>  クライアント コンピューター上のオペレーティング システムをアップグレードする場合、コネクタ ソフトウェアが自動的にアンインストールされます。 アップグレードが完了した後、コネクタ ソフトウェアを再インストールする必要があります。 オペレーティング システムをアップグレードする前に、コネクタ ソフトウェアをアンインストールすることをお勧めします。 まだ容認可能です。 には、アップグレードが完了した後、コネクタ ソフトウェアをアンインストールします。ただし、その可能性があります、サーバーとクライアント コンピューター間の不整合な状態に、コネクタ ソフトウェアをアンインストールして再インストールされるまで。  
  
##### <a name="to-uninstall-connector-software-from-a-computer"></a>コンピューターからコネクタ ソフトウェアをアンインストールするには  
  
1.  Windows 7、Windows 8、Windows 8.1 または Windows 10 を実行しているコンピューターからを起動**コントロール パネルの [**、し、**プログラム**セクションで、をクリックして**ビューには、更新プログラムがインストールされている**します。  
  
2.  インストールされているプログラムの一覧から選択**Windows Server Essentials Connector**、] をクリックし、**アンインストール**します。  
  
3.  [警告] ページで、をクリックして**はい**します。  
  
4.  場合、**ユーザー アカウント制御**ウィンドウが表示されたら、] をクリックして**許可**します。  
  
5.  、Windows Server Essentials の場合は、Windows Server Essentials Connector ページをスタート パッドを閉じるように提案が表示されたら、] をクリックして**OK**します。  
  
6.  プログラムをアンインストールするを待ちます。 ソフトウェアが削除されると**Windows Server Essentials Connector**インストールされているプログラムや更新プログラムの一覧に表示されなくなります。 さらに、スタート パッドとダッシュ ボードへのショートカットは不要になったコンピューターのデスクトップに表示されます。  
  
> [!NOTE]
>  -   コネクタ ソフトウェアをアンインストールしないコンピューターは削除されませんで表示されているコンピューターの一覧から、**デバイス**ダッシュ ボードのタブ。 ダッシュ ボードからコンピューターを削除するを参照してください。[コンピューターをサーバーから削除](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)します。  
> -   コネクタ ソフトウェアをアンインストールすると、サーバーにマッピングされていた、クライアント コンピューター上の共有のフォルダーは削除されません。 サーバーにマッピングされている共有フォルダーを手動で削除する必要があります。  

> -   コネクタ ソフトウェアをアンインストールしても、元のドメインを削除するコンピューターことはありません。 ドメインからコンピューターを手動で参加解除する必要があります。 手順については、次を参照してください。[コンピューターを Windows ドメインから削除](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)します。  

  
###  <a name="BKMK_14"></a>コンピューターからの切断やコンピューターをサーバーに再接続  
 サーバーからコンピューターを切断するには、次の手順を実行する必要があります。  
  

1.  コントロール パネルを使用して、コンピューターからコネクタ ソフトウェアをアンインストールします。 手順については、次を参照してください。[コネクタ ソフトウェアをアンインストール](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)します。   

  
2.  Windows Server Essentials ドメインからコンピューターを削除し、ワークグループに参加させます。 Windows をワークグループに参加させるための詳細な手順について[への参加またはワークグループを作成する](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)します。  
  
3.  ダッシュ ボードを使用して、サーバーからコンピューターを削除します。 手順については、次を参照してください。[コンピューターをサーバーから削除](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)します。  
  
 再接続するには、Windows Server Essentials サーバー ネットワークから切断されていた以前のサーバーにコンピューターには、次の手順を実行する必要があります。  
  

1.  コントロール パネルを使用して、コンピューターからコネクタ ソフトウェアをアンインストールします。 手順については、次を参照してください。[コネクタ ソフトウェアをアンインストール](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)します。  
  
2.  Windows Server Essentials ドメインからコンピューターを削除し、ワークグループに参加させます。 Windows をワークグループに参加させるための詳細な手順について[への参加またはワークグループを作成する](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)します。  
  
3.  コンピューターの接続ウィザードを使用して、コンピューターをサーバーに接続します。 手順については、次を参照してください。[コンピューター、サーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  
  
###  <a name="BKMK_Sleep"></a>バックアップのスリープ状態での動作方法と、休止モード  
 選択した場合、**バックアップ用のコンピューターのスリープ解除**オプションは、コンピューター、サーバーにコンピューターを接続する場合は自動的にスリープ状態から復帰または休止モード毎日のバックアップのスケジュールで指定されているバックアップをできるようにします。 バックアップが完了したら、コンピューターはスリープ状態または休止モード、電源管理設定に基づいてに返します。 このオプションを選択しない場合、サーバーはバックアップされませんコンピューター、コンピューターがスリープまたは休止状態にならない場合。 詳細については、次を参照してください。[クライアント バックアップの管理](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)します。  
  
##  <a name="BKMK_C"></a>スタート パッドを使用します。  
 スタート パッドを使用するには、Windows Server Essentials サーバーから共有リソースにアクセスし、コンピューターのバックアップを実行し、システム正常性アラートに応答します。  
  
-   [スタート パッドの概要](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)  
  
-   [Mac コンピューターでスタート パッドを使用します。](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  
  
## <a name="see-also"></a>参照してください。  
  
-   [コンピューターをサーバーに接続のトラブルシューティングします。](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md)  
  
-   [ユーザー アカウントを管理します。](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  

-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモート操作します。](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [デジタル メディアを再生します。](Play-Digital-Media-in-Windows-Server-Essentials.md)

-   [共有フォルダーの使用](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモート操作します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [デジタル メディアを再生します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)

