---
title: Windows Admin Center でサーバーを管理します。
description: Windows Admin Center (プロジェクト ホノルル) でサーバーを管理します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 04ade4a14272c7840b5036ca6ad5a3bf3d09bcf9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891153"
---
# <a name="manage-servers-with-windows-admin-center"></a>Windows Admin Center でサーバーを管理します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="managing-windows-server-machines"></a>Windows Server マシンの管理

Windows Server 2012 を実行しているか、後で包括的な一連のツールでサーバーを管理する Windows Admin Center を含む証明書、デバイス、イベント、プロセス、役割と機能、更新プログラム、仮想マシンなどの個々 のサーバーを追加することができます。

![サーバー接続の概要画面](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Windows Admin Center へのサーバーの追加

Windows Admin Center にサーバーを追加するには

1. クリックして **+ 追加**すべての接続。
2. 追加することも、**サーバー接続**します。
3. サーバーの名前を入力し、使用する資格情報を求められた場合。
4. クリックして**送信**を完了します。

サーバーは、[概要] ページの接続一覧に追加されます。 サーバーに接続するようにクリックします。

> [!NOTE]
> 追加することも[フェイル オーバー クラスター](manage-failover-clusters.md)または[ハイパー コンバージド クラスター](manage-hyper-converged.md) Windows Admin Center での個別の接続として。

## <a name="tools"></a>ツール

次のツールは、サーバー接続の場合に。

| ツール | 説明 |
| ---- | ----------- |
| [概要](#overview) | サーバーの詳細を表示し、サーバーの状態の制御 |
| [バックアップ](#backup) | 表示および Azure Backup の構成 |  
| [証明書](#certificates) | 表示および証明書の変更 |
| [コンテナー](#containers) | コンテナー表示 |
| [デバイス](#devices) | 表示およびデバイスの変更 |
| [イベント](#events) | イベントの表示 |
| [ファイル](#files) | ファイルやフォルダーを参照します。 |
| [ファイアウォール](#firewall) | 表示し、ファイアウォール規則を変更します。 |
| [インストールされているアプリ](#installed-apps) | 表示およびインストールされているアプリの削除 |
| [ローカル ユーザーとグループ](#local-users-and-groups) | ローカル ユーザーとグループ表示および変更 |
| [Network](#network) | 表示およびネットワーク デバイスの変更 |
| [PowerShell](#powershell) | PowerShell を使用するサーバーとの対話します。 |
| [プロセス](#processes) | 表示および変更プロセスを実行します。 |
| [レジストリ](#registry) | 表示およびレジストリ エントリの変更 |
| [リモート デスクトップ](#remote-desktop) | リモート デスクトップ経由でサーバーとの対話します。 |
| [役割と機能](#roles-and-features) | 役割と機能表示および変更 |
| [スケジュールされたタスク](#scheduled-tasks) | 表示および変更のスケジュールされたタスク |
| [Services](#services) | 表示およびサービスの変更 |
| [ストレージ](#storage) | 表示および記憶域デバイスの変更 |
| [記憶域の移行サービス](#storage-migration-service) | サーバーやファイル共有を Azure または Windows Server 2019 に移行します。 |
| [記憶域レプリカ](#storage-replica) | 記憶域レプリカを使用して、サーバー間の記憶域レプリケーションを管理するには |
| [システム Insights](#system-insights) | システム Insights により、サーバーの機能に関する洞察が増加します。 |
| [更新プログラム](#updates) | インストールされているビューと新しい更新プログラムの確認 |
| [仮想マシン](manage-virtual-machines.md) | 表示し、仮想マシンの管理 |
| [仮想スイッチ](#virtual-switches) | 表示し、仮想スイッチの管理 |

## <a name="overview"></a>概要

**概要**CPU、メモリ、およびネットワークのパフォーマンスの現在の状態を確認することができますもとして操作を実行し、対象のコンピューターまたはサーバーの設定を変更します。

### <a name="features"></a>機能

サーバー マネージャーの概要では、次の機能がサポートされています。

- サーバーの詳細の表示
- CPU の利用状況
- メモリの利用状況の表示
- ネットワーク アクティビティの表示
- サーバーを再起動します。
- サーバーのシャット ダウン
- サーバー上のディスクのメトリックを有効にします。
- サーバー上のコンピューターの ID を編集します。

[**フィードバックと提案された機能をサーバーの概要の表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D)します。

## <a name="backup"></a>バックアップ

**バックアップ**Windows サーバーを Microsoft Azure に直接サーバーのバックアップの破損、攻撃や災害から保護することができます。
[Azure Backup について説明します。](https://aka.ms/windows-admin-center-backup)

[Windows Admin Center でのバックアップのフィードバックを提供します。](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>機能

バックアップでは、次の機能がサポートされています。

- Azure のバックアップの状態の概要を表示します。
- バックアップ項目とスケジュールを構成します。
- 開始またはバックアップ ジョブの停止
- バックアップ ジョブの履歴と状態を表示します。
- 回復ポイントを表示し、データの回復
- バックアップ データを削除します。

## <a name="certificates"></a>証明書

**証明書**コンピューターまたはサーバーの証明書ストアを管理することができます。

### <a name="features"></a>機能

証明書では、次の機能がサポートされています。

- 参照および既存の証明書を検索
- 証明書の詳細の表示
- 証明書をエクスポートします。
- 証明書を更新します。
- 新しい証明書を要求
- 証明書を削除します。

[**証明書のフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D)します。

## <a name="containers"></a>コンテナー

**コンテナー** Windows Server コンテナー ホストでコンテナーを表示することができます。 実行中の Windows Server Core コンテナーの場合は、イベント ログを表示し、コンテナーの CLI にアクセスできます。

[**コンテナーのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)します。

## <a name="devices"></a>デバイス

**デバイス**コンピューターまたはサーバーに接続されているデバイスを管理することができます。

### <a name="features"></a>機能

デバイスでは、次の機能がサポートされています。

- 参照と検索のデバイス
- デバイスの詳細の表示
- デバイスを無効にします。
- デバイス ドライバーの更新

[**デバイスのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)します。

## <a name="events"></a>イベント

**イベント**コンピューターまたはサーバー上のイベント ログを管理することができます。

### <a name="features"></a>機能

イベントでは、次の機能がサポートされています。

- 参照と検索のイベント
- イベントの詳細の表示
- ログからイベントを消去
- ログからイベントをエクスポートします。

[**イベントのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D)します。

## <a name="files"></a>ファイル

**ファイル**コンピューターまたはサーバーのファイルとフォルダーを管理することができます。

### <a name="features"></a>機能

ファイルでは、次の機能がサポートされています。

- ファイルやフォルダーを参照します。
- ファイルまたはフォルダーを検索します。
- 新しいフォルダーを作成します。
- ファイルまたはフォルダーを削除します。
- ファイルまたはフォルダーをダウンロードします。
- ファイルまたはフォルダーをアップロードします。
- ファイルまたはフォルダーの名前を変更します。
- Zip ファイルを抽出します。
- ファイルまたはフォルダーのプロパティの表示
- ファイル サーバー リソース マネージャーの管理[クォータ](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)
- 追加、編集、またはファイル共有を削除します。
- ユーザーとグループのアクセス許可をファイル共有を変更します。

[**ファイルのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)します。

## <a name="firewall"></a>ファイアウォール

**ファイアウォール**ファイアウォールの設定およびコンピューターまたはサーバー上のルールを管理することができます。

### <a name="features"></a>機能

ファイアウォールでは、次の機能がサポートされています。

- ファイアウォールの設定の概要を表示します。
- 受信のファイアウォール規則を表示します。
- 送信ファイアウォール規則を表示します。
- ファイアウォール規則の検索
- ファイアウォール ルールの詳細を表示
- 新しいファイアウォール ルールを作成します。
- 有効にするか、ファイアウォール規則を無効にします。
- ファイアウォール規則の削除
- ファイアウォール規則のプロパティを編集します。

[**ファイアウォールのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D)します。

## <a name="installed-apps"></a>インストールされているアプリ

**アプリがインストールされている**を一覧表示し、インストールされているアプリケーションをアンインストールすることができます。

[**フィードバックと提案された機能をインストール済みアプリの表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D)します。

## <a name="local-users-and-groups"></a>ローカル ユーザーとグループ

**ローカル ユーザーとグループ**セキュリティ グループとローカル コンピューターまたはサーバー上に存在するユーザーを管理することができます。

### <a name="features"></a>機能

ローカル ユーザーとグループでは、次の機能がサポートされています。

- ユーザーとグループのビューと検索
- 新しいユーザーまたはグループを作成します。
- ユーザーのグループ メンバーシップを管理します。
- ユーザーまたはグループを削除します。
- ユーザーのパスワードを変更します。
- ユーザーまたはグループのプロパティを編集します。

[**フィードバックと提案された機能をローカル ユーザーとグループを表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>ネットワーク

**ネットワーク**ネットワーク デバイスとコンピューターまたはサーバー上の設定を管理することができます。

### <a name="features"></a>機能

ネットワークでは、次の機能がサポートされています。

- 参照および既存のネットワーク アダプターを検索
- ネットワーク アダプターの詳細を表示します。
- ネットワーク アダプターのプロパティを編集します。
- 作成、 [Azure のネットワーク アダプター (プレビュー機能)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**ネットワークのフィードバックと提案された機能を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**PowerShell**コンピューターまたは PowerShell セッションを使用するサーバーと対話することができます。

### <a name="features"></a>機能

PowerShell では、次の機能がサポートされています。

- サーバーでの対話型 PowerShell セッションを作成します。
- サーバー上の PowerShell セッションから切断します。

[**PowerShell のフィードバックと提案された機能を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>Processes (プロセス)

**プロセス**コンピューターまたはサーバーで実行中のプロセスを管理することができます。

### <a name="features"></a>機能

プロセスでは、次の機能がサポートされています。

- プロセスの実行を検索および参照
- プロセスの詳細の表示
- プロセスを開始します。
- プロセスを終了します。
- プロセスのダンプを作成します。
- プロセス ハンドルを検索します。

[**プロセスのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D)します。

## <a name="registry"></a>レジストリ

**レジストリ**レジストリ キーと、コンピューターまたはサーバー上の値を管理することができます。

### <a name="features"></a>機能

レジストリでは、次の機能がサポートされています。

- レジストリ キーと値を参照します。
- 追加またはレジストリ値を変更します。
- レジストリ値を削除します

[**レジストリのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)します。

## <a name="remote-desktop"></a>リモート デスクトップ

**リモート デスクトップ**コンピューターまたは対話型デスクトップ セッション経由でサーバーと対話することができます。

### <a name="features"></a>機能

リモート デスクトップでは、次の機能がサポートされています。

- 対話型のリモート デスクトップ セッションを開始します。
- リモート デスクトップ セッションから切断します。
- Ctrl + Alt + Del をリモート デスクトップ セッションに送信します。

[**リモート デスクトップのフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D)します。

## <a name="roles-and-features"></a>役割と機能

**役割と機能の**役割と機能をサーバーに管理することができます。

### <a name="features"></a>機能

役割と機能では、次の機能がサポートされています。

- サーバーへ役割と機能の一覧を参照します。
- 役割または機能の詳細の表示
- 役割または機能をインストールします。
- 役割または機能を削除します。

[**役割と機能に関するフィードバックと提案された機能を表示する**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D)します。

## <a name="scheduled-tasks"></a>スケジュールされたタスク

**スケジュールされたタスク**コンピューターまたはサーバー上のスケジュールされたタスクを管理することができます。

### <a name="features"></a>機能

スケジュールされたタスクでは、次の機能がサポートされています。

- タスク スケジューラ ライブラリを参照します。
- スケジュールされたタスクを編集します。
- 有効にするし、スケジュールされたタスクを無効にします。
- スケジュールされたタスクの開始と停止
- スケジュールされたタスクを作成します。

[**スケジュールされたタスクのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D)します。

## <a name="services"></a>サービス

**サービス**コンピューターまたはサーバー上のサービスを管理することができます。

### <a name="features"></a>機能

サービスでは、次の機能がサポートされています。

- サーバー上の参照と検索サービス
- サービスの詳細を表示します。
- サービスを開始する
- サービスを一時停止します。
- サービスのプロパティを編集します。

[**サービスのフィードバックと提案された機能を表示**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D)します。

## <a name="storage"></a>ストレージ

**記憶域**コンピューターまたはサーバー上の記憶装置を管理することができます。

### <a name="features"></a>機能

記憶域では、次の機能がサポートされています。

- 参照し、サーバー上の既存のディスクを検索
- ディスクの詳細を表示
- ボリュームを作成する
- ディスクを初期化します。
- 作成し、アタッチ、デタッチ、仮想ハード_ディスク (VHD)
- ディスクをオフラインにします。
- ボリュームをフォーマットします。
- ボリュームのサイズを変更します。
- ボリュームのプロパティを編集します。
- ボリュームを削除します。
- クォータの管理をインストールします。

[**記憶域のフィードバックと提案された機能を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>ストレージ移行サービス

**記憶域の移行サービス**サーバーを移行して、ファイルを Azure または Windows Server 2019 に共有することができます-アプリや何も変更するユーザーは必要ありません。
[記憶域の移行サービスを概要します。](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>記憶域の移行サービスには、Windows Server 2019 が必要です。

## <a name="storage-replica"></a>記憶域レプリカ

使用**記憶域レプリカ**サーバー間の記憶域レプリケーションを管理します。
[記憶域レプリカを詳細します。](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## <a name="system-insights"></a>システム インサイト

**システム Insights**ネイティブの予測分析の紹介を提供する Windows Server、サーバーに機能している洞察の増加します。
[システムの Insights を概要します。](http://aka.ms/systeminsights)

>[!NOTE]
>Insights のシステムでは、Windows Server 2019 が必要です。

## <a name="updates"></a>更新プログラム

**更新プログラム**コンピューターまたはサーバー上の Microsoft および Windows の更新プログラムを管理することができます。

### <a name="features"></a>機能

更新プログラムでは、次の機能がサポートされています。

- Windows または Microsoft 更新プログラムが利用可能な表示します。
- 更新履歴の一覧を表示します。
- 更新のインストール
- Microsoft Update から更新プログラムをオンラインで確認します。
- 管理[Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)統合

[**更新プログラムのフィードバックと提案された機能を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>仮想マシン

参照してください[Windows Admin Center での仮想マシンの管理](manage-virtual-machines.md)

## <a name="virtual-switches"></a>仮想スイッチ

**仮想スイッチ**コンピューターまたはサーバー上の HYPER-V 仮想スイッチを管理することができます。

### <a name="features"></a>機能

仮想スイッチでは、次の機能がサポートされています。

- 参照し、サーバー上の仮想スイッチの検索
- 新しい仮想スイッチを作成します。
- 仮想スイッチの名前を変更します。
- 既存の仮想スイッチを削除します。
- 仮想スイッチのプロパティを編集します。

[**フィードバックと提案された機能を仮想スイッチを表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
