---
title: Windows Server Essentials の接続
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: 98292e0715ea662712e596d89646a735e22ba3f9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435975"
---
# <a name="get-connected-in-windows-server-essentials"></a>Windows Server Essentials の接続

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 コネクタ ソフトウェアを使用して、コンピューターを Windows Server Essentials サーバーに接続できます。 コンピューターをサーバーに接続ウィザードを使用して、コンピューターをサーバーに接続したときに、コネクタ ソフトウェアがインストールされます。 このウィザードを開始するには」と入力して**http://<servername\>/connect**ここで、 **< servername\>** サーバーの名前を指定します。  

 このトピックの内容:  


-   [コンピューターをサーバーに接続するための準備します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [スタート パッドを使用します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

-   [コンピューターをサーバーに接続するための準備します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [スタート パッドを使用します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  


##  <a name="BKMK_A"></a> コンピューターをサーバーに接続するための準備します。  
 このセクションでは、コネクタ ソフトウェア、Windows Server Essentials がサポートするオペレーティング システム、コンピューターをサーバーに接続する前に完了する必要がある前提条件となるタスク、コネクタ ソフトウェアを実行するときに、コンピューターに対してサーバーが実行する変更について説明します。  


-   [コネクタ ソフトウェアの概要](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [コンピューターをサーバーに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Mac コンピューターをネットワークに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [クライアント コンピューターのサポートされるオペレーティング システム](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [サーバーがクライアント コンピューターに加える変更](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [ネットワーク ユーザー名とパスワード情報](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [サーバー管理者のアカウント](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Windows ドメインからコンピューターを削除します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a> コネクタ ソフトウェアの概要  
 Windows Server Essentials オペレーティング システム用のコネクタ ソフトウェアは、Windows Server Essentials サーバーをネットワーク内のコンピューターに接続します。 コンピューターをサーバーに接続すると、コネクタ ソフトウェアは自動的にコンピューターをバックアップし、正常性の監視を有効にします。 またコネクタ ソフトウェアにより、Windows Server Essentials サーバーの構成とリモート管理も可能になります。 クライアント コンピューターをサーバーに接続すると、コネクタ ソフトウェアがインストールされます。 クライアント コンピューターを Windows Server Essentials サーバーに接続する詳細な手順については、このトピックで後述する「[コンピューターのサーバーへの接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。  

-   [コネクタ ソフトウェアの概要](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [コンピューターをサーバーに接続するための前提条件](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Mac コンピューターをネットワークに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [クライアント コンピューターのサポートされるオペレーティング システム](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [サーバーがクライアント コンピューターに加える変更](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [ネットワーク ユーザー名とパスワード情報](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [サーバー管理者のアカウント](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Windows ドメインからコンピューターを削除します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a> コネクタ ソフトウェアの概要  
 Windows Server Essentials オペレーティング システム用のコネクタ ソフトウェアは、Windows Server Essentials サーバーをネットワーク内のコンピューターに接続します。 コンピューターをサーバーに接続すると、コネクタ ソフトウェアは自動的にコンピューターをバックアップし、正常性の監視を有効にします。 またコネクタ ソフトウェアにより、Windows Server Essentials サーバーの構成とリモート管理も可能になります。 クライアント コンピューターをサーバーに接続すると、コネクタ ソフトウェアがインストールされます。 クライアント コンピューターを Windows Server Essentials サーバーに接続する詳細な手順については、このトピックで後述する「[コンピューターのサーバーへの接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。  


###  <a name="BKMK_2"></a> コンピューターをサーバーに接続するための前提条件  
 コンピューターをネットワークに接続する前に、次の要件を満たす必要があります。  

-   Windows Server Essentials のインストールが完了し、サーバーが実行されている。 コネクタ ソフトウェアは、サーバーと通信することができない場合、インストールを終了します。  


-   クライアント コンピューターが、サポートされているオペレーティング システムを実行している。 詳細については、次を参照してください。[クライアント コンピューターのオペレーティング システムでサポートされる](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)します。


-   クライアント コンピューターが、インターネットへの有効な接続を確立している。  

-   クライアント コンピューターがサーバーと同じネットワーク上にある場合、クライアント コンピューターは、Windows Server Essentials を実行しているサーバーと同じ IP サブネット上に存在している。  

-   クライアント コンピューターに .NET Framework 4.5 がインストールされている。 コネクタ ソフトウェアは、コンピューターにこのソフトを自動的にインストールします。  

-   クライアント コンピューターが、次の最小システム要件を満たしている。  

    -   1.4 GHz 以上のプロセッサ  

    -   1 GB 以上の RAM  

    -   ハード ドライブの空き容量 1 GB (この容量の一部はインストール後に解放されます)  

-   ブート パーティション (Windows オペレーティング システムインストールされているディスク パーティション) が NTFS ファイル システムでフォーマットされている。  

-   コンピューター名は、15 文字以内で指定する。  

-   コンピューター名に、アンダースコア (_) が使用されていない。  

-   コンピューターの日付と時刻の設定が、サーバーの設定に合わせて調整されている。  

-   クライアント コンピューターが特定の時点で接続できる Windows Server Essentials サーバーは 1 台だけである。  

-   既に別の Active Directory ドメインに参加しているクライアント コンピューターは、Windows Server Essentials ドメインに参加できない。  

> [!NOTE]
> 
>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加することがなくサーバーにコンピューターを接続できます。 この方法は、サポート対象のすべてのクライアント オペレーティング システムで使用できるわけではありません。また、コンピューターをドメインに接続する必要がある、グループ ポリシーや仮想プライベート ネットワーク (VPN) などの機能は使用できません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  

 Windows Server Essentials を実行しているサーバーにコンピューターを接続する詳細な手順については、「[コンピューターをサーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。  

>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加することがなくサーバーにコンピューターを接続できます。 この方法は、サポート対象のすべてのクライアント オペレーティング システムで使用できるわけではありません。また、コンピューターをドメインに接続する必要がある、グループ ポリシーや仮想プライベート ネットワーク (VPN) などの機能は使用できません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  

 Windows Server Essentials を実行しているサーバーにコンピューターを接続する詳細な手順については、「[コンピューターをサーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。  


###  <a name="BKMK_3"></a> Mac コンピューターをネットワークに接続するための前提条件  
 Mac コンピューターをネットワークに接続する前に、次の要件を満たす必要があります。  

-   サーバーのオペレーティング システムのインストールが完了し、サーバーが実行されている。 コネクタ ソフトウェアがサーバーと通信できない場合、インストールは実行されません。  

-   コンピューターで Mac OS X 10.5 (Leopard) 以降が実行されている。  

-   コンピューターがサーバーと同じ IP サブネット上にある。  

-   コンピューターが、インターネットへの有効な接続を確立している。  

-   コンピューターが、次の最小システム要件を満たしている。  

    -   1.4 GHz 以上のプロセッサ  

    -   1 GB 以上の RAM  

    -   ハード ドライブの空き容量 1 GB (この容量の一部はインストール後に解放されます)  

-   クライアント コンピューターが特定の時点で接続できるサーバーは 1 台だけである。  

###  <a name="BKMK_4"></a> クライアント コンピューターのサポートされるオペレーティング システム  
 Windows Server Essentials は、すべてのサポートされているクライアント コンピューターに同じ機能セットを提供します。 これらの機能には、ドメインへの参加、スタート パッド、およびクライアント側の正常性通知が含まれます。  

> [!IMPORTANT]
>  Windows Server Essentials は、Windows の Home、Starter、または Media Center の各バージョンを実行しているコンピューターのドメインへの参加をサポートしません。 さらに、リモート Web アクセスを使ってこれらのコンピューターに接続することはできません。  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  このセクションでは、Windows Server Essentials を実行するサーバーまたは Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter を実行するサーバーに適用されます。 次のコンピューター オペレーティング システムがサポートされています:  

 **Windows 7 オペレーティング システム**  

- Windows 7 Home Basic SP1 (x 86 および x64)  

- Windows 7 Home Premium SP1 (x86 および x64)  

- (X 86 および x64)、Windows 7 Professional SP1  

- (X 86 および x64)、Windows 7 Ultimate SP1  

- (X 86 および x64)、Windows 7 Enterprise SP1  

- Windows 7 Starter の SP1 (x86)  

  **Windows 8 オペレーティング システム**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **Windows 8.1 オペレーティング システム**  

- Windows 8.1  

- Windows 8.1 Pro  

- Windows 8.1 Enterprise  

  **Windows 10 オペレーティング システム**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Mac クライアント コンピューター**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

- Mac OS X v10.8 Mountain Lion  

> [!NOTE]
>  正常性と、Windows Server Essentials ダッシュ ボードから Mac コンピューター用のバックアップの状態を表示することができます。 ただし、ダッシュボードからコンピューター バックアップを構成したり、バックアップを開始したりすることはできません。 さらに、リモート Web アクセスを使って Mac コンピューターに接続することはできません。  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  このセクションでは、Windows Server Essentials を実行しているサーバーに適用されます。 次のコンピューター オペレーティング システムがサポートされています:  

 **Windows 7 オペレーティング システム**  

- Windows 7 Home Basic (x86 および x64)  

- Windows 7 Home Premium (x86 および x64)  

- Windows 7 Professional (x86 および x64)  

- Windows 7 Ultimate (x86 および x64)  

- Windows 7 Enterprise (x86 および x64)  

- Windows 7 Starter (x86)  

  **Windows 8 オペレーティング システム**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **Windows 10 オペレーティング システム**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Mac クライアント コンピューター**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

> [!NOTE]
>  Mac コンピューターの正常性とバックアップの状態は、Windows Server Essentials ダッシュボードから確認できます。 ただし、ダッシュボードからコンピューター バックアップを構成したり、バックアップを開始したりすることはできません。 さらに、リモート Web アクセスを使って Mac コンピューターに接続することはできません。  

###  <a name="BKMK_5"></a> サーバーがクライアント コンピューターに加える変更  
 コンピューターをサーバーに接続する場合、コンピューターとサーバーが連携できるように、Windows Server Essentials ソフトウェアにより、コンピューターに多数の変更が実行されます。  

 このソフトウェアは以下の処理を実行します。  

-   コンピューターにコネクタ ソフトウェアをインストールする  

-   インストールされていない場合は、コンピューターに Microsoft .NET Framework 4.5 をインストールする  

-   ダッシュボードとスタート パッドのショートカットをコンピューターのデスクトップに作成する  

-   次の機能が動作するように、コンピューター上で Windows ファイアウォール ポートを構成する  

    -   コア ネットワーキング  

    -   リモート デスクトップ サービス  

-   バックアップを容易にするため、次の変更を実行します。  

    -   自動バックアップを実行する、スケジュールされたタスクを作成する  

    -   バックアップ操作を管理するサービスをサーバーにインストールする  

    -   ファイルとフォルダーの復元プロセス中に使用される仮想デバイス ドライバーをインストールする  

-   問題を検出し、対応するアラート通知を作成する正常性エージェントをインストールする  

-   正常性評価を繰り返し実行し、正常性アラート定義と同期させるスケジュールされたタスクをコンピューター上で作成する  

-   サーバーや他の Windows Server Essentials 機能と通信するためにコンピューターが使用するサービスを、コンピューターに追加する  

-   リモート デスクトップ サービスが使用できるように、Windows クライアントを実行しているクライアント コンピューターで TCP ポート 3389 を開く  

-   クライアント コンピューターに VPN を展開し、VPN の機能または Windows Server essentials では、有効ですが、Windows Server Essentials で VPN 機能が有効な場合に自動接続エクスペリエンスが提供される場合は、1 回のクリック エクスペリエンスを提供します  


 コンピューターをサーバーに接続するための詳細については、「[コンピューターをサーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。  

###  <a name="BKMK_6"></a> ネットワーク ユーザー名とパスワード情報  
 サーバーの管理担当者から、ネットワーク ユーザー名とパスワード情報を入手できます。 これらの資格情報を使用すると、コンピューターをサーバーに接続し、サーバーからの情報にアクセスすることができます。  

###  <a name="BKMK_6"></a> ネットワーク ユーザー名とパスワード情報  
 サーバーの管理担当者から、ネットワーク ユーザー名とパスワード情報を入手できます。 これらの資格情報を使用すると、コンピューターをサーバーに接続し、サーバーからの情報にアクセスすることができます。 


 サーバー管理者は、ダッシュボードの **[ユーザー]** タブからユーザー アカウントを追加することで、ネットワーク資格情報を作成できます。 ユーザー アカウントの詳細については、「[ダッシュボードを使用したユーザー アカウントの管理](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)」を参照してください。  

###  <a name="BKMK_7"></a> サーバー管理者のアカウント  
 コネクタ ソフトウェアをインストールするには、ネットワーク管理者アカウントの名前とパスワードを入力する必要があります。 ネットワーク管理者アカウントを使用すると、組織のローカル エリア ネットワークを管理し、スイッチやルーターなどのネットワーク デバイスの管理と保守を行うことができます。  

 ネットワーク管理者アカウントを使用して実行できるタスクには、以下のタスクがあります。  

- ネットワーク対応のアプリケーションおよびその他のソフトウェアのインストール  

- サーバー上の記憶域の管理  

- ソフトウェア更新プログラムの配布  

- 定期的なバックアップの実行  

- ネットワーク上の毎日のアクティビティの監視  

  Windows Server Essentials、Windows Server Essentials、および Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 の場合は、ネットワーク管理者を割り当てることができますアクセス レベルを任意のユーザー アカウント。 これにより、ネットワーク管理者タスクを実行するために必要なアクセス許可が与えられます。 ユーザーにネットワーク管理者のアクセス レベルが割り当てられると、管理者のアクセス許可が必要なタスクに対して、 **[ユーザーアクセス制御]** プロンプトが開きます。  

###  <a name="BKMK_8"></a> Windows ドメインからコンピューターを削除します。  
 ドメインからコンピューターを削除するには、ドメイン アカウントのユーザー名とパスワードの入力が必要です。  

##### <a name="to-remove-a-computer-from-a-windows-domain"></a>Windows ドメインからコンピューターを削除するには  

1.  **[スタート]** ボタンをクリックし、 **[コンピューター]** を右クリックし、 **[プロパティ]** をクリックします。  

2.  **[コンピューター名、ドメインおよびワークグループの設定]** で **[設定の変更]** をクリックします。  

    > [!NOTE]
    >  管理者パスワードの入力または確認を求められた場合は、ドメイン パスワードを入力するか、確認を実行します。  

3.  **[システムのプロパティ]** ダイアログ ボックスで **[コンピューター名]** タブをクリックし、 **[変更]** をクリックします。  

4.  **[コンピューター名/ドメイン名の変更]** ダイアログ ボックスの **[所属するグループ]** の下で **[ワークグループ]** をクリックし、次のいずれかの操作を実行します。  

    1.  既存のワークグループに参加するには、参加するワークグループの名前を入力し、 **[OK]** をクリックします。  

    2.  ワークグループを作成するには、作成するワークグループの名前を入力し、 **[OK]** をクリックします。  

        > [!NOTE]
        >  コンピューターがドメインから削除され、そのドメインのコンピューター アカウントが無効になります。  

##  <a name="BKMK_B"></a> コネクタ ソフトウェアを使用してコンピューターをサーバーに接続します。  
 ここでは、コネクタ ソフトウェアのインストール、サーバーへのコンピューターの接続、およびコンピューターをサーバーに接続する際のトラブルシューティングに役に立つ手順と情報へのアクセスを提供します。  


-   [コンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [コンピューターをドメインに参加することがなく、Windows Server Essentials サーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [コネクタ ソフトウェアをインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [コンピューターのデータと設定を移動手動で](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [コンピューターの展開中に複数のユーザー プロファイルを転送します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [コネクタ ソフトウェアをアンインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [コンピューターから切断するか、コンピューターをサーバーに再接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [バックアップのスリープ状態と動作方法と、休止モード](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

-   [コンピューターをサーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [コンピューターをドメインに参加することがなく、Windows Server Essentials サーバーに接続します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [コネクタ ソフトウェアをインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [コンピューターのデータと設定を移動手動で](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [コンピューターの展開中に複数のユーザー プロファイルを転送します。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [コネクタ ソフトウェアをアンインストールします。](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [コンピューターから切断するか、コンピューターをサーバーに再接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [バックアップのスリープ状態と動作方法と、休止モード](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  


###  <a name="BKMK_9"></a> コンピューターをサーバーに接続します。  
 Windows Server Essentials を実行しているサーバーまたは Windows Server 2012 R2 に Windows Server Essentials エクスペリエンス役割がインストールされたコンピューターを接続するときに、クライアント コンピューターにインターネットへの接続を有効にするを確認します。  

 クライアント コンピューターをサーバーに接続するため、次の手順をすべてのクライアント コンピューターで完了します。  

 この手順を完了するには、次の情報が必要です。  

-   新しいネットワークでコンピューターを使用するユーザーのユーザー名とパスワード  

-   コンピューターのローカル管理者アカウントのユーザー名とパスワード  

> [!NOTE]
> 
>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加することがなくサーバーにコンピューターを接続できます。 この方法は、サポート対象のすべてのクライアント オペレーティング システムで使用できるわけではありません。また、コンピューターをドメインに接続する必要がある、グループ ポリシーや仮想プライベート ネットワーク (VPN) などの機能は使用できません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  
> 
>  Windows Server Essentials または Windows Server Essentials のオンプレミス クライアント展開では、Windows Server Essentials ドメインに追加することがなくサーバーにコンピューターを接続できます。 この方法は、サポート対象のすべてのクライアント オペレーティング システムで使用できるわけではありません。また、コンピューターをドメインに接続する必要がある、グループ ポリシーや仮想プライベート ネットワーク (VPN) などの機能は使用できません。 要件と手順については、次を参照してください。[ドメインに参加せず、Windows Server Essentials サーバーにコンピューターを接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)します。  


##### <a name="to-connect-a-client-computer-to-the-server"></a>クライアント コンピューターをサーバーに接続するには  

1.  サーバーに接続するコンピューターにログオンします。  

    > [!NOTE]
    >  このコンピューターに複数のユーザー アカウントがある場合は、コンピューターをサーバーに接続した後もドキュメント、ピクチャ、個人設定を残しておくユーザー アカウントを使用してログオンしてください。  

2.  Internet Explorer などのインターネット ブラウザーを開きます。  

3.  アドレス バーに「 **http://<servername\>/connect**、し、Enter キーを押します。  

    > [!NOTE]
    >  コンピューターがリモートの場所、Windows Server Essentials ネットワークの外部にある場合は、サーバーのウィザード、コンピューターに接続を実行する入力**http://<domainname\>/connect** web ブラウザー (のアドレス バーに場所 < ドメイン\>組織のドメイン名です)。 ドメイン名情報はネットワーク管理者から取得できます。  

4.  **[コンピューターをサーバーに接続]** ページが表示されます。 次のいずれかの操作を行います。  

    -   Windows オペレーティング システムを実行しているコンピューターの場合は、 **[Windows 用ソフトウェアをダウンロード]** をクリックします。  

    -   Mac OS X 以降が実行されているコンピューターの場合は、 **[Mac 用ソフトウェアをダウンロード]** をクリックします。  

5.  ファイルのダウンロードに関するセキュリティ警告メッセージで **[実行]** をクリックします。  

6.  [ユーザー アカウント制御] メッセージが表示されたら、 **[はい]** をクリックするか、必要に応じてローカル ユーザー名とパスワードを入力します。  

7.  コンピューターをサーバーに接続ウィザードが表示されます。 次の作業を行ってウィザードを完了します。  

    1.  エンド ユーザー ライセンス契約に同意します。  

    2.  **[マイ サーバーを検索する]** ページで、ローカル ネットワーク内のサーバーが自動検出されます。接続するサーバーを選択します。 または、情報を入手している場合は、サーバーの名前またはドメイン アドレスを手動で入力することもできます。  

    3.  **[新しいネットワーク ユーザー名およびパスワードの入力]** ページで、以下のように入力します。  

        -   このコンピューターがサーバーに接続する最初のコンピューターであり、このコンピューターをサーバーの管理に使用する場合は、セットアップ中に作成した管理者アカウントを使用します。  

        -   それ以外のコンピューターの場合はすべて、まずダッシュボードを使用してサーバー上にネットワーク ユーザー アカウントを作成します。 コンピューターを使用するユーザーが実行するタスクに応じて、管理者または標準のユーザー特権を持つユーザー アカウントを作成してください。  

    4.  Windows 8、Windows 8.1 または Windows 10 コンピューターを実行する場合は、この手順をスキップします。 コンピューターで Windows 7 が実行されていて、コンピューターを新しいネットワークに参加させた後も残しておきたいドキュメント、ピクチャ、または個人設定 (デスクトップの背景、スクリーン セーバー、Internet Explorer のお気に入りなど) がある場合は、ウィザードの **[既存のデータと設定を移動する場合に選択します]** ページで、 **[自分のネットワーク ユーザー アカウントに自分のデータと設定を移動する]** をオンにします。  

    5.  **[バックアップ作成時にこのコンピューターをスリープ解除する場合、選択します]** ページで、バックアップを作成するためにコンピューターを自動的にスリープ解除するかどうかを選択します。  

    6.  ウィザードの以降の指示に従って、コンピューターをネットワークに参加させます。  

8.  コンピューターをネットワークに参加させたら、新しいユーザー名とパスワードを使用してコンピューターにログオンします。  

    > [!NOTE]
    >  Windows 8 を実行しているコンピューターをサーバーに接続した後、ネットワーク アカウントを使用して初めてこのコンピューターにログオンすると、古いユーザー アカウントからファイルとアプリケーションを移行するように促す指示が表示されます。 **[古いユーザー アカウントからファイルとアプリケーションを移行する方法]** ページの指示に従って、すべてのファイルとアプリケーションをネットワーク ユーザー アカウントに移行します。  

9. (コンピューターには、Windows 8、Windows 8.1 または Windows 10、ダッシュ ボードとコネクタが実行されている場合は、次のように使用できる [スタート] メニューに、コネクタ TrayApp とサーバーのダッシュ ボードへのショートカットが表示されます、コンピューターが、サーバーに正常に接続、TrayApp 使用できるコンピューターのスタート画面から)。  

    -   Windows 8、Windows 8.1 または Windows 10 コンピューターを実行する場合、ダッシュ ボードとコネクタ TrayApp がアプリとして検索が可能になります。  

    -   コネクタ TrayApp から **[リモート接続を維持する]** 機能を有効または無効にすることができます。 また、TrayApp をダブルクリックして、スタート パッドを起動することもできます。 スタート パッドから共有フォルダーのショートカットにアクセスし、コンピューターのバックアップを構成し、アラートへの対処を行い、リモート Web アクセス Web サイトを開くことができます。  

    -   **[ダッシュボード]** リンクから、サーバーを管理することができます。  

###  <a name="BKMK_10"></a> コンピューターをドメインに参加することがなく、Windows Server Essentials サーバーに接続します。  
 このトピックでは、Windows Server Essentials ネットワークにコンピューターをオンプレミス クライアント展開で Windows Server Essentials ドメインに参加させることがなく Windows 7、Windows 8、Windows 8.1 または Windows 10 コンピューターを追加する方法について説明します。 この接続方法は、Windows Server Essentials と Windows Server Essentials でサポートされます。  

 これは、通常の方法に置き換わる方法で、コンピューターを Windows Server Essentials ドメインに参加させる必要があります。 この方法を使うと、コンピューターが別のドメインにある場合、コンピューターを Windows Server Essentials ドメインに追加する前に、そのドメインからコンピューターを削除する必要があります。  

#### <a name="feature-limits"></a>機能の制限  
 クライアント コンピューターが Windows Server Essentials ドメインに追加されていない場合、一部の機能が制限されます。  

-   コンピューターをドメインに参加することが必要なすべての機能ですか? ドメインの資格情報、グループ ポリシー、仮想プライベート ネットワーク (Vpn) などですか? は使用できません。  

-   コンピューターがドメインに参加していることが必要なサード パーティ製のアドオンは、正しく機能しません。  

-   この方法は、社外設置のコンピューターをサーバーに接続するためには使用できません。  

#### <a name="prerequisites"></a>前提条件  

-   コンピューターは、ローカル ネットワークへの物理的な接続が必要です。  

-   コンピューターに次のオペレーティング システムのいずれかをインストールする必要があります。  

    -   Windows 10 Pro、Windows 10 Enterprise  

    -    Windows 8.1 Pro、Windows 8.1 Enterprise、Windows 8 Pro、Windows 8 Enterprise  

    -    Windows 7 Professional (x86 および x64)、Windows 7 Enterprise (x86 および x64)、Windows 7 Ultimate (x86 および x64)  


-   コンピューターは、Windows Server Essentials のクライアント コンピューターの他のすべての要件を満たす必要があります。 詳細については、次を参照してください。[コンピューターをサーバーに接続するための前提条件](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)します。  


-   ドメインに参加せずに接続を有効にするには、ローカルの Administrators グループのメンバーであるアカウントを使用して、コンピューターにサインオンする必要があります。  

-   コンピューターを Windows Server Essentials サーバーに接続するには、次のアカウント情報が必要です。  

    -   Windows Server Essentials の管理者権限を持つアカウント (ユーザーのアカウント)。  

    -   コンピューターを使用するユーザーのドメイン アカウントのユーザー名とパスワード。 ドメイン アカウントは、Windows Server Essentials サーバーの管理者権限が必要です。  

#### <a name="connect-to-a-windows-server-essentials-network"></a>Windows Server Essentials ネットワークへの接続  
 すべての前提条件が満たされていることを確認できたら、コンピューターを Windows Server Essentials ネットワークに接続します。  

###### <a name="to-connect-a-computer-in-a-different-domain-to-a-windows-server-essentials-network"></a>別のドメイン内のコンピューターを Windows Server Essentials ネットワークに接続するには  

1.  ローカルの Administrators グループのメンバーであるアカウントを使用して、クライアント コンピューターにサインオンします。  

2.  管理者権限を使って、コマンド プロンプトを開きます。  

    -   Windows 10 では、クリックして、**開始**ボタンを選択**すべてのアプリ** -> **Windows システム ツール** -> **コマンド プロンプト**コマンド プロンプトを右クリックし、クリックして**管理者として実行**します。  

    -   Windows 8 での**開始**ページで、入力**コマンド**し、Enter キーを押します。 結果で **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。  

    -   Windows 7 での**開始**] メニューの [入力**コマンド**、検索ボックスで右クリック**コマンド プロンプト**、順にクリックします**を管理者として実行**.  

3.  コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  

    ```  
    reg add "HKLM\SOFTWARE\Microsoft\Windows Server\ClientDeployment" /v SkipDomainJoin /t REG_DWORD /d 1  
    ```  


4.  「[コンピューターをサーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」の手順を完了します。  


####  <a name="BKMK_SecondServer"></a> 2 番目のサーバーをネットワークに参加させる  

###### <a name="to-join-a-second-server-to-the-network"></a>2 番目のサーバーをネットワークに参加させるには  

1.  Windows Server Essentials ネットワークに接続するサーバーにログオンします。  

2.  インターネット ブラウザーを開き、アドレス バーに「 **http://<servername\>/connect**ここで、 *< servername\>*  Windows Server を実行するサーバーの名前を指定しますEssentials、および Enter キーを押します。  

3.  Windows Server Essentials ネットワークに接続するサーバー上で Internet Explorer のセキュリティ強化の構成が有効の場合、以下の手順を完了します。それ以外の場合は、この手順をスキップします。  

    1.  ブロックしているメッセージは、そのまま **[閉じる]** をクリックします。  

    2.  追加、 **http://<servername\>/connect**次のように、信頼できる web サイトを web サイト。  

        1.  ブラウザー ナビゲーション ウィンドウで **[ツール]** をクリックし、 **[インターネット オプション]** をクリックします。  

        2.  **[セキュリティ]** タブをクリックし、 **[信頼済みサイト]** をクリックします。  

        3.  **[サイト]** をクリックします。  

        4.  Web サイトが **[この Web サイトをゾーンに追加する]** フィールドに表示されます。 **[追加]** をクリックします。  

        5.  **[閉じる]** をクリックし、 **[OK]** をクリックします。  

    3.  Web ページを更新します。  


    4.  Windows Server Essentials を実行しているサーバーを 2 番目のサーバーに接続するには、「[コンピューターをサーバーに接続](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」の手順に従います。  


~~~
> [!NOTE]
>  Connecting a second server to a server running Windows Server Essentials differs from connecting to a client computer as follows:  
>   
>  -   There is no user profile migration; therefore, the current profile will not be migrated.  
> -   You cannot back up the second server by using client computer backup, and there is no option to wake up the computer for backup.  
~~~

 Windows Server Essentials を実行しているサーバーに、2 番目のサーバーを参加させた後、接続されているサーバーに次の機能が提供されます。  

- 更新プログラムとアラート ステータス機能は、他のクライアント コンピューターと同じように動作します。  

- オンラインとオフラインの機能は、他のクライアント コンピューターと同じように動作します。  

- リモート Web アクセスを使用して、2 番目のサーバーに接続することができます。  

- 正常性レポートに 2 番目のサーバーが含まれるようになります。これは、Windows Server Essentials がこのサーバーに関連するアラートを生成するためです。  

  Windows Server Essentials を実行しているサーバーからの 2 番目のサーバーの管理は、他のクライアント コンピューターの管理と次の点が異なります。  

- TrayApp、スタート パッド、およびダッシュボード クライアントの開始ポイントがありません。  

- 2 番目のサーバーは、 **[デバイス]** タブの **[サーバー]** グループ内に一覧表示されます。  

- 2 番目のサーバーではクライアント コンピューターのバックアップがサポートされていないため、バックアップの状態が **[サポートされていません]** と表示されます。 さらに、2 番目のサーバーを選択して右クリックすると、2 番目のサーバーに対してバックアップおよび復元関連のタスクは表示されません。  

- 2 つ目のサーバーを選択して **[サーバー プロパティの表示]** タスクをクリックしても、サーバーのプロパティ ページに **[バックアップ]** タブが表示されません。  

- Windows Server オペレーティング システムにはセキュリティ センターがないため、2 番目のサーバーのセキュリティ状態は **[該当なし]** と表示されます。  

- 2 番目のサーバーのグループ ポリシーの状態は、 **[該当なし]** と表示されます。  

###  <a name="BKMK_11"></a> コネクタ ソフトウェアをインストールします。  
 コンピューターをサーバーに接続ウィザードを使用してコンピューターをサーバーに接続したときに、コネクタ ソフトウェアがインストールされます。 」と入力して、このウィザードを起動することができます**http://<ServerName\>/connect** web ブラウザーのアドレス バーに (場所 *< ServerName\>* サーバーの名前を指定します)。  

> [!NOTE]
>  コンピューターがリモートの場所にある場合は、サーバーのウィザード、コンピューターに接続を実行する入力**http://<domainname\>/connect** web ブラウザーのアドレス バーに (場所 *< ドメイン\>* 組織のドメイン名です)。 ドメイン名情報はネットワーク管理者から取得できます。  

 コネクタ ソフトウェアは以下の処理を実行します。  

-   コンピューターを Windows Server Essentials に接続する  

-   毎晩、コンピューターが自動的にバックアップする (クライアント バックアップを作成するようにサーバーを構成している場合)  

-   管理者による、コンピューターの正常性の監視を支援する  

-   自宅のコンピューターから Windows Server Essentials の構成とリモート管理を可能にする  


 お使いのコンピューターを Windows Server Essentials サーバーに接続する方法の手順については、次を参照してください。[コンピューターをサーバーに接続する](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。   


###  <a name="BKMK_12"></a> コンピューターのデータと設定を移動手動で  
  Windows Server Essentials と Windows Server Essentials、Windows 7 オペレーティング システムを実行しているクライアント コンピューターに対してのみユーザー プロファイルの移行をサポートします。 Windows 7 ベースのコンピューターをサーバーに接続すると、コンピューターをサーバーに接続ウィザードにより、ユーザー プロファイルを自動的に移行できます。  

 ユーザー プロファイルは、Windows 8、Windows 8.1 または Windows 10 コンピューターをサーバーに接続するときに自動的に転送できません。 ただし Windows 8 コンピューターでは、Windows Easy Transfer を使用して、元のローカル ユーザーからドメインに参加しているコンピューターに、データと設定を転送することができます。 そのためには、Windows 8 の移行元コンピューターと、Windows 8 の移行先コンピューターの両方で、自分が管理者である必要があります。 Windows Easy Transfer を使用してファイルと設定を転送する方法の詳細については、Microsoft サポート技術情報の [記事 2735227](https://support.microsoft.com/kb/2735227) を参照してください。  

###  <a name="BKMK_Transfer"></a> コンピューターの展開中に複数のユーザー プロファイルを転送します。  
 Windows 7 または Windows 7 SP1 オペレーティング システムを実行しているコンピューターを Windows Server Essentials に接続する前に、複数のローカル ユーザー プロファイルを転送するためには、まずサーバー上で対応するネットワーク ユーザー アカウントを作成する必要があります。 ネットワーク ユーザー アカウントの作成に関する詳細については、「 [Add a user account](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)」を参照してください。  

 ユーザー プロファイルの移行は、(Windows Server Essentials) の Windows 7 または Windows 7 SP1 (Windows Server Essentials) を実行するコンピューターでのみサポートされます。 コンピューターをサーバーに接続ウィザードを使用して、コンピューターを Windows Server Essentials サーバーに接続するときに、古いユーザー ローカル アカウントのユーザー データと設定を、新しいネットワーク ユーザー アカウントに移動するオプションが提供されます。 そのためには、ウィザードの **[既存のユーザー データと設定を移動]** ページで、ネットワーク ユーザー アカウントを、コンピューター上に存在するローカル ユーザー アカウントにマッピングして、クライアント コンピューターに格納されている複数のユーザー プロファイルを転送します。  

###  <a name="BKMK_13"></a> コネクタ ソフトウェアをアンインストールします。  
 コントロール パネルを使用して、コンピューターからコネクタ ソフトウェアをアンインストールします。 これは通常、コネクタ ソフトウェアに問題がある場合、またはコネクタ ソフトウェアの新しいバージョンをインストールする必要がある場合に実行します。 この手順を完了するには、管理者としてコンピューターにログオンする必要があります。  

> [!IMPORTANT]
>  クライアント コンピューター上のオペレーティング システムをアップグレードする場合、コネクタ ソフトウェアは自動的にアンインストールされます。 アップグレードが完了したら、コネクタ ソフトウェアを再インストールする必要があります。 オペレーティング システムをアップグレードする前に、コネクタ ソフトウェアをアンインストールすることをお勧めします。 アップグレード完了後に、コネクタ ソフトウェアをアンインストールすることはまだ容認可能ですが、その結果、コネクタ ソフトウェアをアンインストールしてから再インストールするまで、サーバーとクライアント コンピューター間で状態の不整合が発生する可能性があります。  

##### <a name="to-uninstall-connector-software-from-a-computer"></a>コンピューターからコネクタ ソフトウェアをアンインストールするには  

1.  Windows 7、Windows 8、Windows 8.1 または Windows 10 を実行しているコンピューターから開く**コントロール パネルの** 、し、**プログラム**セクションで、**ビューには、更新プログラムがインストールされている**します。  

2.  インストールされているプログラムの一覧から **[Windows Server Essentials Connector]** を選択し、 **[アンインストール]** をクリックします。  

3.  警告ページで、 **[はい]** をクリックします。  

4.  **[ユーザー アカウント制御]** ウィンドウが表示されたら **[許可]** をクリックします。  

5.  Windows Server Essentials で、スタート パッドを閉じるように提案する、Windows Server Essentials Connector ページが表示されている場合 をクリックして**OK**します。  

6.  プログラムがアンインストールされるまで待ちます。 ソフトウェアが削除されると、インストールされているプログラムや更新プログラムの一覧に **[Windows Server Essentials Connector]** が表示されなくなります。 さらに、スタート パッドとダッシュボードへのショートカットが、コンピューターのデスクトップに表示されなくなります。  

> [!NOTE]
> - コネクタ ソフトウェアをアンインストールしても、ダッシュボードの **[デバイス]** タブに表示されているコンピューターの一覧からコンピューターは削除されません。 ダッシュボードからコンピューターを削除するには、「 [Remove a computer from the server](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)」を参照してください。  
>   -   コネクタ ソフトウェアをアンインストールする場合、サーバーにマッピングされていた、クライアント コンピューター上の共有フォルダーは削除されません。 サーバーにマップされている共有フォルダーは、手動で削除する必要があります。  
> 
> -   コネクタ ソフトウェアをアンインストールしても、コンピューターが元のドメインから参加解除されることはありません。 コンピューターをドメインから手動で参加解除する必要があります。 手順については、「[Windows ドメインからコンピューターを削除](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)」を参照してください。  


###  <a name="BKMK_14"></a> コンピューターから切断するか、コンピューターをサーバーに再接続  
 サーバーからコンピューターを切断するには、次の手順を行う必要があります。  


1. コントロール パネルを使用して、コンピューターからコネクタ ソフトウェアをアンインストールします。 詳細な手順については、「[コネクタ ソフトウェアのアンインストール](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)」を参照してください。   


2. Windows Server Essentials ドメインからコンピューターの参加を解除し、ワークグループに参加させます。 Windows をワークグループに参加させるための詳細な手順については、「 [ワークグループへの参加または作成](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)」を参照してください。  

3. ダッシュボードを使用して、サーバーからコンピューターを削除します。 詳細な手順については、「[コンピューターをサーバーから削除](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)」を参照してください。  

   以前、Windows Server Essentials サーバー ネットワークから切断したサーバーにコンピューターを再接続するには、次の手順を行う必要があります。  


4. コントロール パネルを使用して、コンピューターからコネクタ ソフトウェアをアンインストールします。 詳細な手順については、「[コネクタ ソフトウェアのアンインストール](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)」を参照してください。  

5. Windows Server Essentials ドメインからコンピューターの参加を解除し、ワークグループに参加させます。 Windows をワークグループに参加させるための詳細な手順については、「 [ワークグループへの参加または作成](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)」を参照してください。  

6. コンピューターをサーバーに接続ウィザードを使用して、コンピューターをサーバーに接続します。 手順については、次を参照してください。[コンピューターをサーバーに接続する](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  

###  <a name="BKMK_Sleep"></a> バックアップのスリープ状態と動作方法と、休止モード  
 コンピューターをサーバーに接続した際に **[バックアップのためにこのコンピューターのスリープを解除する]** オプションを選択すると、バックアップ スケジュールの指定に従って、毎日スリープ モードまたは休止モードから自動的にウェイクアップして、バックアップを実行します。 バックアップが完了したら、コンピューターは電源管理設定に基づいて、スリープまたは休止モードに戻ります。 このオプションを選択しないと、コンピューターがスリープまたは休止状態の場合、サーバーはコンピューターをバックアップしません。 詳細については、「[ユーザー ステーションの管理](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)」を参照してください。  

##  <a name="BKMK_C"></a> スタート パッドを使用します。  
 スタート パッドを使用すると、Windows Server Essentials サーバーから共有リソースへのアクセス、コンピューターのバックアップの実行、およびシステム正常性アラートへの応答を実行することができます。  

-   [スタート パッドの概要](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)  

-   [Mac コンピューターで、スタート パッドを使用してください。](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  

## <a name="see-also"></a>関連項目  

-   [サーバーに接続しているコンピューターをトラブルシューティングします。](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md)  

-   [ユーザー アカウントの管理](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)  


-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [リモートで作業します。](Work-Remotely-in-Windows-Server-Essentials.md)  

-   [デジタル メディアを再生します。](Play-Digital-Media-in-Windows-Server-Essentials.md)

-   [共有フォルダーの使用](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [リモートで作業します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)  

-   [デジタル メディアを再生します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)

