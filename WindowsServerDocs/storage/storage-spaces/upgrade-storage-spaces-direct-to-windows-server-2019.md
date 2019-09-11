---
title: 記憶域スペースダイレクトクラスターを Windows Server 2019 にアップグレードする
description: Vm の実行中または停止中に、記憶域スペースダイレクトクラスターを Windows Server 2019 にアップグレードする方法について説明します。
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
ms.openlocfilehash: 9966ee0fd3c0a2d1df0180bf177dec03343efc14
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867190"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>記憶域スペースダイレクトクラスターを Windows Server 2019 にアップグレードする

このトピックでは、記憶域スペースダイレクトクラスターを Windows Server 2019 にアップグレードする方法について説明します。 [クラスター OS のローリングアップグレードプロセス](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)を使用して windows server 2016 から windows server 2019 に記憶域スペースダイレクトクラスターをアップグレードするには、次の4つの方法があります。 vm の実行を維持する2つの方法と、すべての vm の停止に関係する2つの方法があります。 各方法には長所と短所が異なるため、組織のニーズに最も適したものを選択します。

- クラスター内の各サーバーで**vm が実行されているときのインプレースアップグレード**—このオプションでは、vm のダウンタイムは発生しませんが、各サーバーがアップグレードされた後に記憶域ジョブ (ミラー修復) が完了するまで待つ必要があります。

- クラスター内の各サーバーで**vm が実行されているときのクリーン OS インストール**-このオプションでは、vm のダウンタイムは発生しませんが、各サーバーをアップグレードした後に記憶域ジョブ (ミラー修復) が完了するまで待つ必要があります。各サーバーとそのアプリとロール。

- クラスター内の各サーバーで**vm が停止しているときのインプレースアップグレード**—このオプションを使用すると、vm のダウンタイムが発生しますが、記憶域ジョブ (ミラー修復) を待つ必要はありません。そのため、処理が高速になります。

- クラスター内の各サーバーで**vm が停止している間のクリーン OS インストール**-このオプションでは、vm のダウンタイムが発生しますが、記憶域ジョブ (ミラー修復) を待つ必要はありません。

## <a name="prerequisites-and-limitations"></a>前提条件と制限事項

アップグレードを続行する前に:

- アップグレードプロセス中に問題が発生した場合に備えて、使用可能なバックアップがあることを確認します。

- ハードウェアベンダーに、Windows Server 2019 でサポートされるサーバーの BIOS、ファームウェア、およびドライバーがあることを確認します。

アップグレードプロセスには、次のような制限があります。

- 176693.292 より前の Windows Server 2019 ビルドで記憶域スペースダイレクトを有効にするには、記憶域スペースダイレクトおよびソフトウェアで定義されたネットワーク機能を有効にするレジストリキーについて、Microsoft サポートに問い合わせる必要がある場合があります。 詳細については、マイクロソフトサポート技術情報の[記事 4464776](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking)を参照してください。

- ReFS ボリュームを使用してクラスターをアップグレードする場合、いくつかの制限があります。

- ReFS ボリュームではアップグレードが完全にサポートされていますが、アップグレードされたボリュームは、Windows Server 2019 での ReFS の機能強化の恩恵を受けることはできません。 これらの利点 (ミラーアクセラレータのパリティのパフォーマンスの向上など) には、新しく作成された Windows Server 2019 ReFS ボリュームが必要です。 つまり、 `New-Volume`コマンドレットまたはサーバーマネージャーを使用して新しいボリュームを作成する必要があります。 次に示すのは、新しいボリュームによって得られる ReFS 拡張機能の一部です。

    - **マップのログバイパス**: クラスター化された (記憶域スペースダイレクト) システムにのみ適用される、スタンドアロンの記憶域プールには適用されない ReFS のパフォーマンスの向上。

    - マルチ回復性を備えたボリュームに固有の、Windows Server 2019 の**圧縮**効率の向上。

- Windows Server 2016 記憶域スペースダイレクトクラスターサーバーをアップグレードする前に、サーバーをストレージメンテナンスモードにすることをお勧めします。 詳細については、「[記憶域スペースダイレクトのトラブルシューティング](troubleshooting-storage-spaces.md)」の「イベント5120」セクションを参照してください。 この問題は Windows Server 2016 で修正されていますが、ベストプラクティスとして、各記憶域スペースダイレクトサーバーをアップグレード中にストレージメンテナンスモードにすることをお勧めします。

- スイッチを使用するソフトウェア定義ネットワーク環境には既知の問題があります。 この問題には、Windows Server 2019 から Windows Server 2016 への Hyper-v VM のライブマイグレーション (以前のオペレーティングシステムへのライブマイグレーション) が含まれます。 ライブマイグレーションを成功させるには、Windows Server 2019 から Windows Server 2016 にライブ移行されている Vm の VM ネットワーク設定を変更することをお勧めします。 この問題は、2019-01D 修正プログラムロールアップパッケージ (ビルド 17763.292) で Windows Server 2019 に対して修正されています。 詳細については、マイクロソフトサポート技術情報の[記事 4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)を参照してください。

上記の既知の問題のため、次に示す4つのプロセスのいずれかを使用して Windows Server 2016 クラスターをアップグレードするのではなく、新しい Windows Server 2019 クラスターを構築し、以前のクラスターからデータをコピーすることを検討している場合があります。

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Vm の実行中にインプレースアップグレードを実行する

このオプションを使用すると、VM のダウンタイムは発生しませんが、各サーバーがアップグレードされた後に記憶域ジョブ (ミラー修復) が完了するまで待つ必要があります。 アップグレードプロセス中に個々のサーバーは順番に再起動されますが、クラスター内の残りのサーバーとすべての Vm は実行されたままになります。

1. クラスター内のすべてのサーバーに最新の Windows 更新プログラムがインストールされていることを確認します。 詳細については、「 [windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」を参照してください。 少なくとも、マイクロソフトサポート技術情報の[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 月19日、2019) をインストールしてください。 ビルド番号 (コマンドを`ver`参照) は14393.2828 以上である必要があります。

2. スイッチが設定されたソフトウェア定義ネットワークを使用している場合は、管理者特権の PowerShell セッションを開き、次のコマンドを実行して、クラスター上のすべての Vm で VM ライブマイグレーションの検証チェックを無効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 一度に1つのクラスターサーバーで次の手順を実行します。

   1. Hyper-v VM ライブマイグレーションを使用して、アップグレードしようとしているサーバーから実行中の Vm を移動します。

   2. 次の PowerShell コマンドを使用してクラスターサーバーを一時停止します。一部の内部グループは非表示になっていることに注意してください。 この手順は慎重に行うことをお勧めします。サーバーから Vm をまだライブ移行していない場合は、このコマンドレットによって実行されるため、必要に応じて前の手順を省略できます。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 次の PowerShell コマンドを実行して、サーバーをストレージメンテナンスモードにします。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 次のコマンドレットを実行して、 **OperationalStatus**値が**メンテナンスモードで**あることを確認します。

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. **Setup.exe**を実行し、[個人用ファイルとアプリを保持する] オプションを使用して、サーバーで Windows server 2019 のアップグレードインストールを実行します。 インストールが完了すると、サーバーがクラスターに残り、クラスターサービスが自動的に開始されます。

   6. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。 詳細については、「 [windows 10 および Windows Server 2019 の更新履歴](https://support.microsoft.com/help/4464619/windows-10-update-history)」を参照してください。 ビルド番号 (コマンドを`ver`参照) は17763.292 以上である必要があります。

   7. 次の PowerShell コマンドを使用して、ストレージメンテナンスモードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   8. 次の PowerShell コマンドを使用して、サーバーを再開します。

       ```PowerShell
       Resume-ClusterNode
       ```

   9. 記憶域の修復ジョブが完了し、すべてのディスクが正常な状態に戻るまで待機します。 サーバーのアップグレード中に実行されている Vm の数によっては、時間がかかることがあります。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。

5. すべてのサーバーを Windows Server 2019 にアップグレードした後、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > クラスターの機能レベルをできるだけ早く更新することをお勧めしますが、技術的には最大4週間で済みます。

6. クラスターの機能レベルが更新された後、次のコマンドレットを使用して記憶域プールを更新します。 この時点で、などの新しいコマンド`Get-ClusterPerf`レットは、クラスター内の任意のサーバーで完全に動作します。

   ```PowerShell
   Update-StoragePool
   ```

7. 必要に応じて、各 vm を停止し、 `Update-VMVersion`コマンドレットを使用して vm を再起動して、vm の構成レベルをアップグレードします。

8. スイッチおよび無効化された VM ライブマイグレーションに関するチェックをオンにした状態でソフトウェア定義ネットワークを使用している場合は、次のコマンドレットを使用して、VM ライブ検証チェックを再度有効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. アップグレードしたクラスターが想定どおりに機能することを確認します。 ロールは正常にフェールオーバーする必要があり、VM のライブマイグレーションがクラスターで使用されている場合、Vm はライブマイグレーションを正常に行う必要があります。

10. クラスター検証 (`Test-Cluster`) を実行し、クラスター検証レポートを調べて、クラスターを検証します。

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Vm の実行中に OS のクリーンインストールを実行する

このオプションを使用すると、VM のダウンタイムは発生しませんが、各サーバーがアップグレードされた後に記憶域ジョブ (ミラー修復) が完了するまで待つ必要があります。 アップグレードプロセス中に個々のサーバーは順番に再起動されますが、クラスター内の残りのサーバーとすべての Vm は実行されたままになります。

1. クラスター内のすべてのサーバーで最新の更新プログラムが実行されていることを確認します。 詳細については、「 [windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」を参照してください。 少なくとも、マイクロソフトサポート技術情報の[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 月19日、2019) をインストールしてください。 ビルド番号 (コマンドを`ver`参照) は14393.2828 以上である必要があります。

2. スイッチが設定されたソフトウェア定義ネットワークを使用している場合は、管理者特権の PowerShell セッションを開き、次のコマンドを実行して、クラスター上のすべての Vm で VM ライブマイグレーションの検証チェックを無効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 一度に1つのクラスターサーバーで次の手順を実行します。

   1. Hyper-v VM ライブマイグレーションを使用して、アップグレードしようとしているサーバーから実行中の Vm を移動します。

   2. 次の PowerShell コマンドを使用してクラスターサーバーを一時停止します。一部の内部グループは非表示になっていることに注意してください。 この手順は慎重に行うことをお勧めします。サーバーから Vm をまだライブ移行していない場合は、このコマンドレットによって実行されるため、必要に応じて前の手順を省略できます。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 次の PowerShell コマンドを実行して、サーバーをストレージメンテナンスモードにします。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 次のコマンドレットを実行して、 **OperationalStatus**値が**メンテナンスモードで**あることを確認します。

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  次の PowerShell コマンドを実行して、クラスターからサーバーを削除します。  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. サーバーで Windows Server 2019 のクリーンインストールを実行する: システムドライブのフォーマットを設定し、 **setup.exe**を実行して、"Nothing" オプションを使用します。 セットアップの完了後にサーバーの id、役割、機能、およびアプリケーションを構成し、サーバーを再起動する必要があります。

   5. Hyper-v の役割とフェールオーバークラスタリング機能をサーバーにインストールします ( `Install-WindowsFeature`コマンドレットを使用できます)。

   6. 記憶域スペースダイレクトで使用するために、サーバーの製造元によって承認されたハードウェアの最新のストレージとネットワークドライバーをインストールします。

   7. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。 詳細については、「 [windows 10 および Windows Server 2019 の更新履歴](https://support.microsoft.com/help/4464619/windows-10-update-history)」を参照してください。 ビルド番号 (コマンドを`ver`参照) は17763.292 以上である必要があります。

   8. 次の PowerShell コマンドを使用して、サーバーをクラスターに再度参加させます。

       ```PowerShell
       Add-ClusterNode
       ```

   9. 次の PowerShell コマンドを使用して、ストレージメンテナンスモードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. 記憶域の修復ジョブが完了し、すべてのディスクが正常な状態に戻るまで待機します。 サーバーのアップグレード中に実行されている Vm の数によっては、時間がかかることがあります。 実行するコマンドを次に示します。

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. クラスター内の次のサーバーをアップグレードします。

5. すべてのサーバーを Windows Server 2019 にアップグレードした後、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > クラスターの機能レベルをできるだけ早く更新することをお勧めしますが、技術的には最大4週間で済みます。

6. クラスターの機能レベルが更新された後、次のコマンドレットを使用して記憶域プールを更新します。 この時点で、などの新しいコマンド`Get-ClusterPerf`レットは、クラスター内の任意のサーバーで完全に動作します。

   ```PowerShell
   Update-StoragePool
   ```

7. 必要に応じて、各 vm を停止し、 `Update-VMVersion`コマンドレットを使用して vm を再起動して、vm の構成レベルをアップグレードします。

8. スイッチおよび無効化された VM ライブマイグレーションに関するチェックをオンにした状態でソフトウェア定義ネットワークを使用している場合は、次のコマンドレットを使用して、VM ライブ検証チェックを再度有効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. アップグレードしたクラスターが想定どおりに機能することを確認します。 ロールは正常にフェールオーバーする必要があり、VM のライブマイグレーションがクラスターで使用されている場合、Vm はライブマイグレーションを正常に行う必要があります。

10. クラスター検証 (`Test-Cluster`) を実行し、クラスター検証レポートを調べて、クラスターを検証します。

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Vm の停止中にインプレースアップグレードを実行する

このオプションを使用すると、VM のダウンタイムが発生しますが、アップグレード中に Vm を実行したままにした場合よりも時間が短くなります。各サーバーをアップグレードした後に記憶域ジョブ (ミラー修復) が完了するまで待機する必要がないためです。 個々のサーバーはアップグレード処理中に順番に再起動されますが、クラスター内の残りのサーバーは実行されたままになります。

1. クラスター内のすべてのサーバーで最新の更新プログラムが実行されていることを確認します。 詳細については、「 [windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」を参照してください。 少なくとも、マイクロソフトサポート技術情報の[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 月19日、2019) をインストールしてください。 ビルド番号 (コマンドを`ver`参照) は14393.2828 以上である必要があります。

2. クラスターで実行されている Vm を停止します。

3. 一度に1つのクラスターサーバーで次の手順を実行します。

   1. 次の PowerShell コマンドを使用してクラスターサーバーを一時停止します。一部の内部グループは非表示になっていることに注意してください。 この手順は、慎重に行うことをお勧めします。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. 次の PowerShell コマンドを実行して、サーバーをストレージメンテナンスモードにします。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. 次のコマンドレットを実行して、 **OperationalStatus**値が**メンテナンスモードで**あることを確認します。

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. **Setup.exe**を実行し、[個人用ファイルとアプリを保持する] オプションを使用して、サーバーで Windows server 2019 のアップグレードインストールを実行します。  
   インストールが完了すると、サーバーがクラスターに残り、クラスターサービスが自動的に開始されます。

   5.  新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。  
   詳細については、「 [windows 10 および Windows Server 2019 の更新履歴](https://support.microsoft.com/help/4464619/windows-10-update-history)」を参照してください。
   ビルド番号 (コマンドを`ver`参照) は17763.292 以上である必要があります。

   6.  次の PowerShell コマンドを使用して、ストレージメンテナンスモードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   7.  次の PowerShell コマンドを使用して、サーバーを再開します。

       ```PowerShell
       Resume-ClusterNode
       ```

   8.  記憶域の修復ジョブが完了し、すべてのディスクが正常な状態に戻るまで待機します。  
   Vm が実行されていないため、これは比較的高速です。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。
5. すべてのサーバーを Windows Server 2019 にアップグレードした後、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   クラスターの機能レベルをできるだけ早く更新することをお勧めしますが、技術的には最大4週間で済みます。

6. クラスターの機能レベルが更新された後、次のコマンドレットを使用して記憶域プールを更新します。  
   この時点で、などの新しいコマンド`Get-ClusterPerf`レットは、クラスター内の任意のサーバーで完全に動作します。

   ```PowerShell
   Update-StoragePool
   ```

7. クラスターで Vm を起動し、正常に動作していることを確認します。

8. 必要に応じて、各 vm を停止し、 `Update-VMVersion`コマンドレットを使用して vm を再起動して、vm の構成レベルをアップグレードします。

9. アップグレードしたクラスターが想定どおりに機能することを確認します。  
   ロールは正常にフェールオーバーする必要があり、VM のライブマイグレーションがクラスターで使用されている場合、Vm はライブマイグレーションを正常に行う必要があります。

10. クラスター検証 (`Test-Cluster`) を実行し、クラスター検証レポートを調べて、クラスターを検証します。

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Vm の停止中に OS のクリーンインストールを実行する

このオプションを使用すると、VM のダウンタイムが発生しますが、アップグレード中に Vm を実行したままにした場合よりも時間が短くなります。各サーバーをアップグレードした後に記憶域ジョブ (ミラー修復) が完了するまで待機する必要がないためです。 個々のサーバーはアップグレード処理中に順番に再起動されますが、クラスター内の残りのサーバーは実行されたままになります。

1. クラスター内のすべてのサーバーで最新の更新プログラムが実行されていることを確認します。  
   詳細については、「 [windows 10 および Windows Server 2016 の更新履歴](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)」を参照してください。
   少なくとも、マイクロソフトサポート技術情報の[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 月19日、2019) をインストールしてください。 ビルド番号 (コマンドを`ver`参照) は14393.2828 以上である必要があります。

2. クラスターで実行されている Vm を停止します。

3. 一度に1つのクラスターサーバーで次の手順を実行します。

   2. 次の PowerShell コマンドを使用してクラスターサーバーを一時停止します。一部の内部グループは非表示になっていることに注意してください。  
      この手順は、慎重に行うことをお勧めします。

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. 次の PowerShell コマンドを実行して、サーバーをストレージメンテナンスモードにします。

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. 次のコマンドレットを実行して、 **OperationalStatus**値が**メンテナンスモードで**あることを確認します。

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. 次の PowerShell コマンドを実行して、クラスターからサーバーを削除します。  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. サーバーで Windows Server 2019 のクリーンインストールを実行する: システムドライブのフォーマットを設定し、 **setup.exe**を実行して、"Nothing" オプションを使用します。  
      セットアップの完了後にサーバーの id、役割、機能、およびアプリケーションを構成し、サーバーを再起動する必要があります。

   7. Hyper-v の役割とフェールオーバークラスタリング機能をサーバーにインストールします ( `Install-WindowsFeature`コマンドレットを使用できます)。

   8. 記憶域スペースダイレクトで使用するために、サーバーの製造元によって承認されたハードウェアの最新のストレージとネットワークドライバーをインストールします。

   9. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。  
      詳細については、「 [windows 10 および Windows Server 2019 の更新履歴](https://support.microsoft.com/help/4464619/windows-10-update-history)」を参照してください。
      ビルド番号 (コマンドを`ver`参照) は17763.292 以上である必要があります。

   10. 次の PowerShell コマンドを使用して、サーバーをクラスターに再度参加させます。

      ```PowerShell
      Add-ClusterNode
      ```

   11. 次の PowerShell コマンドを使用して、ストレージメンテナンスモードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. 記憶域の修復ジョブが完了し、すべてのディスクが正常な状態に戻るまで待機します。  
       サーバーのアップグレード中に実行されている Vm の数によっては、時間がかかることがあります。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。

5. すべてのサーバーを Windows Server 2019 にアップグレードした後、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   クラスターの機能レベルをできるだけ早く更新することをお勧めしますが、技術的には最大4週間で済みます。

6. クラスターの機能レベルが更新された後、次のコマンドレットを使用して記憶域プールを更新します。  
   この時点で、などの新しいコマンド`Get-ClusterPerf`レットは、クラスター内の任意のサーバーで完全に動作します。

   ```PowerShell
   Update-StoragePool
   ```

7. クラスターで Vm を起動し、正常に動作していることを確認します。

8. 必要に応じて、各 vm を停止し、 `Update-VMVersion`コマンドレットを使用して vm を再起動して、vm の構成レベルをアップグレードします。

9. アップグレードしたクラスターが想定どおりに機能することを確認します。  
   ロールは正常にフェールオーバーする必要があり、VM のライブマイグレーションがクラスターで使用されている場合、Vm はライブマイグレーションを正常に行う必要があります。

10. クラスター検証 (`Test-Cluster`) を実行し、クラスター検証レポートを調べて、クラスターを検証します。
