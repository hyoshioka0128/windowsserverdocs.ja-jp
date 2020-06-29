---
title: Windows Server Essentials でのオンライン バックアップの管理
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5c9f6dc91d5bc46d3be6e20e105530a9dca2b548
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470653"
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Windows Server Essentials でのオンライン バックアップの管理

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 Microsoft Azure Backup と統合すると、Windows Server Essentials ダッシュボードに [**オンラインバックアップ**] 管理ページが表示されます。 **[オンライン バックアップ]** ページでは、一般的な管理タスクを実行できます。 [オンライン バックアップ] ページには次の機能が含まれています。

- 次のサブセクション ページがあります。

  -   **[オンライン バックアップ]** オンライン バックアップ用のサーバーを登録すると、このセクションに、現在のバックアップの状態、記憶域の状態、およびアカウント情報が表示されます。

  -   **保護されたフォルダー**このセクションには、サーバー上のすべての共有フォルダーとすべてのファイル履歴フォルダー、および Azure でバックアップするように選択したその他のすべてのフォルダーが一覧表示されます。 この一覧には、フォルダー名、フォルダーのパス、および各共有フォルダーの状態が含まれています。

  -   **[バックアップ履歴]** このセクションには、最近のオンライン バックアップの一覧が表示されます。 この一覧には、操作の種類、および各バックアップの時間と状態が含まれています。

- 選択したバックアップ ジョブまたは復元ジョブに関する追加情報が表示される詳細ウィンドウ。

- 実行できる一連の管理タスクが表示される作業ウィンドウ。

  ベスト プラクティスとして、最も重要なビジネスおよびユーザーのデータをバックアップする必要があります。 たとえば、重要なデータ ファイルを含むサーバー フォルダーをバックアップする必要があります。 また、重要な情報を含むネットワーク コンピューターのファイル履歴もバックアップする必要があります。

  オンラインでバックアップするデータを決定する際は、実装するバックアップの頻度と保持ポリシーを検討します。 その後、予算を確認し、確保できる記憶域の容量を決定します。 ニーズに対する記憶域のコストとボリュームのバランスを取り、重要なデータをできるだけ多く保護するようにオンライン バックアップを構成します。 料金情報については、「 [Azure Backup の料金詳細](https://azure.microsoft.com/pricing/details/backup/)」を参照してください。

  次のセクションでは、Windows Server Essentials ダッシュボードに表示できるさまざまなオンライン バックアップ タスクについて説明します。

## <a name="online-backup-tasks-in-the-dashboard"></a>ダッシュボードでのオンライン バックアップ タスク

-   [Azure Backup 資格情報コンテナーに証明書をアップロードする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)

-   [オンライン バックアップを構成する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)

-   [オンライン バックアップを開始する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)

-   [オンライン バックアップからファイルとフォルダーを復元する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)

-   [このサーバーをバックアップ用に登録する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)

-   [サーバーの登録解除](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)

###  <a name="upload-a-certificate-to-the-azure-backup-vault"></a><a name="BKMK_1"></a>証明書を Azure Backup コンテナーにアップロードする
 Windows Server Essentials のオンラインバックアップに Azure Backup を使用するには、その前に、バックアップ資格情報コンテナーに登録するための公開証明書をアップロードする必要があります。 証明書は、サブスクリプションに関連付けられているリソースを管理するために、Microsoft Online Services サブスクリプションの所有者の代理として機能する、Azure Backup の展開 (エージェント) を認証するために使用されます。

> [!NOTE]
>  証明書をアップロードする前に、「[Azure Backup サービスへのサインアップ](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)」の手順を完了する必要があります、

##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>Azure Backup サービスで使用する証明書をアップロードするには

1. 管理者アカウントで Windows Server Essentials ダッシュボードにログオンします。

2. ダッシュボードの **[ホーム]** ページで、**[オンライン バックアップ]** をクリックします。

3. **[オンライン バックアップ]** 領域で、**[Azure Backup コンテナーに証明書をアップロード]** をクリックします。

    これにより、Azure 管理ポータルで**Recovery Services**が開きます。 Azure にまだサインインしていない場合は、Microsoft アカウントを使用してサインインする必要があります。

4. オンライン バックアップに使用するバックアップ コンテナーの名前をクリックして、バックアップ コンテナーの **[クイック スタート]** ページを開きます。

5. **[証明書の管理]** をクリックします。

6. **[証明書の管理]** ダイアログ ボックスで、Windows Server Essentials によって生成されたパブリック証明書のパスを貼り付けます。 パブリック証明書のパスを入手するには、次の手順を実行します。

   1.  Windows Server Essentials ダッシュボードで、**[オンライン バックアップ]** タブをクリックします。

   2.  **[オンライン バックアップ]** ページで、生成された証明書のパスをコピーします。

   3.  Azure 管理ポータルに切り替えて、[**証明書の管理**] ダイアログボックスで、生成された公開証明書をアップロードするためのパスを貼り付けます。

   > [!NOTE]
   >  独自のパブリック証明書を使用することもできます。 必要な証明書を知るには、**[クイック スタート]** ページで、**[証明書を取得]** リンクをクリックします。

   > [!NOTE]
   >   Azure には、公開キーを持つ x.509 v2 証明書が必要です。 詳細については、「 [資格情報コンテナー証明書を管理する](https://msdn.microsoft.com/library/azure/dn169036.aspx)」を参照してください。

7. 証明書を選択した後に、**[OK]** (チェック マーク) をクリックします。

8. **[クイック スタート]** ページに戻ります。 **[ダッシュボード]** をクリックし、証明書が正常にアップロードされたことを確認します。 証明書が正常にアップロードされると、ダッシュボードに証明書の拇印と有効期限が表示されます。

   この手順を完了した後は、次の手順を実行します。

9. Azure Backup サービスにサーバーを登録します。 詳細については、「[このサーバーをバックアップ用に登録する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)」を参照してください。

10. サーバーのオンライン バックアップを構成します。 詳細については、「[オンライン バックアップを構成する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。

###  <a name="configure-online-backup"></a><a name="BKMK_2"></a>オンラインバックアップの構成
 サーバーを Azure Backup に登録した後、Windows Server Essentials のオンラインバックアップ設定を構成できます。

##### <a name="to-configure-online-backup"></a>オンライン バックアップを構成するには

1.  Windows Server Essentials ダッシュボードのサーバーの登録ウィザードまたは **[オンライン バックアップ]** ページから、**[オンライン バックアップの構成]** をクリックします。 オンライン バックアップの構成ウィザードが表示されます。

2.  ウィザードの [**オンラインバックアップの構成**] ページで、Azure Backup にバックアップする各サーバーフォルダーのチェックボックスをオンにします。 バックアップに含めない各サーバー フォルダーのチェック ボックスをオフにします。 一覧に表示されていないフォルダーを追加するには、**[フォルダーの追加]** をクリックします。 選択が完了したら、**[次へ]** をクリックします。

    > [!NOTE]
    >  ローカル サーバー上にないフォルダーと、ReFS としてフォーマットされたドライブ上にあるフォルダーを選択することはできません。

3.  ウィザードの **[ファイル履歴バックアップの追加]** ページで、ファイル履歴機能をサポートするネットワーク コンピューター用にファイル履歴バックアップを含めることができます。 **[次へ]** をクリックして続行します。

4.  ウィザードの **[バックアップ スケジュールの指定]** ページで、次の項目を構成し、**[次へ]** をクリックして続行します。

    -   オンライン バックアップを実行する時刻を選択するか受け入れます。 既定の時刻は午後 10 時 00 分です。 2 回目のバックアップを実行する時刻を指定することもできます。

    -   オンライン バックアップを実行する曜日を選択するか受け入れます。 既定では、オンライン バックアップは月曜日から金曜日まで実行されます。

5.  ウィザードの **[バックアップの保持ポリシーの指定]** ページで、オンライン バックアップを保持する日数を選択し、**[次へ]** をクリックします。 既定では 7 日です。 オンライン バックアップを 15 日間または 30 日間保持するように選択することもできます。

    > [!NOTE]
    >   Azure Backup は常に最新のバックアップを保持します。 バックアップ先にバックアップを格納するための十分な空き容量がない場合、バックアップ処理に失敗します。 このような状況を避けるには、追加の記憶域を購入するか、またはデータの保持期間を短くしてください。 価格情報については、Microsoft Azure Backup の[料金詳細](https://azure.microsoft.com/pricing/details/backup/)を参照してください。

6.  ウィザードの **[帯域幅の使用率の選択]** ページで、オンライン バックアップに割り当てられているインターネット帯域幅の量を制限する場合、**[インターネット帯域幅の使用を有効にする]** を選択します。 このページのオプションを使用して、営業時間と非営業時間にオンライン バックアップで利用できるインターネット帯域幅の量を指定します。 その後、営業時間と営業日を定義します。

    > [!NOTE]
    >   Azure Backup では、統合ソフトウェアが情報をバックアップまたは復元するときにネットワーク帯域幅をどのように利用するかをカスタマイズできます。 制限としてよく知られている手法を使用すると、特定の日時間隔の間にバックアップおよび復元プロセスで使用できるネットワーク帯域幅の量を制御できます。 オンライン バックアップの構成ウィザードで **[インターネット帯域幅の使用を有効にする]** チェック ボックスをオンにすると、営業日と営業時間を指定して、帯域幅を制限する営業時間を適用できます。 非営業時間の制限は、他のすべての時間にも使用されます。 有効な帯域幅の範囲は、両方の制限で 256 Kbps から [無制限] です。

7.  オンライン バックアップの構成が完了したら、**[閉じる]** をクリックします。

    > [!TIP]
    >  バックアップの構成が正常に完了すると、**[オンライン バックアップ]** ページに、最新のオンライン バックアップの状態と、バックアップ コンテナーで使用される記憶域の容量が表示されます。 以前のバックアップの状態を表示するには、**[バックアップ履歴]** をクリックします。

###  <a name="start-an-online-backup"></a><a name="BKMK_3"></a>オンラインバックアップを開始する

> [!NOTE]
>  オンライン バックアップを開始する前に、[このサーバーをバックアップ用に登録](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)して、[オンライン バックアップを構成](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)する必要があります。

##### <a name="to-start-an-online-backup-immediately"></a>オンライン バックアップを今すぐ開始するには

1.  管理者としてダッシュボードにログオンします。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  **[オンライン バックアップ タスク]** ウィンドウで、**[今すぐバックアップを開始]** をクリックします。

###  <a name="restore-files-and-folders-from-an-online-backup"></a><a name="BKMK_4"></a>オンラインバックアップからファイルとフォルダーを復元する
 ファイルとフォルダーの復元ウィザードを使用して、オンラインでバックアップされたファイルとフォルダーを検索、選択、および復元する処理を実行できます。 ウィザードの各手順では、次のタスクを実行します。

1.  **ファイルとフォルダーの復元元のオンライン バックアップを選択します。**

     ファイルとフォルダーの復元ウィザードを実行する場合、現在ログオン中のサーバーのオンライン バックアップからファイルを復元するか、または別のサーバーのバックアップから復元するかを最初に指定する必要があります。

2.  **ファイルとフォルダーの復元元のサーバーを選択します。**

     ファイルとフォルダーを別のサーバーから復元することを選択した場合、使用可能なサーバーの一覧から復元元のサーバーを選択し、**[次へ]** をクリックします。

3.  **復元するファイルとフォルダーが含まれるボリュームを選択します。**

     オンライン バックアップに含まれるボリュームは、バックアップ元のサーバー上のボリュームに対応しています。 ボリュームを選択して、復元するバックアップの日付と時刻を選択し、**[次へ]** をクリックします。

4.  **復元するファイルとフォルダーを選択します。**

     ウィザードの **[復元する項目の選択]** ページで、さまざまなフォルダーの場所を開いて、復元する各ファイルまたはフォルダーのチェック ボックスをオンにすることができます。 ファイルの選択が完了したら、**[次へ]** をクリックします。

5.  **ファイルとフォルダーの復元先を指定します。**

     ウィザードの **[復元オプションの指定]** ページで、ファイルとフォルダーの復元先を指定できます。 2 つのオプションがあります。

    -   **[元の場所に復元]**: このオプションを選択すると、ファイルとフォルダーがバックアップ元の場所に復元されます。

    -   **[別の場所に復元]**:  このオプションを選択すると、ファイルの復元先にサーバー上の別の場所を指定できます。

         既定のインストールでは、復元するファイルと同じ名前のファイルが復元先に存在する場合、元のファイルのコピーが作成されます。 さらに、現在のファイルのアクセス許可を反映するようにアクセス制御リスト (ACL) が更新されます。 **[詳細設定]** をクリックして、既定の設定をカスタマイズできます。

6.  **復元情報を確認します。**

     **[復元情報の確認]** ページに、指定した復元手順の要約が表示されます。 ファイルの復元を続行するには、オンライン バックアップ アカウントの正しいパスフレーズを入力する必要があります。

###  <a name="register-this-server-for-backup"></a><a name="BKMK_5"></a>このサーバーをバックアップ用に登録する
 Windows Server Essentials サーバー上のファイル、フォルダー、およびファイル履歴をバックアップまたは復元して Azure Backup するには、最初にサーバーを Microsoft Azure Backup サービスに登録する必要があります。

> [!NOTE]
>  サーバーを登録する前に、オンライン バックアップを保存するバックアップ コンテナーで使用する証明書をアップロードする必要があります。 詳細については、「[Azure Backup コンテナーに証明書をアップロードする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)」を参照してください。

##### <a name="to-register-your-server-with-azure-backup"></a>Azure Backup にサーバーを登録するには

1.  サーバーに管理者としてログオンし、ダッシュボードを開きます。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  **[オンライン バックアップ]** サブセクションで、**[登録]** をクリックします。

4.  オンライン バックアップのバックアップ コンテナーで使用する証明書を選択します。 既定では、既定の証明書が選択されています。別の証明書を選択する場合は、**[参照]** を使用します。 続けて、 **[次へ]** をクリックします。

5.  ウィザードの指示に従ってパスフレーズを作成し、登録を完了します。

###  <a name="unregister-server"></a><a name="BKMK_6"></a>サーバーの登録解除

> [!CAUTION]
>  Microsoft Azure Backup サービスから Windows Server Essentials サーバーの登録を解除すると、Azure Backup はサーバーをバックアップできなくなります。 さらに、以前にアップロードされたサーバー データは消去されます。 オンライン バックアップを再開するには、サーバーを再登録する必要があります。

##### <a name="to-unregister-your-server-with-azure-backup"></a>Azure Backup からサーバーの登録を解除するには

1.  [Azure の管理ポータル](https://manage.windowsazure.com)にサインインします。

2.  **[復旧サービス]** をクリックします。

3.  **[復旧サービス]** で、バックアップ コンテナーの名前をクリックします。

4.  コンテナーの **[クイック スタート]** ページで、**[サーバー]** をクリックします。

5.  サーバーを選択して、**[削除]** をクリックし、確認プロンプトで **[はい]** をクリックします。

## <a name="related-tasks"></a>関連タスク

-   [オンライン バックアップ ポリシーを変更する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)

-   [オンライン バックアップ記憶域の使用状況を表示する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)

-   [オンライン バックアップに新しいフォルダーを含める](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)

-   [オンライン バックアップ ポリシーからファイル履歴バックアップを削除または除外する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)

-   [オンライン サーバー バックアップを無効または再度有効にする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)

-   [進行中のオンライン サーバー バックアップを停止する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)

-   [オンライン バックアップの状態を表示する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)

-   [オンライン バックアップのアラートを表示および管理する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)

-   [オンライン バックアップを既定の設定にリセットする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)

-   [Azure Backup サービスにサインアップする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)

-   [Azure Backup と Windows Server Essentials を統合する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)

-   [Windows Server Essentials のオンライン バックアップ用のフォルダーを保護する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)

-   [Windows Server Essentials のオンラインバックアップ履歴](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)

###  <a name="change-the-online-backup-policy"></a><a name="BKMK_7"></a>オンラインバックアップポリシーを変更する
 Windows Server Essentials ダッシュボードを使用して、オンライン バックアップ ポリシーを簡単に変更できます。

##### <a name="to-change-the-online-backup-policy"></a>オンライン バックアップ ポリシーを変更するには

1. 管理者としてダッシュボードにログオンします。

2. ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3. **[オンライン バックアップ タスク]** ウィンドウで、**[オンライン バックアップの構成]** をクリックします。

4. ウィザードの指示に従ってバックアップ ポリシーをカスタマイズします。

   カスタマイズできる設定の詳細については、「[オンライン バックアップの構成](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。

###  <a name="view-online-backup-storage-usage"></a><a name="BKMK_8"></a>オンラインバックアップ記憶域の使用状況の表示

##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>オンライン バックアップで使用されている記憶域の容量を表示するには

1.  管理者としてダッシュボードにログオンします。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  **[オンライン バックアップ]** タブの情報ウィンドウに、**[記憶域の状態]** が表示されます。

###  <a name="include-a-new-folder-in-online-backup"></a><a name="BKMK_9"></a>オンラインバックアップに新しいフォルダーを含める

##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>オンライン バックアップ ポリシーに新しいフォルダーを含めるには

1. 管理者としてダッシュボードにログオンします。

2. ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3. **[オンライン バックアップ タスク]** ウィンドウで、**[オンライン バックアップの構成]** をクリックします。

4. **[バックアップ ポリシーの変更または削除]** ページで、**[オンライン バックアップ ポリシーのカスタマイズ]** をクリックします。

5. **[オンライン バックアップの構成]** ページで、含めるフォルダーが一覧に表示されていない場合は、**[フォルダーの追加]** をクリックします。

6. **[フォルダーの追加]** ウィンドウで、オンライン バックアップに含めるフォルダーを参照して選択し、**[OK]** をクリックします。

7. **[オンライン バックアップの構成]** ページで、必要に応じてその他の含めるフォルダーを選択し、**[次へ]** をクリックします。

8. ウィザードの指示に従って、オンライン バックアップ ポリシーのカスタマイズを完了します。

   カスタマイズできる設定の詳細については、「[オンライン バックアップの構成](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。

###  <a name="remove-or-exclude-file-history-backups-from-the-online-backup-policy"></a><a name="BKMK_10"></a>オンラインバックアップポリシーからファイル履歴バックアップを削除または除外する

##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>オンライン バックアップ ポリシーからフォルダーを削除または除外するには

1.  管理者としてダッシュボードにログオンします。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  [**保護さ**れたフォルダー] タブをクリックします。詳細ウィンドウに、フォルダーの一覧とオンラインバックアップの状態が表示されます。

4.  オンライン バックアップ ポリシーから除外するフォルダーを選択し、作業ウィンドウで、**[オンライン バックアップからフォルダーを削除]** をクリックします。

###  <a name="disable-or-re-enable-online-server-backup"></a><a name="BKMK_11"></a>オンラインサーバーバックアップを無効または再度有効にする
 Azure Backup を使用してサーバーデータをバックアップまたは復元する方法については、「[このサーバーをバックアップ用に登録](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)する」を参照してください。

 Azure Backup を使用してサーバーデータのバックアップまたは復元を停止する手順については、「[サーバーの登録解除](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)」を参照してください。

###  <a name="stop-an-online-server-backup-in-progress"></a><a name="BKMK_12"></a>進行中のオンラインサーバーバックアップを停止する

##### <a name="to-stop-an-online-server-backup-in-progress"></a>進行中のオンライン サーバー バックアップを停止するには

1.  管理者としてダッシュボードにログオンします。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  **[オンライン バックアップ タスク]** ウィンドウで、**[バックアップの停止]** をクリックします。

     バックアップを停止すると、**[バックアップ履歴]** の一覧で、そのバックアップの状態が **[中止]** に変わります。

###  <a name="view-online-backup-status"></a><a name="BKMK_13"></a>オンラインバックアップの状態の表示

##### <a name="to-view-the-backup-status"></a>バックアップの状態を表示するには

1.  管理者としてダッシュボードにログオンします。

2.  ナビゲーション バーで、**[オンライン バックアップ]** をクリックします。

3.  [**バックアップ履歴**] タブをクリックします。リストビューには、各バックアップジョブの状態が表示されます。 バックアップ ジョブを選択すると、そのジョブに関する詳細情報が表示されます。

###  <a name="view-and-manage-online-backup-alerts"></a><a name="BKMK_14"></a>オンラインバックアップのアラートを表示および管理する
 他の多くのアラートと同様に、Azure Backup のアラートはアラートビューアーに表示されます。

##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>オンライン バックアップ アラートをアラート ビューアーに表示するには

1. ダッシュボードを開きます。

2. 次のいずれかの操作を行います。

     Windows Server Essentials: ナビゲーションウィンドウで、[アラート] アイコンが [ \( 重大]、[警告]、[情報] のいずれかになっている可能性があり \) ます。 アラート ビューアーが開きます。

     Windows Server Essentials:**ホーム**ページで、[**正常性の監視**] タブをクリックします。

3. Azure Backup に関連する問題のアラートの一覧を確認します。

   アラートビューアーまたは [正常性の監視] タブを使用してアラートを管理する方法の詳細については、「[システム正常性の管理](Manage-System-Health-in-Windows-Server-Essentials.md)」を参照してください。

###  <a name="reset-online-backup-to-default-settings"></a><a name="BKMK_15"></a>オンラインバックアップを既定の設定にリセットする
 Windows Server Essentials には、オンライン バックアップの設定を構成するのに役立つウィザードが用意されています。 既定の設定を復元する場合は、**[オンライン バックアップの構成]** タスクを実行し、**[オンライン バックアップ ポリシーの削除]** オプションを選択します。 その後、**[オンライン バックアップの構成]** タスクを再実行します。 以前にアップロードされたデータは変更されません。

###  <a name="sign-up-for-azure-backup-service"></a><a name="BKMK_16"></a>Azure Backup サービスにサインアップする
 Microsoft Azure Backup と Windows Server Essentials の統合を準備するには、Microsoft Online Services アカウントを使用して Azure 管理ポータルにログオンし、Azure にオンラインバックアップを格納するためのバックアップコンテナーを作成します。 次に、Azure Backup 統合モジュールをダウンロードし、ダウンロードしたファイルを使用して、Azure Backup アドインを Windows Server Essentials サーバーにインストールします。 Microsoft アカウントを持っていない場合は、無料評価版にサインアップできます。

 このセットアップを実行するには、次のタスクを実行します。

1.  Microsoft Online Services アカウントおよび Backup プレビュー版にサインアップします。

2.  オンライン バックアップを保存するバックアップ コンテナーを作成します。

3.  Azure Backup エージェントをダウンロードします。

4.  Azure Backup アドインをサーバーにインストールします。

####  <a name="sign-up-for-a-microsoft-online-services-account-and-the-backup-preview"></a><a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a>Microsoft Online Services アカウントとバックアッププレビューにサインアップする

1.  Windows Server Essentials ダッシュボードにログオンします。

2.  ダッシュボードの **[ホーム]** ページで、**[アドイン]** カテゴリ、**[Azure Backup との統合]**、**[クリックして Azure Backup にサインアップする]** の順にクリックします。

3.  [Azure **Recovery Services** ] ページの [**バックアップ (プレビュー)** ] セクションで、詳細を確認します。

4.  Azure サブスクリプションをお持ちでない場合は、[**無料試用版**] をクリックし、指示に従って azure サブスクリプションを取得します。

     Azure サブスクリプションを既にお持ちの場合は、web ページの右上隅にある [**ポータル**] をクリックして、azure 管理ポータルにアクセスします。

5.  [Azure 管理ポータル] ページで、左側のウィンドウに**Recovery Services**が表示されます。 ここで、Windows Server Essentials からのオンラインバックアップを保存するバックアップコンテナーを管理します。

####  <a name="create-a-backup-vault-to-store-online-backups"></a><a name="BKMK_Createabackupvaulttostoreonlinebackups"></a>オンラインバックアップを格納するためのバックアップコンテナーを作成する

1.  Windows Server Essentials サーバー上の Web ブラウザーから、 [Azure 管理ポータル](https://manage.windowsazure.com)にサインインします。

2.  Azure 管理ポータルで、[**新規**]、[ **Data Services**]、[ **Recovery Services**]、[**バックアップコンテナー**]、[**簡易作成**] の順にクリックします。

3.  バックアップ コンテナーの名前を入力し、バックアップを保存するリージョンを選択して、**[簡易作成]** をクリックします。

     **[復旧サービス]** 領域が開き、新しいバックアップ コンテナーが表示されます。

####  <a name="download-the-azure-backup-agent"></a><a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a>Azure Backup エージェントのダウンロード

1.  Windows Server Essentials ダッシュボードを開きます。

2.  ダッシュボードの **[ホーム]** ページで、**[開始する]** タブをクリックし、**[アドイン]** カテゴリ、**[Azure Backup との統合]**、**[クリックして Azure Backup 統合モジュールをダウンロードする]** の順にクリックします。

####  <a name="install-the-azure-backup-add-in-on-the-server"></a><a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a>Azure Backup アドインをサーバーにインストールする

1. 管理者アカウントを使用してサーバーにサインインし、前の手順でダウンロードした **OnlineBackupAddin.wssx** ファイルを実行します。

2. **[ソフトウェア ライセンス条項]** が表示されます。 使用条件に同意する場合は、**[同意する]** をクリックしてインストールを続行します。

3. **[アドインのインストール]** ページで、**[アドインのインストール]** をクリックします。

   > [!NOTE]
   >  前提条件ソフトウェアをインストールするために、サーバーの再起動が必要な場合があります。

    **[インストール]** ページが表示されます。 インストールが開始すると、進行状況のインジケーターにインストールの進行状況が表示されます。 インストールが完了すると、Azure Backup アドインが正常にインストールされたことを示すメッセージが表示されます。

4. **[完了]** をクリックします。

5. ダッシュボードを閉じてから再度開きます。

    **[オンライン バックアップ]** という新しいタブがダッシュボードに追加されています。 このタブでは、サーバーを登録し、バックアップ設定を構成し、Azure 管理ポータルで**Recovery Services**を開いて、サーバーのバックアップコンテナーを管理できます。

   これらの手順を完了した後に、次の手順を実行します。

6. Windows Server Essentials で、オンラインバックアップに使用する証明書をアップロードします。 詳細については、「[Azure Backup コンテナーに証明書をアップロードする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)」を参照してください。

7. サーバーを Azure Backup コンテナーに登録します。 詳細については、「[このサーバーをバックアップ用に登録する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)」を参照してください。

8. サーバーのオンライン バックアップを構成します。 詳細については、「[オンライン バックアップを構成する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。

###  <a name="integrate-azure-backup-with-windows-server-essentials"></a><a name="BKMK_17"></a>Azure Backup と Windows Server Essentials の統合
 Microsoft Azure Backup 統合モジュールは、Windows Server Essentials の新機能です。これを使用すると、Microsoft が提供する Azure でホストされるストレージシステムに、サーバーからファイルやフォルダーを暗号化してバックアップすることができます。 Azure Backup を使用してサーバー上のデータを暗号化およびバックアップすることにより、重大なビジネスデータが、火災、洪水、盗難、またはその他の災害によって致命的に失われるのを防ぐことができます。 Azure Backup を使用してサーバーデータをバックアップすると、インターネット上のセキュリティで保護されたデータセンターにアップロードされる前に、パスフレーズを使用して情報が暗号化されます。 オンライン バックアップのデータにアクセスするには、証明書によって認証されているサーバーが必要で、パスフレーズを入力する必要があります。

 サーバーを Azure Backup に統合して登録した後、定期的にスケジュールされたバックアップを実行するようにオンラインバックアップ設定を構成できます。 また、オンライン バックアップ ダッシュボードで **[今すぐバックアップを開始]** タスクをクリックして、オンライン バックアップをいつでも開始できます。

 オンライン バックアップのセットアップには、次の手順が必要です。

1.  [Azure Backup サービスにサインアップ](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)する-backup サービスにサインアップした後に、バックアップコンテナーを作成し、Azure Backup 統合モジュールをダウンロードしてインストールします。

2.  [Azure Backup 資格情報コンテナーに証明書をアップロードする](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)

3.  [このサーバーをバックアップ用に登録する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)

4.  [オンライン バックアップを構成する](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)

> [!NOTE]
>   Azure Backup は、パスフレーズを使用してオンラインバックアップのファイルとフォルダーを暗号化します。 暗号化パスフレーズを変更すると、サーバーの登録時に指定したパスフレーズが置き換えられます。 パスフレーズには、ASCII コード文字のみを使用できます。

###  <a name="protect-folders-for-online-backup-in-windows-server-essentials"></a><a name="BKMK_18"></a>Windows Server Essentials でオンラインバックアップ用のフォルダーを保護する
 ダッシュボードの [オンライン バックアップ] セクションの **[保護されているフォルダー]** サブセクションに、サーバー上のすべての共有フォルダーの一覧が表示されます。 次の表で、一覧に含まれる情報を説明します。

|列|説明|
|------------|-----------------|
|**フォルダー名:**|オンライン バックアップに含まれているフォルダーの名前。<br /><br /> フォルダーを追加または除外するには、**[オンライン バックアップの構成]** タスクを実行します。|
|**フォルダーのパス:**|フォルダーの場所。|
|**状態:**|**保護**されて**いない状態、保護されていない**状態、**不明な**状態の3種類があります。|

###  <a name="online-backup-history-in-windows-server-essentials"></a><a name="BKMK_19"></a>Windows Server Essentials のオンラインバックアップ履歴
 ダッシュボードの [オンライン バックアップ] セクションの **[バックアップ履歴]** サブセクションに、最近のオンライン バックアップの一覧が表示されます。 正常に完了したバックアップを使用して、ファイルとフォルダーを復元することができます。 次の表で、一覧に含まれる情報を説明します。

|列|説明|
|------------|-----------------|
|**運用**|**[バックアップ]** と **[復元]** という 2 種類の操作があります。|
|**ごと**|最新の状態がログに記録された時刻です。|
|**状態:**|[**成功**]、[**進行**中]、[**キャンセル**]、[**警告**]、および [**失敗**] の5種類の状態があります。|

## <a name="additional-references"></a>その他のリファレンス

-   [バックアップと復元の管理](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)

-   [Microsoft Online Services の管理](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)

-   [Windows Server Essentials の使用](../use/Use-Windows-Server-Essentials.md)
