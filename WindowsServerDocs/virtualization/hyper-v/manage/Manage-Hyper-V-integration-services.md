---
title: Hyper-v Integration Services を管理する
description: 統合サービスをオンまたはオフにし、必要に応じてインストールする方法について説明します。
ms.technology: compute-hyper-v
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server
ms.service: na
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: 39d57afbd8c4df78764c5975d4cc3d48848475c1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392765"
---
>適用対象: Windows 10、Windows Server 2016、Windows Server 2019

# <a name="manage-hyper-v-integration-services"></a>Hyper-v Integration Services を管理する

Hyper-v では、仮想マシンのパフォーマンスを向上させ、Hyper-v ホストとの双方向通信を活用することにより便利な機能を提供 Integration Services ます。 これらのサービスの多くは便利な (ゲストファイルコピーなど) であり、他のサービスは、統合されたデバイスドライバーなど、仮想マシンの機能にとって重要です。 この一連のサービスとドライバーは、"統合コンポーネント" と呼ばれることもあります。 個々の便宜的サービスが特定の仮想マシンに対して動作するかどうかを制御できます。 ドライバーのコンポーネントは、手動でサービスを提供するためのものではありません。

各統合サービスの詳細については、「 [hyper-v Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services)」を参照してください。

> [!IMPORTANT]
> を機能させるには、使用する各サービスがホストとゲストの両方で有効になっている必要があります。 Windows ゲストオペレーティングシステムでは、"Hyper-V ゲストサービスインターフェイス" を除くすべての統合サービスが既定でオンになっています。 サービスは、個別にオンまたはオフにすることができます。 次のセクションでは、その方法について説明します。

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>Hyper-v マネージャーを使用して統合サービスをオンまたはオフにする

1. 中央のウィンドウで、仮想マシンを右クリックし、 **[設定]** をクリックします。
  
2. **[設定]** ウィンドウの左ペインで、 **[管理]** の下にある **[Integration Services]** をクリックします。
  
Integration Services ウィンドウには、Hyper-v ホストで使用可能なすべての統合サービスの一覧と、ホストがバーチャルマシンを使用できるようにしたかどうかが表示されます。

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>PowerShell を使用して統合サービスをオンまたはオフにする

PowerShell でこれを行うには、 [Enable-VMIntegrationService](https://technet.microsoft.com/library/hh848500.aspx)を使用し、 [-Vmintegrationservice を無効](https://technet.microsoft.com/library/hh848488.aspx)にします。

次の例では、"demovm" という名前の仮想マシンのゲストファイルコピー統合サービスをオンまたはオフにする方法を示します。

1. 実行中の統合サービスの一覧を取得します。
  
    ``` PowerShell
    Get-VMIntegrationService -VMName "DemoVM"
    ```

1. 出力は次のようになります。

    ``` PowerShell
   VMName      Name                    Enabled PrimaryStatusDescription SecondaryStatusDescription
   ------      ----                    ------- ------------------------ --------------------------
   DemoVM      Guest Service Interface False   OK
   DemoVM      Heartbeat               True    OK                       OK
   DemoVM      Key-Value Pair Exchange True    OK
   DemoVM      Shutdown                True    OK
   DemoVM      Time Synchronization    True    OK
   DemoVM      VSS                     True    OK
   ```

1. ゲストサービスインターフェイスを有効にする:

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. ゲストサービスインターフェイスが有効になっていることを確認します。

   ```
   Get-VMIntegrationService -VMName "DemoVM" 
   ``` 

1. ゲストサービスインターフェイスをオフにする:

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```
   
## <a name="checking-the-guests-integration-services-version"></a>ゲストの integration services のバージョンを確認しています
ゲストの統合サービスが最新でない場合、一部の機能が正しく機能しないか、まったく動作しない可能性があります。 Windows のバージョン情報を取得するには、ゲストオペレーティングシステムにログオンし、コマンドプロンプトを開き、次のコマンドを実行します。

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```

以前のゲストオペレーティングシステムでは、利用可能なすべてのサービスが提供されません。 たとえば、Windows Server 2008 R2 ゲストに "Hyper-V ゲストサービスインターフェイス" を含めることはできません。

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Windows ゲストから統合サービスを開始および停止する
統合サービスを完全に機能させるには、対応するサービスがホスト上で有効になっていることに加え、ゲスト内で実行されている必要があります。 Windows ゲストでは、各統合サービスは標準の Windows サービスとして一覧表示されます。 コントロールパネルまたは PowerShell の [サービス] アプレットを使用して、これらのサービスを停止および開始できます。

> [!IMPORTANT]
> 統合サービスを停止すると、バーチャルマシンを管理するホストの機能に重大な影響を及ぼす可能性があります。 正しく機能するには、ホストとゲストの両方で、使用する各統合サービスを有効にする必要があります。
> ベストプラクティスとして、上記の手順に従って、Hyper-v からの統合サービスのみを制御することをお勧めします。 Hyper-v で状態を変更すると、ゲストオペレーティングシステムの一致するサービスが停止または自動的に開始されます。
> ゲストオペレーティングシステムでサービスを開始したが、Hyper-v で無効になっている場合、サービスは停止します。 Hyper-v で有効になっているゲストオペレーティングシステムでサービスを停止すると、Hyper-v によって、最終的に再び開始されます。 ゲストでサービスを無効にすると、Hyper-v は起動できなくなります。

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows サービスを使用して Windows ゲスト内の統合サービスを開始または停止する

1. 管理者として ```services.msc``` を実行するか、コントロールパネルの [サービス] アイコンをダブルクリックして、サービスマネージャーを開きます。

    ![[Windows サービス] ウィンドウを示すスクリーンショット](media/HVServices.png) 

1. "Hyper-v" で始まるサービスを検索します。 

1. 開始または停止するサービスを右クリックします。 目的のアクションをクリックします。

### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows PowerShell を使用して Windows ゲスト内の統合サービスを開始または停止する

1. Integration services の一覧を取得するには、次のように実行します。

    ```
    Get-Service -Name vm*
    ```

1.  出力は次のようになります。

    ```PowerShell
    Status   Name               DisplayName
    ------   ----               -----------
    Running  vmicguestinterface Hyper-V Guest Service Interface
    Running  vmicheartbeat      Hyper-V Heartbeat Service
    Running  vmickvpexchange    Hyper-V Data Exchange Service
    Running  vmicrdv            Hyper-V Remote Desktop Virtualizati...
    Running  vmicshutdown       Hyper-V Guest Shutdown Service
    Running  vmictimesync       Hyper-V Time Synchronization Service
    Stopped  vmicvmsession      Hyper-V VM Session Service
    Running  vmicvss            Hyper-V Volume Shadow Copy Requestor
    ```

1. サービスの[開始](https://technet.microsoft.com/library/hh849825.aspx)または[停止の](https://technet.microsoft.com/library/hh849790.aspx)いずれかを実行します。 たとえば、Windows PowerShell Direct を無効にするには、次のように実行します。

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Linux ゲストから統合サービスを開始および停止する 

一般的に、Linux 統合サービスは Linux カーネルで提供されます。 Linux integration services ドライバーには**hv_utils**という名前が付けられています。

1. **Hv_utils**が読み込まれているかどうかを確認するには、次のコマンドを使用します。

   ``` BASH
   lsmod | grep hv_utils
   ``` 
  
2. 出力は次のようになります。  
  
    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

3. 必要なデーモンが実行されているかどうかを確認するには、次のコマンドを使用します。
  
    ``` BASH
    ps -ef | grep hv
    ```
  
4. 出力は次のようになります。 
  
    ```BASH
    root       236     2  0 Jul11 ?        00:00:00 [hv_vmbus_con]
    root       237     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    ...
    root       252     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    root      1286     1  0 Jul11 ?        00:01:11 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9333     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9365     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_vss_daemon
    scooley  43774 43755  0 21:20 pts/0    00:00:00 grep --color=auto hv          
    ```

5. 使用できるデーモンを表示するには、次を実行します。

    ``` BASH
    compgen -c hv_
    ```
  
6. 出力は次のようになります。
  
    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon     
    ```
  
   次のような統合サービスデーモンが表示されます。 不足しているものがある場合は、システムでサポートされていないか、インストールされていない可能性があります。 詳細については、「 [Windows 上の hyper-v でサポートされている Linux および FreeBSD 仮想マシン](https://technet.microsoft.com/library/dn531030.aspx)」を参照してください。  
   - **hv_vss_daemon**: このデーモンは、Linux 仮想マシンのライブバックアップを作成するために必要です。
   - **hv_kvp_daemon**: このデーモンでは、組み込みキーと外部キーの値のペアを設定および照会できます。
   - **hv_fcopy_daemon**: このデーモンは、ホストとゲスト間にファイルコピーサービスを実装します。  

### <a name="examples"></a>例

これらの例では、`hv_kvp_daemon`という名前の KVP デーモンを停止して開始する方法を示します。

1. プロセス ID \(PID\) を使用して、デーモンのプロセスを停止します。 PID を検索するには、出力の2番目の列を確認するか、`pidof`を使用します。 Hyper-v デーモンはルートとして実行されるため、ルートアクセス許可が必要です。

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. すべての `hv_kvp_daemon` プロセスが失われたことを確認するには、次のように実行します。

    ```
    ps -ef | hv
    ```

1. デーモンを再起動するには、次のようにデーモンを root として実行します。

    ``` BASH
    sudo hv_kvp_daemon
    ``` 

1. `hv_kvp_daemon` プロセスが新しいプロセス ID と共に一覧表示されていることを確認するには、次のように実行します。

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>統合サービスを最新の状態に保つ

仮想マシンの最高のパフォーマンスと最新機能を利用するには、統合サービスを最新の状態に保つことをお勧めします。 これは、Windows Update から重要な更新プログラムを取得するように設定されている場合、ほとんどの Windows ゲストで既定で発生します。 現在のカーネルを使用している Linux ゲストは、カーネルを更新すると最新の統合コンポーネントを受け取ります。

**Windows 10 ホストで実行されている仮想マシンの場合:**

> [!NOTE]
> イメージファイル vmguest .iso は、不要になったため、Windows 10 の Hyper-v には含まれていません。

| Guest  | 更新方法 | 説明 |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | Windows Update | データ交換統合サービスが必要です。* |
| Windows 7 | Windows Update | データ交換統合サービスが必要です。* |
| Windows Vista (SP 2) | Windows Update | データ交換統合サービスが必要です。* |
| - | | |
| Windows Server 2016 | Windows Update | |
| Windows Server 半期チャネル | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | Windows Update | データ交換統合サービスが必要です。* |
| Windows Server 2008 R2 (SP 1) | Windows Update | データ交換統合サービスが必要です。* |
| Windows Server 2008 (SP 2) | Windows Update | Windows Server 2016 での拡張サポートのみ ([詳細](https://support.microsoft.com/lifecycle?p1=12925)はこちら)。 |
| Windows Home Server 2011 | Windows Update | Windows Server 2016 ではサポートされません ([詳細につい](https://support.microsoft.com/lifecycle?p1=15820)てはこちらを参照)。 |
| Windows Small Business Server 2011 | Windows Update | メインストリーム サポートではありません ([詳細](https://support.microsoft.com/lifecycle?p1=15817))。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用 Integration services はディストリビューションに組み込まれていますが、オプションの更新プログラムが利用可能な場合もあります。 ******** |

\* データ交換統合サービスを有効にできない場合、これらのゲストの統合サービスは、[ダウンロードセンター](https://support.microsoft.com/kb/3071740)からキャビネット (cab) ファイルとして入手できます。 Cab を適用する手順については、こちらの[ブログ記事](https://blogs.technet.com/b/virtualization/archive/2015/07/24/integration-components-available-for-virtual-machines-not-connected-to-windows-update.aspx)をご覧ください。

**Windows 8.1 ホストで実行されている仮想マシンの場合:**

| Guest  | 更新方法 | 説明 |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows 7 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Vista (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows XP (SP 2、SP 3) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| - | | |
| Windows Server 2016 | Windows Update | |
| Windows Server 半期チャネル | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2008 R2 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2008 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Home Server 2011 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Small Business Server 2011 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2003 R2 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2003 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用 Integration services はディストリビューションに組み込まれていますが、オプションの更新プログラムが利用可能な場合もあります。 ** |


**Windows 8 ホストで実行されている仮想マシンの場合:**

| Guest  | 更新方法 | 説明 |
|:---------|:---------|:---------|
| Windows 8.1 | Windows Update | |
| Windows 8 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows 7 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Vista (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows XP (SP 2、SP 3) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| - | | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2008 R2 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。|
| Windows Server 2008 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Home Server 2011 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Small Business Server 2011 | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2003 R2 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| Windows Server 2003 (SP 2) | 統合サービス ディスク | 以下の[手順](#install-or-update-integration-services)を参照してください。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用 Integration services はディストリビューションに組み込まれていますが、オプションの更新プログラムが利用可能な場合もあります。 ** |

Linux ゲストの詳細については、「 [Windows 上の hyper-v のサポートされている linux および FreeBSD 仮想マシン](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)」を参照してください。

## <a name="install-or-update-integration-services"></a>Integration services のインストールまたは更新

Windows Server 2016 と Windows 10 より前のホストでは、ゲストオペレーティングシステムの統合サービスを手動でインストールまたは更新する必要があります。 
  
1.  Hyper-V マネージャーを開きます。 サーバーマネージャーの ツール メニューで、 **Hyper-v マネージャー** をクリックします。  
  
2.  仮想マシンに接続します。 仮想マシンを右クリックし、 **[接続]** をクリックします。  
  
3.  [仮想マシン接続] の [操作] メニューで、 **[統合サービス セットアップ ディスクの挿入]** をクリックします。 この操作により、仮想 DVD ドライブにセットアップ ディスクが読み込まれます。 ゲストオペレーティングシステムによっては、インストールを手動で開始する必要がある場合があります。  
  
4.  インストールが完了すると、すべての統合サービスを使用できるようになります。

これらの手順は、オンライン仮想マシン用の Windows PowerShell セッション内で自動化または実行することはできません。 オフラインの VHDX イメージに適用できます。こちらの[ブログ記事をご覧](https://blogs.technet.microsoft.com/virtualization/2013/04/18/how-to-install-integration-services-when-the-virtual-machine-is-not-running/)ください。
