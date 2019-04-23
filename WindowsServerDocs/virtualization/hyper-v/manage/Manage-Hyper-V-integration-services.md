---
title: HYPER-V 統合サービスを管理します。
description: 統合サービスを有効または無効にし、必要な場合は、それらをインストールする方法について説明します
ms.technology: compute-hyper-v
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.service: na
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: b049efc61d5060791574f20fcdd8b369a26f0507
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890253"
---
>適用先:Windows 10、Windows Server 2016、Windows Server 2019

# <a name="manage-hyper-v-integration-services"></a>HYPER-V 統合サービスを管理します。

HYPER-V 統合サービスは仮想マシンのパフォーマンスを強化し、HYPER-V ホストとの双方向通信を利用して、便利な機能を提供します。 これらのサービスの多くは、合成デバイス ドライバーなどの仮想マシンの機能に重要な他のユーザーは、ゲスト ファイル コピーなど、便利な機能です。 これは、一連のサービスとドライバーは、「統合コンポーネント」と呼ばれることがあります。 個々 の便利なサービスが、指定された仮想マシンの動作するかどうかを制御できます。 ドライバー コンポーネントは、手動で処理されるものではありません。

各統合サービスに関する詳細については、次を参照してください。 [Hyper-v 統合サービス](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services)します。

>[!IMPORTANT]
>使用する各サービスは、機能するために、ホストとゲストの両方で有効にする必要があります。 「HYPER-V ゲスト サービス インターフェイス」を除くすべての integration services では、Windows ゲスト オペレーティング システムでは既定でです。 サービスを有効または無効に個別にします。 方法については、次のセクションで説明します。

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>オンまたはオフ、HYPER-V マネージャーを使用して、統合サービスを有効にします。

1. 中央のウィンドウから仮想マシンを右クリックし、をクリックして**設定**します。
  
2. 左側のウィンドウから、**設定**ウィンドウで、**管理**、 をクリックして**Integration Services**します。
  
Integration Services ウィンドウには、HYPER-V ホストで、使用可能なすべての integration services が一覧表示し、ホストがそれらを使用する仮想マシンを有効にするかどうか。

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>オンまたはオフ、PowerShell を使用して、統合サービスを有効にします。

これを PowerShell では、使用[Enable-vmintegrationservice](https://technet.microsoft.com/library/hh848500.aspx)と[Disable-vmintegrationservice](https://technet.microsoft.com/library/hh848488.aspx)します。

次の例では、ゲスト ファイル コピー統合サービス オン/オフ"demovm"という名前の仮想マシンにすることを示します。

1. 統合サービスを実行しているの一覧を取得します。
  
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

1. ゲスト サービス インターフェイスをオンにします。

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. ゲスト サービス インターフェイスが有効になっていることを確認します。

   ```
   Get-VMIntegrationService -VMName "DemoVM" 
   ``` 

1. ゲスト サービス インターフェイスをオフにします。

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```
   
## <a name="checking-the-guests-integration-services-version"></a>ゲストの統合サービスのバージョンの確認
一部の機能が機能しないか正しく、またはまったくゲストの統合サービスが最新でない場合。 Windows、ログオン、ゲスト オペレーティング システムのバージョン情報を取得するには、コマンド プロンプトを開きし、このコマンドを実行します。

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```
以前のゲスト オペレーティング システムのすべての利用可能なサービスではありません。 たとえば、Windows Server 2008 R2 ゲストでは、「HYPER-V ゲスト サービス インターフェイス」を含めることはできません。

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>開始および停止から Windows ゲスト統合サービス
統合サービスを完全に機能させるためには、その対応するサービスは、ホストで有効にされているだけでなく、ゲスト内で実行する必要があります。 Windows ゲストでは、各統合サービスは、標準の Windows サービスとして一覧表示されます。 コントロール パネルまたは PowerShell でのサービス アプレットを使用して、停止し、これらのサービスを開始できます。

>[!IMPORTANT]
> 統合サービスを停止すると、仮想マシンを管理するホストの機能に大きく影響可能性があります。 正常に機能するには、ホストとゲストの両方で使用する各統合サービスを有効にする必要があります。
> ベスト プラクティスとして、上記の手順を使用して HYPER-V から統合サービスを制御する必要がありますだけです。 ゲスト オペレーティング システムに一致するサービスを停止または HYPER-V では、その状態を変更すると、自動的に開始します。
> ゲスト オペレーティング システムでサービスを開始する、HYPER-V で無効になっている場合は、サービスは停止します。 HYPER-V で有効になっているゲスト オペレーティング システムでサービスを停止した場合、HYPER-V 最終的に再び開始されます。 ゲスト サービスを無効にした場合、HYPER-V は起動できません。

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows サービスを使用して開始または Windows ゲスト内で統合サービスを停止するには

1. 実行してサービス マネージャーを開く```services.msc```管理者として、またはコントロール パネルの [サービス] アイコンをダブルクリックします。

    ![Windows サービス ウィンドウを示すスクリーン ショット](media/HVServices.png) 

1. "ハイパー-V"で始まるサービスを検索します。 

1. 開始または停止サービスを右クリックします。 目的のアクションをクリックします。


### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows PowerShell を使用して開始または Windows ゲスト内で統合サービスを停止するには

1. Integration services の一覧を取得するには、次のコマンドを実行します。

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

1. いずれかを実行[Start-service](https://technet.microsoft.com/library/hh849825.aspx)または[Stop-service](https://technet.microsoft.com/library/hh849790.aspx)します。 たとえば、Windows PowerShell ダイレクトを無効にするには、次のように実行します。

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>起動し、Linux ゲストから統合サービスの停止 

一般的に、Linux 統合サービスは Linux カーネルで提供されます。 Linux 統合サービス ドライバーの名前は**hv_utils**します。

1.  確認する**hv_utils**が読み込まれる場合は、このコマンドを使用します。

    ``` BASH
    lsmod | grep hv_utils
    ``` 
  
1. 出力は次のようになります。  
  
    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

1. 必要なデーモンが実行されているかどうかに検索するには、このコマンドを使用します。
  
    ``` BASH
    ps -ef | grep hv
    ```
  
1. 出力は次のようになります。 
  
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

1. 使用できるデーモンを表示するには、次を実行します。

    ``` BASH
    compgen -c hv_
    ```
  
1. 出力は次のようになります。
  
    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon     
    ```
  
 表示される統合サービス デーモンは、次に示します。 いずれかが存在しない場合は、システムでサポートされる可能性がありますいないまたは、インストールできない可能性があります。 詳細については、「 [Windows 上の HYPER-V ではサポートされている Linux および FreeBSD の仮想マシン](https://technet.microsoft.com/library/dn531030.aspx)します。  
  - **hv_vss_daemon**:Linux 仮想マシンのライブ バックアップを作成するには、このデーモンが必要です。
  - **hv_kvp_daemon**:このデーモンは、設定および照会の組み込みと外部キー値のペアを使用できます。
  - **hv_fcopy_daemon**:このデーモンは、ファイル サービス、ホストとゲスト間のコピーを実装します。  

### <a name="examples"></a>例

これらの例を示しますの停止と開始という、KVP デーモン`hv_kvp_daemon`します。

1. プロセス ID を使用して、 \(PID\)デーモンのプロセスを停止します。 PID を検索するには、出力の 2 番目の列を確認または使用`pidof`します。 HYPER-V デーモンは、ルート アクセスを許可する必要がありますので、ルートとして実行します。

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. 確認するすべて`hv_kvp_daemon`プロセスはなくなりを実行します。

    ```
    ps -ef | hv
    ```

1. デーモンをもう一度開始するには、ルートとしてデーモンを実行します。

    ``` BASH
    sudo hv_kvp_daemon
    ``` 

1. 確認する、`hv_kvp_daemon`プロセスの実行、新しいプロセス ID が記載されています。

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>統合サービスを常に最新の状態に保つ

統合サービス、仮想マシンの最適なパフォーマンスと最新の機能を取得する最新の状態をままことをお勧めします。 これは既定で Windows ゲストのほとんどは Windows Update から重要な更新プログラムを取得するように設定する場合がします。 現在のカーネルを使用して Linux ゲストのカーネルを更新するときに、最新の統合コンポーネントが表示されます。

**Windows 10 ホストで実行されている仮想マシンの場合:**

> [!NOTE]
> イメージ ファイルの vmguest.iso は不要になったため、Windows 10 での HYPER-V に含まれてはありません。

| Guest  | 更新方法 | メモ |
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
| Windows Server 2008 (SP 2) | Windows Update | Windows Server 2016 でのみサポートを拡張 ([についてお読みください](https://support.microsoft.com/lifecycle?p1=12925))。 |
| Windows Home Server 2011 | Windows Update | Windows Server 2016 ではサポートされません ([についてお読みください](https://support.microsoft.com/lifecycle?p1=15820))。 |
| Windows Small Business Server 2011 | Windows Update | メインストリーム サポートではありません ([詳細](https://support.microsoft.com/lifecycle?p1=15817))。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用の統合サービスは、ディストリビューションに組み込まれてもありますオプションの更新プログラム利用可能です。 ******** |

\* これらのゲスト統合サービスはから利用可能な場合は、データ交換統合サービスを有効にすることはできません、[ダウンロード センター](https://support.microsoft.com/kb/3071740)で、キャビネット (cab) ファイル。 Cab を適用する手順については、この[ブログの投稿](https://blogs.technet.com/b/virtualization/archive/2015/07/24/integration-components-available-for-virtual-machines-not-connected-to-windows-update.aspx)します。

**Windows 8.1 ホストで実行されている仮想マシンの場合:**

| Guest  | 更新方法 | メモ |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows 7 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Vista (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows XP (SP 2、SP 3) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| - | | |
| Windows Server 2016 | Windows Update | |
| Windows Server 半期チャネル | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2008 R2 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2008 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Home Server 2011 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Small Business Server 2011 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2003 R2 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2003 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用の統合サービスは、ディストリビューションに組み込まれてもありますオプションの更新プログラム利用可能です。 ** |


**Windows 8 ホストで実行されている仮想マシンの場合:**

| Guest  | 更新方法 | メモ |
|:---------|:---------|:---------|
| Windows 8.1 | Windows Update | |
| Windows 8 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows 7 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Vista (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows XP (SP 2、SP 3) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| - | | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2008 R2 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。|
| Windows Server 2008 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Home Server 2011 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Small Business Server 2011 | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2003 R2 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| Windows Server 2003 (SP 2) | 統合サービス ディスク | 参照してください[指示](#install-or-update-integration-services)、後述します。 |
| - | | |
| Linux ゲスト | パッケージ マネージャー | Linux 用の統合サービスは、ディストリビューションに組み込まれてもありますオプションの更新プログラム利用可能です。 ** |

Linux ゲストの詳細については、次を参照してください。 [Windows 上の Hyper-v ではサポートされている Linux および FreeBSD の仮想マシン](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)します。

## <a name="install-or-update-integration-services"></a>インストールまたは統合サービスの更新

ホストの Windows Server 2016 および Windows 10 より前する必要があります手動でインストールまたはゲスト オペレーティング システムの統合サービスを更新します。 
  
1.  Hyper-V マネージャーを開きます。 サーバー マネージャーの [ツール] メニューからクリックして **、HYPER-V Manager**します。  
  
2.  仮想マシンに接続します。 仮想マシンを右クリックし、をクリックして**Connect**します。  
  
3.  [仮想マシン接続] の [操作] メニューで、**[統合サービス セットアップ ディスクの挿入]** をクリックします。 この操作により、仮想 DVD ドライブにセットアップ ディスクが読み込まれます。 ゲスト オペレーティング システムによっては、手動でインストールを開始する必要があります。  
  
4.  インストールが完了すると、すべての統合サービスを使用できるようになります。

次の手順は、自動またはオンラインの仮想マシンの Windows PowerShell セッションで行われたことはできません。 オフラインの VHDX イメージに適用することができます。[このブログの投稿を参照してください。](https://blogs.technet.microsoft.com/virtualization/2013/04/18/how-to-install-integration-services-when-the-virtual-machine-is-not-running/)します。
