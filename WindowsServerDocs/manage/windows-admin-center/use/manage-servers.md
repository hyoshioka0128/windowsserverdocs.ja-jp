---
title: Windows 管理センターを使用してサーバーを管理する
description: Windows 管理センターを使用したサーバーの管理 (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c7f436ea9b2baa00294ccef52a5d7a27c7247e4a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406785"
---
# <a name="manage-servers-with-windows-admin-center"></a>Windows 管理センターを使用してサーバーを管理する

>適用先:Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="managing-windows-server-machines"></a>Windows Server コンピューターの管理

Windows Server 2012 以降を実行している個々のサーバーを Windows 管理センターに追加して、証明書、デバイス、イベント、プロセス、役割と機能、更新プログラム、Virtual Machines などの包括的なツールセットを使用してサーバーを管理できます。

![サーバー接続の概要画面](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Windows 管理センターへのサーバーの追加

Windows 管理センターにサーバーを追加するには:

1. すべての接続 の下にある  **+ 追加** をクリックします。
2. **サーバー接続**を追加することを選択します。
3. サーバーの名前を入力し、メッセージが表示されたら、使用する資格情報を入力します。
4. **[送信]** をクリックして完了します。

サーバーが [概要] ページの接続リストに追加されます。 サーバーに接続するには、これをクリックします。

> [!NOTE]
> Windows 管理センターでは、[フェールオーバークラスター](manage-failover-clusters.md)または[ハイパー集約クラスター](manage-hyper-converged.md)を個別の接続として追加することもできます。

## <a name="tools"></a>ツール

サーバー接続では、次のツールを使用できます。

| ツール | 説明 |
| ---- | ----------- |
| [概要](#overview) | サーバーの詳細を表示し、サーバーの状態を制御する |
| [Active Directory](#active-directory-preview) | Active Directory の管理 |
| [Backup](#backup) | Azure Backup の表示と構成 |  
| [証明書](#certificates) | 証明書の表示と変更 |
| [コンテナー](#containers) | コンテナーの表示 |
| [デバイス](#devices) | デバイスの表示と変更 |
| [[DHCP]](#dhcp) | DHCP サーバー構成の表示と管理 |
| [DNS](#dns) | DNS サーバー構成の表示と管理 |
| [イベント](#events) | イベントの表示 |
| [ファイル](#files) | ファイルとフォルダーの参照 |
| [Firewall](#firewall) | ファイアウォール規則の表示と変更 |
| [インストール済みアプリ](#installed-apps) | インストールされているアプリを表示および削除する |
| [ローカルユーザーとグループ](#local-users-and-groups) | ローカルユーザーとグループを表示および変更する |
| [Network](#network) | ネットワークデバイスの表示と変更 |
| [PowerShell](#powershell) | PowerShell を使用したサーバーとの対話 |
| [プロセス](#processes) | 実行中のプロセスの表示と変更 |
| [登録](#registry) | レジストリエントリの表示と変更 |
| [リモートデスクトップ](#remote-desktop) | リモートデスクトップを使用したサーバーとの対話 |
| [役割と機能](#roles-and-features) | 役割と機能を表示および変更する |
| [スケジュールされたタスク](#scheduled-tasks) | スケジュールされたタスクの表示と変更 |
| [Services](#services) | サービスの表示と変更 |
| [[設定]](#settings) | サービスの表示と変更 |
| [ストレージ](#storage) | 記憶装置の表示と変更 |
| [記憶域移行サービス](#storage-migration-service) | サーバーとファイル共有を Azure または Windows Server 2019 に移行する |
| [記憶域レプリカ](#storage-replica) | 記憶域レプリカを使用してサーバー間の記憶域レプリケーションを管理する |
| [システム インサイト](#system-insights) | System Insights を使用すると、サーバーの機能についての洞察を高めることができます。 |
| [版](#updates) | インストールされていることを確認し、新しい更新プログラムを確認します |
| [仮想マシン](manage-virtual-machines.md) | バーチャルマシンの表示と管理 |
| [仮想スイッチ](#virtual-switches) | 仮想スイッチの表示と管理 |

## <a name="overview"></a>概要

**概要**を使用すると、CPU、メモリ、およびネットワークパフォーマンスの現在の状態を確認できるだけでなく、操作を実行したり、対象のコンピューターまたはサーバーの設定を変更したりできます。

### <a name="features"></a>機能

サーバーマネージャーの概要では、次の機能がサポートされています。

- サーバーの詳細の表示
- CPU の利用状況の表示
- メモリアクティビティの表示
- ネットワークアクティビティの表示
- サーバーの再起動
- サーバーのシャットダウン
- サーバーのディスクメトリックを有効にする
- サーバーのコンピューター ID の編集
- BMC IP アドレスをハイパーリンク付きで表示します (IPMI 互換の BMC が必要です)。

[**サーバーの概要に関するフィードバックと提案された機能をご確認**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D)ください。

## <a name="active-directory-preview"></a>Active Directory (プレビュー)

**Active Directory**は、[拡張機能フィード](../configure/using-extensions.md)で使用できる早期プレビューです。

### <a name="features"></a>機能

次の Active Directory 管理を使用できます。

- ユーザーの作成
- グループの作成
- ユーザー、コンピューター、およびグループを検索する
- グリッドで選択した場合のユーザー、コンピューター、およびグループの詳細ウィンドウ
- グローバルグリッドアクションのユーザー、コンピューター、およびグループ (無効化/有効化、削除)
- ユーザー パスワードのリセット
- ユーザーオブジェクト: グループメンバーシップ & 基本プロパティを構成する
- コンピューターオブジェクト: 1 台のコンピューターへの委任を構成する
- グループオブジェクト: メンバーシップを管理する (一度に1ユーザーを追加/削除する)  

[**Active Directory のフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D)します。

## <a name="backup"></a>バックアップ

**バックアップ**を使用すると、サーバーを Microsoft Azure に直接バックアップして、Windows server を破損、攻撃、災害から保護することができます。
[詳細については、Azure Backup を参照してください。](https://aka.ms/windows-admin-center-backup)

[Windows 管理センターでバックアップに関するフィードバックを提供する](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>機能

バックアップでは、次の機能がサポートされています。

- Azure backup の状態の概要を表示する
- バックアップ項目とスケジュールの構成
- バックアップジョブの開始または停止
- バックアップジョブの履歴と状態の表示
- 回復ポイントの表示とデータの回復
- バックアップデータの削除

## <a name="certificates"></a>証明書

証明**書**を使用すると、コンピューターまたはサーバー上の証明書ストアを管理できます。

### <a name="features"></a>機能

証明書では、次の機能がサポートされています。

- 既存の証明書を参照して検索する
- 証明書の詳細の表示
- 証明書のエクスポート
- 証明書の更新
- 新しい証明書を要求する
- 証明書の削除

[**証明書のフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D)します。

## <a name="containers"></a>コンテナー

**コンテナーを使用する**と、Windows Server コンテナーホスト上のコンテナーを表示できます。 Windows Server Core コンテナーが実行されている場合は、イベントログを表示し、コンテナーの CLI にアクセスできます。

[**コンテナーのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)します。

## <a name="devices"></a>デバイス

**デバイス**では、コンピューターまたはサーバー上の接続されているデバイスを管理できます。

### <a name="features"></a>機能

デバイスでは、次の機能がサポートされています。

- デバイスの参照と検索
- デバイスの詳細の表示
- デバイスを無効にする
- デバイスのドライバーを更新する

[**デバイスのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)します。

## <a name="dhcp"></a>DHCP

**DHCP**を使用すると、コンピューターまたはサーバー上の接続されているデバイスを管理できます。

### <a name="features"></a>機能

- IPV4 と IPV6 のスコープを作成/構成/表示する
- アドレスの除外を作成し、開始 IP アドレスと終了 IP アドレスを構成する
- アドレス予約を作成し、クライアントの MAC アドレス (IPV4)、DUID、および IAID (IPV6) を構成する

[**DHCP のフィードバックと提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D)された機能を表示します。

## <a name="dns"></a>DNS

**DNS**を使用すると、コンピューターまたはサーバー上の接続されているデバイスを管理できます。

### <a name="features"></a>機能

- DNS 前方参照ゾーン、逆引き参照ゾーン、および DNS レコードの詳細を表示する
- 前方参照ゾーン (プライマリ、セカンダリ、またはスタブ) を作成し、前方参照ゾーンのプロパティを構成する
- ホスト (A または AAAA)、CNAME または MX の種類の DNS レコードを作成する
- DNS レコードの構成のプロパティ
- IPV4 および IPV6 の逆引き参照ゾーン (プライマリ、セカンダリ、スタブ) を作成し、逆引き参照ゾーンのプロパティを構成する
- 逆引き参照ゾーンに DNS レコードの PTR、CNAME 型を作成します。

[**DHCP のフィードバックと提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D)された機能を表示します。

## <a name="events"></a>イベント

**イベント**を使用すると、コンピューターまたはサーバー上のイベントログを管理できます。

### <a name="features"></a>機能

イベントでは、次の機能がサポートされています。

- イベントの参照と検索
- イベントの詳細の表示
- ログからイベントを消去します
- ログからイベントをエクスポートする

[**フィードバックとイベントの提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D)します。

## <a name="files"></a>ファイル

**ファイル**を使用すると、コンピューターまたはサーバー上のファイルとフォルダーを管理できます。

### <a name="features"></a>機能

ファイルでは、次の機能がサポートされています。

- ファイルとフォルダーの参照
- ファイルまたはフォルダーの検索
- 新しいフォルダーの作成
- ファイルまたはフォルダーを削除する
- ファイルまたはフォルダーをダウンロードする
- ファイルまたはフォルダーをアップロードする
- ファイルまたはフォルダーの名前を変更する
- Zip ファイルを抽出する
- ファイルまたはフォルダーのプロパティの表示
- ファイル共有の追加、編集、または削除
- ファイル共有のユーザーとグループのアクセス許可を変更する

[**ファイルのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)します。

## <a name="firewall"></a>ファイアウォール

**ファイアウォール**では、コンピューターまたはサーバーのファイアウォール設定と規則を管理できます。

### <a name="features"></a>機能

ファイアウォールでは、次の機能がサポートされています。

- ファイアウォール設定の概要を表示する
- 受信ファイアウォール規則の表示
- 送信ファイアウォール規則の表示
- ファイアウォール規則の検索
- ファイアウォール規則の詳細の表示
- 新しいファイアウォール規則を作成する
- ファイアウォール規則を有効または無効にする
- ファイアウォール規則の削除
- ファイアウォール規則のプロパティを編集する

[**フィードバックと、ファイアウォールの提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D)します。

## <a name="installed-apps"></a>インストール済みアプリ

**インストール**されているアプリを使用して、インストールされているアプリケーションを一覧表示およびアンインストールできます。

[**インストールされているアプリのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D)します。

## <a name="local-users-and-groups"></a>ローカル ユーザーとグループ

**ローカルユーザーとグループ**を使用すると、コンピューターまたはサーバーのローカルに存在するセキュリティグループとユーザーを管理できます。

### <a name="features"></a>機能

ローカルユーザーとグループでは、次の機能がサポートされています。

- ユーザーとグループの表示と検索
- 新しいユーザーまたはグループを作成する
- ユーザーのグループメンバーシップを管理する
- ユーザーまたはグループを削除する
- ユーザーのパスワードを変更する
- ユーザーまたはグループのプロパティを編集する

[**ローカルユーザーとグループのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>ネットワーク

**ネットワーク**では、コンピューターまたはサーバー上のネットワークデバイスと設定を管理できます。

### <a name="features"></a>機能

ネットワークでは、次の機能がサポートされています。

- 既存のネットワークアダプターの参照と検索
- ネットワークアダプターの詳細を表示する
- ネットワークアダプターのプロパティの編集
- [Azure ネットワークアダプターを作成する (プレビュー機能)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**ネットワークのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**Powershell**を使用すると、powershell セッションを使用してコンピューターまたはサーバーと対話できます。

### <a name="features"></a>機能

PowerShell では、次の機能がサポートされています。

- サーバーで対話型の PowerShell セッションを作成する
- サーバー上の PowerShell セッションから切断する

[**PowerShell のフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>Processes (プロセス)

**プロセス**を使用すると、コンピューターまたはサーバー上で実行中のプロセスを管理できます。

### <a name="features"></a>機能

プロセスでは、次の機能がサポートされています。

- 実行中のプロセスを参照して検索する
- プロセスの詳細の表示
- プロセスを開始する
- プロセスを終了する
- プロセスダンプの作成
- プロセスハンドルの検索

[**フィードバックとプロセスの提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D)します。

## <a name="registry"></a>レジストリ

**レジストリ**を使用して、コンピューターまたはサーバー上のレジストリキーと値を管理できます。

### <a name="features"></a>機能

レジストリでは、次の機能がサポートされています。

- レジストリキーと値の参照
- レジストリ値を追加または変更する
- レジストリ値の削除

[**フィードバックと、レジストリの提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)します。

## <a name="remote-desktop"></a>リモート デスクトップ

**リモートデスクトップ**を使用すると、対話型デスクトップセッションを使用してコンピューターまたはサーバーと対話できます。

### <a name="features"></a>機能

リモートデスクトップでは、次の機能がサポートされています。

- 対話型のリモートデスクトップセッションを開始する
- リモートデスクトップセッションからの切断
- Ctrl + Alt + Del をリモートデスクトップセッションに送信する

[**リモートデスクトップのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D)します。

## <a name="roles-and-features"></a>役割と機能

**役割と機能**を使用すると、サーバー上の役割と機能を管理できます。

### <a name="features"></a>機能

役割と機能では、次の機能がサポートされています。

- サーバー上の役割と機能の一覧を参照する
- 役割または機能の詳細の表示
- 役割または機能をインストールする
- 役割または機能を削除する

[**役割と機能に関するフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D)します。

## <a name="scheduled-tasks"></a>スケジュールされたタスク

**スケジュール**されたタスクを使用して、コンピューターまたはサーバー上のスケジュールされたタスクを管理できます。

### <a name="features"></a>機能

スケジュールされたタスクでは、次の機能がサポートされています。

- タスクスケジューラライブラリの参照
- スケジュールされたタスクの編集
- スケジュールされたタスクを有効 & 無効にする
- スケジュールされたタスクの開始 & 停止
- スケジュールされたタスクの作成

スケジュールされた[**タスクのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D)します。

## <a name="services"></a>Services

**サービス**を使用すると、コンピューターまたはサーバー上のサービスを管理できます。

### <a name="features"></a>機能

サービスでは、次の機能がサポートされています。

- サーバー上のサービスを参照および検索する
- サービスの詳細を表示する
- サービスを開始する
- サービスを一時停止する
- サービスのプロパティを編集する

[**サービスのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D)します。

## <a name="settings"></a>設定

**設定**は、コンピューターまたはサーバーの設定を管理するための一元的な場所です。

### <a name="features"></a>機能

- ユーザーとシステムの環境変数を表示および変更する
- アラートを監視するための構成を表示[Azure Monitor](azure-monitor.md)
- 電源構成の表示と変更
- リモートデスクトップの設定を表示および変更する
- ロールベースのアクセス制御設定を表示および変更する
- Hyper-v ホストの設定を表示および変更する (該当する場合)

## <a name="storage"></a>ストレージ

**記憶域**を使用すると、コンピューターまたはサーバー上の記憶装置を管理できます。

### <a name="features"></a>機能

ストレージでは、次の機能がサポートされています。

- サーバー上の既存のディスクを参照して検索する
- ディスクの詳細の表示
- ボリュームを作成する
- ディスクの初期化
- バーチャルハードディスク (VHD) の作成、アタッチ、および切断
- ディスクをオフラインにする
- ボリュームのフォーマット
- ボリュームのサイズを変更する
- ボリュームのプロパティの編集
- ボリュームの削除
- クォータ管理のインストール
- ファイルサーバーリソースマネージャーのクォータ[の記憶域の管理-> のクォータの作成と更新](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)

[**ストレージのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>ストレージ移行サービス

**Storage Migration Service**を使用すると、アプリケーションやユーザーによる変更を必要とせずに、サーバーとファイル共有を Azure または Windows Server 2019 に移行することができます。
[Storage Migration Service の概要を見る](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>Storage Migration Service には Windows Server 2019 が必要です。

## <a name="storage-replica"></a>記憶域レプリカ

**記憶域レプリカ**を使用して、サーバー間の記憶域レプリケーションを管理します。
[記憶域レプリカの詳細情報](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## <a name="system-insights"></a>システム インサイト

**System Insights**では、予測分析が Windows server にネイティブで導入され、サーバーの機能に関する洞察が向上しています。
[System Insights の概要を見る](http://aka.ms/systeminsights)

>[!NOTE]
>System Insights には Windows Server 2019 が必要です。

## <a name="updates"></a>更新プログラム

**更新プログラム**を使用すると、コンピューターまたはサーバーで Microsoft や Windows の更新プログラムを管理できます。

### <a name="features"></a>機能

更新プログラムでは、次の機能がサポートされています。

- 使用可能な Windows または Microsoft 更新プログラムの表示
- 更新履歴の一覧を表示する
- 更新のインストール
- オンラインで Microsoft Update からの更新プログラムを確認する
- [Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)統合の管理

[**更新プログラムのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>仮想マシン

「 [Windows 管理センターでの Virtual Machines の管理」を](manage-virtual-machines.md)参照してください。

## <a name="virtual-switches"></a>仮想スイッチ

**仮想スイッチ**を使用すると、コンピューターまたはサーバー上の hyper-v 仮想スイッチを管理できます。

### <a name="features"></a>機能

仮想スイッチでは、次の機能がサポートされています。

- サーバー上の仮想スイッチを参照および検索する
- 新しい仮想スイッチを作成する
- 仮想スイッチの名前を変更する
- 既存の仮想スイッチを削除する
- 仮想スイッチのプロパティを編集する

[**仮想スイッチのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
