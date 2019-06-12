---
title: Windows Server 2019 に記憶域スペース ダイレクト クラスターをアップグレードします。
description: Windows Server 2019 - またはいずれかを実行する Vm を維持しながら、停止中に記憶域スペース ダイレクト クラスターをアップグレードする方法。
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
ms.openlocfilehash: 9db92aa33cde9b2beed11149dae06bb3af2b5a03
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455408"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>Windows Server 2019 に記憶域スペース ダイレクト クラスターをアップグレードします。

このトピックでは、Windows Server 2019 に記憶域スペース ダイレクト クラスターをアップグレードする方法について説明します。 4 つのアプローチを使用して Windows Server 2019、記憶域スペース ダイレクト クラスターから Windows Server 2016 へのアップグレードには、[クラスター OS のローリング アップグレード プロセス](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)— を実行する Vm を保持する 2 つと 2 つの関連します。すべての Vm を停止しています。 各アプローチには、それぞれ長所と短所、そのいずれか、組織のニーズに最適な選択があります。

- **インプレース アップグレード中に、Vm が実行されている**クラスター内の各サーバーで、このオプションには、VM のダウンタイムは発生しないが、記憶域ジョブ (ミラー修復) 各サーバーをアップグレードした後に完了するまで待機する必要があります。

- **Vm が実行中にクリーンアップ OS インストール**クラスター内の各サーバーで、このオプションには、VM のダウンタイムは発生しないが、各サーバーとすべての記憶域ジョブ (ミラー修復) 各サーバーをアップグレードすると、設定する必要がありますを完了するまで待つ必要がありますそのアプリとロールをもう一度です。

- **インプレース アップグレードの Vm が停止している間**クラスター内の各サーバーで、このオプションが VM のダウンタイムが生じますが、高速ですが、記憶域ジョブ (ミラー修復) を待機する必要はありません。

- **Vm が停止している間にクリーンアップ OS がインストール**クラスター内の各サーバーで、このオプションが VM のダウンタイムが生じますが、ストレージの高速ですが、ジョブ (ミラー修復) を待機する必要はありません。

## <a name="prerequisites-and-limitations"></a>前提条件と制限事項

アップグレードする前。

- アップグレード処理中に問題がある場合、使用可能なバックアップがあることを確認します。

- ハードウェア ベンダーには、BIOS、ファームウェア、および Windows Server 2019 でサポートされるサーバー用のドライバーが持つことを確認します。

これには注意すべきアップグレード プロセスをいくつかの制限があります。

- を有効にする記憶域スペース ダイレクトと Windows Server 2019 ビルド 176693.292 より前に、顧客は、記憶域スペース ダイレクトとソフトウェアによるネットワーク制御の機能を有効にするレジストリ キーを Microsoft サポートにお問い合わせください必要があります。 詳細については、マイクロソフト サポート技術情報を参照してください。[記事 4464776](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking)します。

- ReFS ボリュームを使用するクラスターをアップグレードする場合は、いくつかの制限があります。

- ReFS ボリュームで完全にサポートをアップグレードする、ただし、アップグレードされたボリュームにとってメリットがありません ReFS からでは、Windows Server 2019 の機能強化。 ミラー アクセラレータを使用したパリティの場合、パフォーマンスの向上など、これらの特典には、新しく作成された Windows Server 2019 ReFS ボリュームが必要です。 使用して新しいボリュームを作成しなければ、つまり、`New-Volume`コマンドレットまたはサーバー マネージャー。 新しいボリュームを取得、ReFS の拡張機能の一部を次に示します。

    - **マップのログ バイパス**: のみクラスター (記憶域スペース ダイレクト) システムに適用され、スタンドアロンの記憶域プールには適用されませんを ReFS でパフォーマンスが向上します。

    - **圧縮**マルチ回復力のあるボリュームに固有の Windows Server 2019 で効率性が向上します。

- Windows Server 2016 記憶域スペース ダイレクト クラスター サーバーをアップグレードする前に、サーバーを記憶域メンテナンス モードに配置することをお勧めします。 詳細については、のイベント 5120 セクションを参照してください。[記憶域スペース ダイレクトのトラブルシューティングを行う](troubleshooting-storage-spaces.md)します。 この問題は、Windows Server 2016 で修正されていますが、ベスト プラクティスとして、アップグレード中に記憶域メンテナンス モードに各記憶域スペース ダイレクトのサーバーを配置お勧めします。

- SET スイッチを使用してソフトウェアによるネットワーク制御の環境での既知の問題があります。 この問題には、HYPER-V VM のライブ マイグレーション Windows Server 2019 から Windows Server 2016 (以前のオペレーティング システムへのライブ マイグレーション) にはが含まれます。 ライブ移行を成功させるには、Windows Server 2016 を Windows Server 2019 からライブで移行したされている Vm 上の VM ネットワーク設定を変更するをお勧めします。 この問題は、2019 01 D の修正プログラム ロールアップ パッケージで Windows Server 2019 の修正はとも呼ばれる 17763.292 をビルドします。 詳細については、マイクロソフト サポート技術情報を参照してください。[記事 4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)します。

一部のお客様には、既知の問題により、新しい Windows Server 2019 クラスターを構築し、次に示す 4 つのプロセスのいずれかを使用して、Windows Server 2016 クラスターをアップグレードする代わりに、以前のクラスターからデータをコピーを検討できます。

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Vm が実行されているときに、インプレース アップグレードを実行します。

このオプションには、VM のダウンタイムは発生しないが、記憶域ジョブ (ミラー修復) 各サーバーをアップグレードした後に完了するまで待機する必要があります。 個々 のサーバーは、アップグレード処理中に順番に再起動は、すべての Vm と同様に、クラスター内の残りのサーバーが実行されているままです。

1. クラスター内のすべてのサーバーに最新の Windows 更新プログラムがインストールされていることを確認します。 詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)します。 マイクロソフト サポート技術情報のインストールには、少なくとも[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 年 2 月 19日)。 ビルド番号 (を参照してください`ver`コマンド) 14393.2828 以上にする必要があります。

2. を使用してソフトウェアによるネットワーク制御スイッチのセットを使用している場合は、管理者特権の PowerShell セッションを開き、クラスター上のすべての Vm で VM のライブ マイグレーションの検証チェックを無効にするには、次のコマンドを実行します。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 一度に 1 つのクラスター サーバーで、次の手順に従います。

   1. HYPER-V VM のライブ マイグレーションを使用すると、アップグレードしようとしているサーバーから Vm を実行して移動できます。

   2. 次の PowerShell コマンドを使用して、クラスターのサーバーを一時停止 — 一部の内部グループが非表示に注意してください。 注意が必要です、この手順をお勧め-既にライブをしていない場合、ためでしたをスキップ、前の手順を使用する場合に、このコマンドレットには、サーバーから Vm を移行します。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 次の PowerShell コマンドを実行して、記憶域メンテナンス モードでサーバーを配置します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 確認する次のコマンドレットを実行する、 **OperationalStatus**値は**メンテナンス モードで**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. 実行して、サーバーで Windows Server 2019 のアップグレードのインストールを実行**setup.exe** 「個人ファイルとアプリを保持」オプションを使用します。 インストールが完了した後、クラスターとクラスターで、サーバーはサービスの開始に自動的にします。

   6. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。 詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2019](https://support.microsoft.com/help/4464619/windows-10-update-history)します。 ビルド番号 (を参照してください`ver`コマンド) 17763.292 以上にする必要があります。

   7. 次の PowerShell コマンドを使用して、記憶域メンテナンス モードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   8. 次の PowerShell コマンドを使用して、サーバーを再開します。

       ```PowerShell
       Resume-ClusterNode
       ```

   9. ストレージ修復ジョブが終了して、正常な状態に戻るにすべてのディスクを待機します。 サーバーのアップグレード中に実行されている Vm の数に応じてかなりの時間がかかります。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。

5. Windows Server 2019 にすべてのサーバーがアップグレードされた後は、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > これを行うに最大 4 週間以内が技術的には、クラスターの機能レベルをできるだけ早く更新をお勧めします。

6. クラスターの機能レベルが更新された後は、記憶域プールを更新するのに次のコマンドレットを使用します。 この時点などの新しいコマンドレット`Get-ClusterPerf`クラスター内の任意のサーバーで完全に運用可能になります。

   ```PowerShell
   Update-StoragePool
   ```

7. 必要に応じて、各 VM を停止することで VM 構成レベルをアップグレードを使用して、`Update-VMVersion`コマンドレットでは、Vm を再度開始します。

8. 使用しているソフトウェアによるネットワーク制御スイッチのセットを使用して場合、無効になっている VM のライブ マイグレーションのチェックを上記の指示に従ってコマンドレットを使用して次を VM のライブの検証チェックを再度有効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. アップグレードされたクラスターが期待どおりに機能することを確認します。 ロールはフェールオーバーが正しくと Vm の正常にライブ マイグレーションは、クラスターでは、VM のライブ マイグレーションを使用する場合。

10. クラスターの検証を実行して、クラスターの検証 (`Test-Cluster`) と、クラスター検証レポートを確認します。

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Vm が実行されているときに、OS のクリーン インストールを実行します。

このオプションには、VM のダウンタイムは発生しないが、記憶域ジョブ (ミラー修復) 各サーバーをアップグレードした後に完了するまで待機する必要があります。 個々 のサーバーは、アップグレード処理中に順番に再起動は、すべての Vm と同様に、クラスター内の残りのサーバーが実行されているままです。

1. クラスター内のすべてのサーバーに最新の更新プログラムが実行されていることを確認します。 詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)します。 マイクロソフト サポート技術情報のインストールには、少なくとも[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 年 2 月 19日)。 ビルド番号 (を参照してください`ver`コマンド) 14393.2828 以上にする必要があります。

2. を使用してソフトウェアによるネットワーク制御スイッチのセットを使用している場合は、管理者特権の PowerShell セッションを開き、クラスター上のすべての Vm で VM のライブ マイグレーションの検証チェックを無効にするには、次のコマンドを実行します。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 一度に 1 つのクラスター サーバーで、次の手順に従います。

   1. HYPER-V VM のライブ マイグレーションを使用すると、アップグレードしようとしているサーバーから Vm を実行して移動できます。

   2. 次の PowerShell コマンドを使用して、クラスターのサーバーを一時停止 — 一部の内部グループが非表示に注意してください。 注意が必要です、この手順をお勧め-既にライブをしていない場合、ためでしたをスキップ、前の手順を使用する場合に、このコマンドレットには、サーバーから Vm を移行します。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 次の PowerShell コマンドを実行して、記憶域メンテナンス モードでサーバーを配置します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 確認する次のコマンドレットを実行する、 **OperationalStatus**値は**メンテナンス モードで**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  次の PowerShell コマンドを実行してクラスターからサーバーを削除します。  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. サーバーで Windows Server 2019 のクリーン インストールを実行します。 実行形式は、システム ドライブ**setup.exe** "無"を使用してオプション。 サーバー id、役割、機能、およびセットアップの完了後にアプリケーションおよびサーバーが再起動を構成する必要があります。

   5. サーバーに Hyper-v の役割とフェールオーバー クラスタ リング機能をインストールする (使用することができます、`Install-WindowsFeature`コマンドレット)。

   6. 記憶域やネットワークの最新のドライバーのハードウェア記憶域スペース ダイレクトで使用するため、サーバーの製造元によって承認されているをインストールします。

   7. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。 詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2019](https://support.microsoft.com/help/4464619/windows-10-update-history)します。 ビルド番号 (を参照してください`ver`コマンド) 17763.292 以上にする必要があります。

   8. 次の PowerShell コマンドを使用してサーバーをクラスターに再度参加します。

       ```PowerShell
       Add-ClusterNode
       ```

   9. 次の PowerShell コマンドを使用して、記憶域メンテナンス モードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. ストレージ修復ジョブが終了して、正常な状態に戻るにすべてのディスクを待機します。 サーバーのアップグレード中に実行されている Vm の数に応じてかなりの時間がかかります。 実行するコマンドを次に示します。

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. クラスター内の次のサーバーをアップグレードします。

5. Windows Server 2019 にすべてのサーバーがアップグレードされた後は、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > これを行うに最大 4 週間以内が技術的には、クラスターの機能レベルをできるだけ早く更新をお勧めします。

6. クラスターの機能レベルが更新された後は、記憶域プールを更新するのに次のコマンドレットを使用します。 この時点などの新しいコマンドレット`Get-ClusterPerf`クラスター内の任意のサーバーで完全に運用可能になります。

   ```PowerShell
   Update-StoragePool
   ```

7. 各 VM を停止しを使用して VM 構成レベルを必要に応じてアップグレード、`Update-VMVersion`コマンドレットでは、Vm を再度開始します。

8. 使用しているソフトウェアによるネットワーク制御スイッチのセットを使用して場合、無効になっている VM のライブ マイグレーションのチェックを上記の指示に従ってコマンドレットを使用して次を VM のライブの検証チェックを再度有効にします。

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. アップグレードされたクラスターが期待どおりに機能することを確認します。 ロールはフェールオーバーが正しくと Vm の正常にライブ マイグレーションは、クラスターでは、VM のライブ マイグレーションを使用する場合。

10. クラスターの検証を実行して、クラスターの検証 (`Test-Cluster`) と、クラスター検証レポートを確認します。

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Vm が停止している間に、インプレース アップグレードを実行します。

このオプションは、VM のダウンタイムが生じますが、記憶域ジョブ (ミラー修復) 各サーバーをアップグレードした後に完了するまで待つ必要がないため、アップグレード中に実行する Vm を保持する場合よりも短時間がかかることができます。 個々 のサーバーは、アップグレード処理中に順番に再起動は、クラスター内の残りのサーバーが実行されている残っています。

1. クラスター内のすべてのサーバーに最新の更新プログラムが実行されていることを確認します。 詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)します。 マイクロソフト サポート技術情報のインストールには、少なくとも[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 年 2 月 19日)。 ビルド番号 (を参照してください`ver`コマンド) 14393.2828 以上にする必要があります。

2. クラスターで実行されている Vm を停止します。

3. 一度に 1 つのクラスター サーバーで、次の手順に従います。

   1. 次の PowerShell コマンドを使用して、クラスターのサーバーを一時停止 — 一部の内部グループが非表示に注意してください。 注意が必要です、この手順をお勧めします。

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. 次の PowerShell コマンドを実行して、記憶域メンテナンス モードでサーバーを配置します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. 確認する次のコマンドレットを実行する、 **OperationalStatus**値は**メンテナンス モードで**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. 実行して、サーバーで Windows Server 2019 のアップグレードのインストールを実行**setup.exe** 「個人ファイルとアプリを保持」オプションを使用します。  
   インストールが完了した後、クラスターとクラスターで、サーバーはサービスの開始に自動的にします。

   5.  新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。  
   詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2019](https://support.microsoft.com/help/4464619/windows-10-update-history)します。
   ビルド番号 (を参照してください`ver`コマンド) 17763.292 以上にする必要があります。

   6.  次の PowerShell コマンドを使用して、記憶域メンテナンス モードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   7.  次の PowerShell コマンドを使用して、サーバーを再開します。

       ```PowerShell
       Resume-ClusterNode
       ```

   8.  ストレージ修復ジョブが終了して、正常な状態に戻るにすべてのディスクを待機します。  
   Vm が実行されていないために、比較的高速で、この必要があります。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。
5. Windows Server 2019 にすべてのサーバーがアップグレードされた後は、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   これを行うに最大 4 週間以内が技術的には、クラスターの機能レベルをできるだけ早く更新をお勧めします。

6. クラスターの機能レベルが更新された後は、記憶域プールを更新するのに次のコマンドレットを使用します。  
   この時点などの新しいコマンドレット`Get-ClusterPerf`クラスター内の任意のサーバーで完全に運用可能になります。

   ```PowerShell
   Update-StoragePool
   ```

7. クラスターに Vm を起動し、正しく機能しているかを確認します。

8. 各 VM を停止しを使用して VM 構成レベルを必要に応じてアップグレード、`Update-VMVersion`コマンドレットでは、Vm を再度開始します。

9. アップグレードされたクラスターが期待どおりに機能することを確認します。  
   ロールはフェールオーバーが正しくと Vm の正常にライブ マイグレーションは、クラスターでは、VM のライブ マイグレーションを使用する場合。

10. クラスターの検証を実行して、クラスターの検証 (`Test-Cluster`) と、クラスター検証レポートを確認します。

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Vm が停止したときに、OS のクリーン インストールを実行します。

このオプションは、VM のダウンタイムが生じますが、記憶域ジョブ (ミラー修復) 各サーバーをアップグレードした後に完了するまで待つ必要がないため、アップグレード中に実行する Vm を保持する場合よりも短時間がかかることができます。 個々 のサーバーは、アップグレード処理中に順番に再起動は、クラスター内の残りのサーバーが実行されている残っています。

1. クラスター内のすべてのサーバーに最新の更新プログラムが実行されていることを確認します。  
   詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)します。
   マイクロソフト サポート技術情報のインストールには、少なくとも[記事 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 年 2 月 19日)。 ビルド番号 (を参照してください`ver`コマンド) 14393.2828 以上にする必要があります。

2. クラスターで実行されている Vm を停止します。

3. 一度に 1 つのクラスター サーバーで、次の手順に従います。

   2. 次の PowerShell コマンドを使用して、クラスターのサーバーを一時停止 — 一部の内部グループが非表示に注意してください。  
      注意が必要です、この手順をお勧めします。

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. 次の PowerShell コマンドを実行して、記憶域メンテナンス モードでサーバーを配置します。

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. 確認する次のコマンドレットを実行する、 **OperationalStatus**値は**メンテナンス モードで**:

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. 次の PowerShell コマンドを実行してクラスターからサーバーを削除します。  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. サーバーで Windows Server 2019 のクリーン インストールを実行します。 実行形式は、システム ドライブ**setup.exe** "無"を使用してオプション。  
      サーバー id、役割、機能、およびセットアップの完了後にアプリケーションおよびサーバーが再起動を構成する必要があります。

   7. サーバーに Hyper-v の役割とフェールオーバー クラスタ リング機能をインストールする (使用することができます、`Install-WindowsFeature`コマンドレット)。

   8. 記憶域やネットワークの最新のドライバーのハードウェア記憶域スペース ダイレクトで使用するため、サーバーの製造元によって承認されているをインストールします。

   9. 新しくアップグレードされたサーバーに最新の Windows Server 2019 更新プログラムがあることを確認します。  
      詳細については、次を参照してください。[更新履歴の Windows 10 および Windows Server 2019](https://support.microsoft.com/help/4464619/windows-10-update-history)します。
      ビルド番号 (を参照してください`ver`コマンド) 17763.292 以上にする必要があります。

   10. 次の PowerShell コマンドを使用してサーバーをクラスターに再度参加します。

      ```PowerShell
      Add-ClusterNode
      ```

   11. 次の PowerShell コマンドを使用して、記憶域メンテナンス モードからサーバーを削除します。

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. ストレージ修復ジョブが終了して、正常な状態に戻るにすべてのディスクを待機します。  
       サーバーのアップグレード中に実行されている Vm の数に応じてかなりの時間がかかります。 実行するコマンドを次に示します。

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. クラスター内の次のサーバーをアップグレードします。

5. Windows Server 2019 にすべてのサーバーがアップグレードされた後は、次の PowerShell コマンドレットを使用して、クラスターの機能レベルを更新します。
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   これを行うに最大 4 週間以内が技術的には、クラスターの機能レベルをできるだけ早く更新をお勧めします。

6. クラスターの機能レベルが更新された後は、記憶域プールを更新するのに次のコマンドレットを使用します。  
   この時点などの新しいコマンドレット`Get-ClusterPerf`クラスター内の任意のサーバーで完全に運用可能になります。

   ```PowerShell
   Update-StoragePool
   ```

7. クラスターに Vm を起動し、正しく機能しているかを確認します。

8. 各 VM を停止しを使用して VM 構成レベルを必要に応じてアップグレード、`Update-VMVersion`コマンドレットでは、Vm を再度開始します。

9. アップグレードされたクラスターが期待どおりに機能することを確認します。  
   ロールはフェールオーバーが正しくと Vm の正常にライブ マイグレーションは、クラスターでは、VM のライブ マイグレーションを使用する場合。

10. クラスターの検証を実行して、クラスターの検証 (`Test-Cluster`) と、クラスター検証レポートを確認します。
