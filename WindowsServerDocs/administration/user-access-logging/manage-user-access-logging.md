---
title: ユーザー アクセス ログの管理
description: ユーザーアクセスログを管理する方法について説明します。
ms.topic: article
ms.assetid: 4f039017-4152-47eb-838e-bb6ef730b638
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 75f0395afbcbefcdc4ac3a9fc4dc4de3bf962428
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991749"
---
# <a name="manage-user-access-logging"></a>ユーザー アクセス ログの管理

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このドキュメントでは、ユーザー アクセス ログ (UAL) を管理する方法について説明します。

UAL は、サーバーの管理者がローカル サーバー上で役割とサービスの一意のクライアント要求の数を定量化できるようにするための機能です。

UAL は既定でインストールされ、有効化されます。また、ほぼリアルタイム ベースでデータを収集します。 UAL にはいくつかの構成オプションがあります。 ここでは、これらのオプションとその使用目的について説明します。

UAL の利点の詳細については、「[ユーザーアクセスログの概要](get-started-with-user-access-logging.md)」を参照してください。

**このドキュメントの内容**

このドキュメントで扱う構成オプションは次のとおりです。

-   UAL サービスの無効化と有効化

-   データの収集と削除

-   UAL で記録されたデータの削除

-   大量のイベントが存在する環境での UAL の管理

-   破損した状態からの回復

-   ワーク フォルダーの使用ライセンス追跡の有効化

## <a name="disabling-and-enabling-the-ual-service"></a><a name="BKMK_Step1"></a>UAL サービスの無効化と有効化
UAL が有効になり、Windows Server 2012 以降を実行しているコンピューターが初めてインストールされて起動されたときに、既定で実行されます。 管理者は、プライバシー要件またはその他の業務上のニーズに合わせて UAL をオフにしたり、無効にすることができます。 UAL は、サービスコンソール、コマンドライン、または PowerShell コマンドレットを使用して無効にすることができます。 ただし、次回コンピューターを起動するときに UAL が実行されないようにするには、サービスを無効にする必要もあります。 次の手順では、UAL をオフにして無効にする方法について説明します。

> [!NOTE]
> `Get-Service UALSVC` PowerShell コマンドレットを使用して、UAL サービスが実行しているかまたは停止しているか、有効か無効かなど、UAL に関する情報を取得できます。

#### <a name="to-stop-and-disable-the-ual-service-by-using-the-services-console"></a>サービス コンソールを使用して UAL サービスを停止および無効にするには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  サーバー マネージャーで、**[ツール]** をポイントし、**[サービス]** をクリックします。

3.  下にスクロールして、**[User Access Logging Service]** を選択します。**[サービスの停止]** をクリックします。

4.  \-サービス名を右クリックし、[**プロパティ**] を選択します。 **[全般]** タブで、**[スタートアップの種類]** を **[無効]** に変更し、**[OK]** をクリックします。

#### <a name="to-stop-and-disable-ual-from-the-command-line"></a>コマンド ラインを使用して UAL を停止および無効にするには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  Windows ロゴ キーを押しながら R キーを押し、「**cmd**」と入力してコマンド プロンプト ウィンドウを開きます。

    > [!IMPORTANT]
    > [**ユーザー アカウント制御**] ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、[**はい**] をクリックします。

3.  「**net stop ualsvc**」と入力し、Enter キーを押します。

4.  「**netsh ualsvc set opmode mode=disable**」と入力し、Enter キーを押します。

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

また、Stop-service および Disable-Ual の Windows PowerShell コマンドを使用して、UAL を停止および無効にすることもできます。

```
Stop-service ualsvc
```

```
Disable-ual
```

後で UAL を再起動して再度有効にする場合は、次の手順で実行できます。

#### <a name="to-start-and-enable-the-ual-service-by-using-the-services-console"></a>サービス コンソールを使用して UAL サービスを開始および有効にするには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  サーバー マネージャーで、**[ツール]** をポイントし、**[サービス]** をクリックします。

3.  下にスクロールして、**[User Access Logging Service]** を選択します。**[サービスの開始]** をクリックします。

4.  サービス名を右クリックし、**[プロパティ]** をクリックします。 **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。

#### <a name="to-start-and-enable-ual-from-the-command-line"></a>コマンド ラインを使用して UAL を開始および有効にするには

1.  ローカル管理者の資格情報でサーバーにサインインします。

2.  Windows ロゴ キーを押しながら R キーを押し、「**cmd**」と入力してコマンド プロンプト ウィンドウを開きます。

    > [!IMPORTANT]
    > [**ユーザー アカウント制御**] ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、[**はい**] をクリックします。

3.  「**net start ualsvc**」と入力し、Enter キーを押します。

4.  「**netsh ualsvc set opmode mode=enable**」と入力し、Enter キーを押します。

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

また、Start-service および Enable-Ual の Windows PowerShell コマンドを使用して、UAL を開始し、再度有効にすることもできます。

```
Enable-ual
```

```
Start-service ualsvc
```

## <a name="collecting-ual-data"></a><a name="BKMK_Step2"></a>UAL データの収集
前のセクションで説明した PowerShell コマンドレットに加えて、次の12つの追加のコマンドレットを使用して UAL データを収集できます。

-   **Get-UalOverview**: インストールされている製品と役割の UAL 関連の詳細と履歴を示します。

-   **Get-UalServerUser**: ローカル サーバーまたはターゲットのサーバーのクライアント ユーザー アクセス データを示します。

-   **Get-UalServerDevice**: ローカル サーバーまたはターゲットのサーバーのクライアント デバイス アクセス データを示します。

-   **Get-UalUserAccess**: クライアント ユーザー アクセス データをローカル サーバーまたはターゲットのサーバーにインストールされている役割または製品ごとに示します。

-   **Get-UalDeviceAccess**: クライアント デバイス アクセス データをローカル サーバーまたはターゲットのサーバーにインストールされている役割または製品ごとに示します。

-   **Get-UalDailyUserAccess**: クライアント ユーザー アクセス データをその年の日付ごとに示します。

-   **Get-UalDailyDeviceAccess**:クライアント デバイス アクセス データをその年の日付ごとに示します。

-   **Get-UalDailyAccess**: クライアント デバイス データとユーザー アクセス データの両方をその年の日付ごとに示します。

-   **Get-UalHyperV**: ローカル サーバーまたはターゲットのサーバーに関連する仮想マシン データを示します。

-   **Get-UalDns**: ローカル DNS サーバーまたはターゲットの DNS サーバーの DNS クライアント固有データを示します。

-   **Get-UalSystemId**: ローカル サーバーまたはターゲットのサーバーを一意に識別するシステム固有のデータを示します。

`Get-UalSystemId` はサーバーの一意のプロファイルを示すために使用され、プロファイルにはそのサーバーからの他のすべてのデータが関連付けられます。サーバーでで変更が発生すると、新しいプロファイルのパラメーターのいずれか `Get-UalSystemId` が作成されます。  `Get-UalOverview` は、サーバーにインストールされている役割およびそのサーバーで使用されている役割の一覧を管理者に提供するために使用されます。

> [!NOTE]
> 印刷とドキュメントサービスとファイルサービスの基本的な機能は、既定でインストールされます。 したがって、管理者は、すべての役割がインストールされているのと同様に、これらに関する情報を常に確認することができます。これらのサーバーの役割について UAL では一意のデータが収集されるため、Hyper-V と DNS で異なる UAL コマンドレットが含まれます。

UAL コマンドレットの一般的なユース ケース シナリオでは、管理者がデータ範囲の一意のクライアント アクセスについて UAL に対してクエリを実行します。これは、さまざまな方法で実行できます。次に、データ範囲の一意のデバイス アクセスについてクエリを実行するための推奨される方法を示します。

```
PS C:\Windows\system32>Gwmi -Namespace "root\AccessLogging" -query "SELECT * FROM MsftUal_DeviceAccess WHERE LastSeen >='1/01/2013' and LastSeen <='3/31/2013'"

```

この方法を使用すると、そのデータ範囲内でサーバーに要求を行った、すべての一意のクライアント デバイスの詳細な一覧が IP アドレスで返されます。

一意の各クライアントの ' ActivityCount ' は、1日あたり65535に制限されています。また、日付別にクエリを実行する場合にのみ、PowerShell から WMI を呼び出す必要があります。次の例に示すように、他のすべての UAL コマンドレット パラメーターは PS クエリ内で期待どおりに使用できます。

```
PS C:\Windows\system32> Get-UalDeviceAccess -IPAddress "10.36.206.112"

ActivityCount    : 1
FirstSeen        : 6/23/2012 5:06:50 AM
IPAddress        : 10.36.206.112
LastSeen         : 6/23/2012 5:06:50 AM
ProductName      : Windows Server 2012 Datacenter
RoleGuid         : 10a9226f-50ee-49d8-a393-9a501d47ce04
RoleName         : File Server
TenantIdentifier : 00000000-0000-0000-0000-000000000000
PSComputerName

```

UAL は、最大2年分の履歴を保持します。 サービスの実行中に管理者が UAL データを取得できるようにするため、UAL は、active database ファイル (現在の .mdb) のコピーを、WMI プロバイダーの使用について24時間ごとに*GUID .mdb*という名前のファイルに作成します。

年の初日に、UAL は新しい *GUID.mdb* を作成します。 古い*GUID .mdb*は、プロバイダーが使用するアーカイブとして保持されます。  2 年後に、元の *GUID.mdb* が上書きされます。

> [!IMPORTANT]
> 次の手順は上級ユーザーのみ実行する必要があります。この手順は、通常 UAL アプリケーション プログラミング インターフェイスの独自のインストールメンテーションをテストする開発者によって使用されます。

#### <a name="to-adjust-the-default-24-hour-interval-to-make-data-visible-to-the-wmi-provider"></a>既定の 24 時間間隔を調整して、データが WMI プロバイダーに表示されるようにするには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  Windows ロゴ キーを押しながら R キーを押し、「**cmd**」と入力してコマンド プロンプト ウィンドウを開きます。

3.  レジストリ値を追加します:  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\WMI\AutoLogger\Sum\PollingInterval (REG_DWORD)**

    > [!WARNING]
    > レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上のすべての重要なデータのバックアップを作成してください。

    次の例では、2分間の間隔を追加する方法を示しています (長期実行状態としては推奨されません): **REG add HKLM\System\CurrentControlSet\Control\WMI \\ AutoLogger\Sum/v POLLINGINTERVAL/T REG \_ DWORD/d 12万/f**

    時間値は、ミリ秒単位で表されます。 最小値は 60 秒で、最大値は 7 日間です。既定値は 24 時間です。

4.  サービス コンソールを使用して、User Access Logging Service を停止し、再開します。

## <a name="deleting-data-logged-by-ual"></a>UAL で記録されたデータの削除
UAL は、ミッション クリティカルなコンポーネントを意図したものではありません。 そのデザインは、高度なレベルの信頼性を維持しながら、ローカル システムの運用に与える影響をできる限り最小限にすることを目的にしています。 これにより、管理者は操作のニーズに合わせて UAL データベースとサポートファイル (\Windows\System32\LogFilesSUM\ ディレクトリ内のすべてのファイル) を手動で削除することもできます。

#### <a name="to-delete-data-logged-by-ual"></a>UAL で記録されたデータを削除するには

1. User Access Logging Service を停止します。

2. エクスプローラーを開きます。

3. **\Windows\System32\Logfiles\SUM \\ **にアクセスします。

4. フォルダー内のすべてのファイルを削除します。

## <a name="managing-ual-in-high-volume-environments"></a>大量のイベントが存在する環境での UAL の管理
ここでは、大量のクライアント ボリュームを含むサーバーで UAL を使用するときに管理者が実行できる内容について説明します。

UAL で記録できるアクセスの最大数は 1 日に 65,535 個です。UAL は、インターネットに直接接続されているサーバー (インターネットに直接接続されている Web サーバーなど)、またはサーバーの主な機能が非常に高パフォーマンスであるシナリオ (HPC ワークロード環境など) での使用はお勧めできません。 UAL は主に、大容量が予想される小規模、中規模、およびエンタープライズのイントラネットのシナリオを対象としていますが、インターネットに接続するトラフィックボリュームを定期的に処理する多数の展開ほどのものではありません。

**メモリの ual**: ual では拡張ストレージエンジン (ESE) が使用されるため、ual のメモリ要件は時間の経過と共に (またはクライアント要求の量によって) 増加します。 ただし、システム パフォーマンスへの影響を最小限に抑えるためにシステムから要求があった場合、メモリは放棄されます。

**ディスク上の ual**: ual のハードディスク要件は、次のようになります。

-   一意のクライアント レコードが 0 の場合: 22 M

-   一意のクライアント レコードが 50,000 個の場合: 80 M

-   一意のクライアント レコードが 500,000 個の場合: 384 M

-   一意のクライアント レコードが 1,000,000 個の場合: 729 M

## <a name="recovering-from-a-corrupt-state"></a>破損した状態からの回復
このセクションでは、UAL が拡張可能ストレージエンジン (ESE) を高レベルで使用する方法と、UAL データが破損または回復不能な場合に管理者が実行できる操作について説明します。

UAL ではシステム リソースの使用を最適化し、破損への耐性を確保するために ESE を使用します。  ESE の利点の詳細については、MSDN の「 [Extensible Storage Engine](/windows/win32/extensible-storage-engine/extensible-storage-engine) 」を参照してください。

UAL サービスが開始されるたびに、ESE でソフト回復が実行されます。 詳細については、MSDN の「 [Extensible Storage Engine Files (Extensible Storage Engine ファイル)](/windows/win32/extensible-storage-engine/extensible-storage-engine-files) 」を参照してください。

ソフト回復で問題が発生した場合は、ESE でクラッシュ回復が実行されます。 詳細については、MSDN の「 [JetInit Function (JetInit 関数)](/windows/win32/extensible-storage-engine/jetinit-function) 」を参照してください。

UAL が ESE ファイルの既存のセットで開始できない場合は、\Windows\System32\LogFiles\SUM\ ディレクトリ内のすべてのファイルが削除されます。 これらのファイルが削除されると、User Access Logging Service が再開されて、新しいファイルが作成されます。 UAL サービスは、新たにインストールされたコンピューターの場合と同様に再開されます。

> [!IMPORTANT]
> UAL データベース ディレクトリのファイルは移動または変更しないでください。 移動または変更すると、このセクションで説明したクリーンアップ ルーチンを含む回復手順が開始されます。 \Windows\System32\LogFiles\SUM\ ディレクトリのバックアップが必要な場合、このディレクトリのすべてのファイルをまとめてバックアップして、復元操作が期待どおりに機能するようにする必要があります。

## <a name="enable-work-folders-usage-license-tracking"></a>ワーク フォルダーの使用ライセンス追跡の有効化
ワーク フォルダー サーバーは、UAL を使用してクライアントの使用状況をレポートできます。 UAL とは異なり、ワーク フォルダーのログは既定では有効になりません。 次のレジストリ キーを変更することによって有効にできます。

```
Reg add HKLM\Software\Microsoft\Windows\CurrentVersion\SyncShareSrv /v EnableWorkFoldersUAL /t REG_DWORD /d 1
```

レジストリ キーを追加した後、ログを有効にするには、サーバーで SyncShareSvc サービスを再起動する必要があります。

ログを有効にした後は、クライアントがサーバーに接続するたびに、2 つの情報イベントが Windows ログ\アプリケーション チャネルに記録されます。 ワーク フォルダーの場合、各ユーザーが 1 台以上のクライアント デバイスを使用してサーバーに接続し、データ更新を 10 分ごとに確認できます。 サーバーに 1000 人のユーザーが接続して各ユーザーが 2 台のデバイスを使用すると、アプリケーション ログは 70 分ごとに上書きされ、関係のない問題のトラブルシューティングが困難になります。 これを回避するには、ユーザーアクセスログサービスを一時的に無効にするか、サーバーの Windows ログ \ アプリケーションチャネルのサイズを大きくします。

## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目

- [ユーザーアクセスログを使ってみる](get-started-with-user-access-logging.md)