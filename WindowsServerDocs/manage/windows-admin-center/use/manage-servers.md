---
title: Windows Admin Center でサーバーを管理します。
description: Windows Admin center (Project Honolulu) サーバーを管理します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93a40345d05a6230596832b2d455d36eee2401b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296684"
---
# Windows Admin Center でサーバーを管理します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## Windows Server のマシンの管理

Windows Server 2012 を実行しているか、後で Windows Admin Center を包括的な一連のツールを使用してサーバーを管理する証明書、デバイス、イベント、プロセス、役割と機能、更新プログラム、仮想マシンなどを含む個別のサーバーを追加することができます。

![サーバー接続の概要] 画面](../media/manage-servers/server-overview.png)

## Windows Admin Center にサーバーを追加します。

Windows Admin Center のサーバーを追加します。

1. すべての接続 [ **+ 追加]** をクリックします。
2. **サーバー接続**を追加する場合に選択します。
3. サーバーの名前を入力し、使用する資格情報を要求します。
4. 終了するための**送信**] をクリックします。

サーバーは、概要ページで、接続の一覧に追加されます。 サーバーに接続する] をクリックします。

> [!NOTE]
> Windows Admin Center で別の接続と、[フェールオーバー クラスター](manage-failover-clusters.md)または[ハイパーコンバージド クラスター](manage-hyper-converged.md)を追加することもできます。

## ツール

次のツール サーバー接続を利用できます。

| ツール | 説明 |
| ---- | ----------- |
| [概要](#overview) | サーバーの詳細を表示し、サーバーの状態を制御 |
| [Active Directory](#active-directory-preview) | Active Directory を管理します。 |
| [バックアップ](#backup) | 表示および Azure Backup を構成します。 |  
| [証明書](#certificates) | 表示し、証明書の変更 |
| [コンテナー](#containers) | コンテナーの表示 |
| [デバイス](#devices) | 表示してデバイスの変更 |
| [DHCP](#dhcp) | 表示および DHCP サーバーの構成の管理 |
| [DNS](#dns) | 表示し、DNS サーバーの構成の管理 |
| [イベント](#events) | イベントの表示 |
| [ファイル](#files) | ファイルやフォルダーを参照します。 |
| [ファイアウォール](#firewall) | 表示してファイアウォール規則を変更します。 |
| [インストール済みアプリ](#installed-apps) | 表示およびインストール済みのアプリを削除します。 |
| [ローカル ユーザーとグループ](#local-users-and-groups) | 表示してローカル ユーザーとグループの変更 |
| [ネットワーク](#network) | 表示およびネットワーク デバイスの変更 |
| [PowerShell](#powershell) | PowerShell でのサーバーとの対話します。 |
| [プロセス](#processes) | 表示および変更プロセスを実行します。 |
| [レジストリ](#registry) | 表示およびレジストリ エントリの変更 |
| [リモート デスクトップ](#remote-desktop) | リモート デスクトップ経由でサーバーとの対話します。 |
| [役割と機能](#roles-and-features) | 表示して役割と機能の変更 |
| [スケジュールされたタスク](#scheduled-tasks) | 表示および変更のスケジュールされたタスク |
| [サービス](#services) | 表示し、サービスの変更 |
| [設定](#settings) | 表示し、サービスの変更 |
| [記憶域](#storage) | 表示および記憶域デバイスの変更 |
| [ストレージ移行サービス](#storage-migration-service) | Azure または Windows Server 2019 のサーバーやファイル共有を移行します。 |
| [記憶域レプリカ](#storage-replica) | 記憶域レプリカを使用してサーバー間の記憶域のレプリケーションを管理するには |
| [システム インサイト](#system-insights) | システム インサイトは、サーバーの機能に関するインサイトが増加します。 |
| [アップデート](#updates) | インストールされているビューと新しい更新プログラムのチェック |
| [仮想マシン](manage-virtual-machines.md) | 表示し、仮想マシンの管理 |
| [仮想スイッチ](#virtual-switches) | 表示し、仮想スイッチの管理 |

## 概要

**概要**では、CPU、メモリ、およびネットワークのパフォーマンスの現在の状態を参照してくださいほか、操作を実行し、対象のコンピューターまたはサーバーの設定を変更できます。

### 機能

サーバー マネージャーの概要では、次の機能がサポートされています。

- サーバーの詳細の表示
- アクティビティの CPU の表示
- メモリのアクティビティの表示
- ネットワーク アクティビティの表示
- サーバーを再起動します。
- サーバーを停止します。
- サーバー上のディスクのメトリックを有効にします。
- サーバー上のコンピューター ID を編集します。
- (IPMI と互換性のある BMC が必要) にハイパーリンクが含まれる BMC IP アドレスを表示します。

[**ビューのフィードバックとサーバーの概要の機能を提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D)します。

## Active Directory (プレビュー)

**Active Directory**では、[拡張機能フィード](../configure/using-extensions.md)に利用できる初期のプレビューです。

### 機能

次の Active Directory 管理利用できます。

- ユーザーを作成します。
- グループを作成します。
- ユーザー、コンピューター、およびグループの検索
- ユーザー、コンピューター、およびグループ グリッドで選択した場合の詳細ウィンドウ
- グローバル グリッド操作ユーザー、コンピューター、およびグループ (有効/無効を削除)
- ユーザー パスワードのリセット
- ユーザー オブジェクト: 基本的なプロパティ & グループ メンバーシップを構成します。
- コンピューター オブジェクト: 1 台のコンピューターに委任の構成
- グループ オブジェクトの: (1 の追加/削除ユーザーが同時に) のメンバーシップの管理  

[**ビューのフィードバックと Active Directory の提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D)します。

## バックアップ

**バックアップ**では、Microsoft Azure に直接、サーバーをバックアップすることによって、破損、攻撃や障害から、Windows server を保護することができます。
[Azure Backup について説明します。](https://aka.ms/windows-admin-center-backup)

[Windows Admin Center でのバックアップのフィードバックを提供します。](https://aka.ms/backup-wac-feedback)

### 機能

バックアップでは、次の機能がサポートされています。

- Azure バックアップ状態の概要を表示します。
- バックアップ アイテムとスケジュールを構成します。
- 開始または停止するバックアップ ジョブ
- バックアップ ジョブの履歴の表示と状態
- 回復ポイントを表示し、データを復元します。
- バックアップ データを削除します。

## 証明書

**証明書**では、コンピューターまたはサーバー上の証明書ストアを管理することができます。

### 機能

証明書では、次の機能がサポートされています。

- 参照し、既存の証明書を検索
- 証明書の詳細の表示
- 証明書をエクスポートします。
- 証明書を更新します。
- 新しい証明書を要求します。
- 証明書を削除します。

[**ビューのフィードバックと証明書の提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D)します。

## コンテナー

**コンテナー**では、Windows Server コンテナー ホストでコンテナーを表示することができます。 実行中の Windows Server Core コンテナーの場合は、イベント ログを表示し、コンテナーの CLI にアクセスできます。

[**ビューのフィードバックとコンテナーの機能を提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)します。

## デバイス

**デバイス**では、コンピューターまたはサーバーに接続されているデバイスを管理することができます。

### 機能

デバイスでは、次の機能がサポートされています。

- デバイスの参照と検索
- デバイスの詳細の表示
- デバイスを無効にします。
- デバイスのドライバーの更新

[**ビューのフィードバックとデバイスの機能の提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)します。

## DHCP

**DHCP**では、コンピューターまたはサーバーに接続されているデバイスを管理することができます。

### 機能

- 作成/構成/ビュー IPV4 と IPV6 のスコープ
- アドレスの除外を作成し、開始と終了の IP アドレスを構成します。
- アドレスの予約を作成し、クライアント MAC アドレス (IPV4) DUID と IAID (IPV6) の構成

[**ビューのフィードバックおよび DHCP の提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D)します。

## DNS

**DNS**には、コンピューターまたはサーバーに接続されているデバイスを管理することができます。

### 機能

- DNS 前方参照ゾーン、逆引き参照ゾーンおよび DNS レコードの詳細を表示します。
- 前方参照ゾーンを作成 (プライマリ、セカンダリ、またはスタブ)、および前方参照ゾーンのプロパティの構成
- ホストを作成します (A または AAAA) CNAME または MX 種類の DNS レコード
- DNS レコードのプロパティを構成します。
- IPV4 と IPV6 の逆引き参照ゾーンを作成する (プライマリ、セカンダリとスタブ)、逆引き参照ゾーンのプロパティを構成します。
- 作成 PTR、DNS の CNAME 型が逆引き参照ゾーンの下に記録します。

[**ビューのフィードバックおよび DHCP の提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D)します。

## イベント

**イベント**では、コンピューターまたはサーバー上のイベント ログを管理することができます。

### 機能

イベントでは、次の機能がサポートされています。

- ブラウズおよび検索イベント
- イベントの詳細の表示
- ログからイベントを消去
- ログからイベントをエクスポートします。

[**ビューのフィードバックとイベントの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D)します。

## ファイル

**ファイル**には、コンピューターまたはサーバーでファイルとフォルダーを管理することができます。

### 機能

ファイルには、次の機能がサポートされています。

- ファイルやフォルダーを参照します。
- ファイルまたはフォルダーを検索します。
- 新しいフォルダーを作成します。
- ファイルまたはフォルダーを削除します。
- ファイルまたはフォルダーをダウンロードします。
- ファイルまたはフォルダーをアップロードします。
- ファイルまたはフォルダーの名前を変更します。
- Zip ファイルを抽出します。
- ファイルまたはフォルダーのプロパティを表示します。
- ファイル サーバー リソース マネージャー[のクォータ](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)を管理します。
- 追加、編集、またはファイル共有を削除します。
- ユーザーとグループにファイル共有にアクセス許可を変更します。

[**ビューのフィードバックとファイルの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)します。

## ファイアウォール

**ファイアウォール**では、ファイアウォールの設定とコンピューターまたはサーバー上の規則を管理することができます。

### 機能

ファイアウォールでは、次の機能がサポートされています。

- ファイアウォールの設定の概要を表示します。
- 受信ファイアウォール規則を表示します。
- 送信のファイアウォール規則を表示します。
- 検索のファイアウォール規則
- ファイアウォール規則の詳細を表示します。
- 新しいファイアウォール規則を作成します。
- 有効にするか、ファイアウォール規則を無効にします。
- ファイアウォール規則を削除します。
- ファイアウォール規則のプロパティを編集します。

[**ビューのフィードバックとファイアウォールの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D)します。

## インストール済みアプリ

**インストールされているアプリ**を表示し、インストールされているアプリケーションをアンインストールできます。

[**ビューのフィードバックとインストールされているアプリの機能を提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D)します。

## ローカル ユーザーとグループ

**ローカル ユーザーとグループ**を使用すると、セキュリティ グループとローカル コンピューターまたはサーバー上に存在するユーザーを管理できます。

### 機能

ローカル ユーザーとグループでは、次の機能がサポートされています。

- ビューと検索のユーザーとグループ
- 新しいユーザーまたはグループを作成します。
- ユーザーのグループ メンバーシップを管理します。
- ユーザーまたはグループを削除します。
- ユーザーのパスワードを変更します。
- ユーザーまたはグループのプロパティを編集します。

[**ローカル ユーザーとグループのフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## ネットワーク

**ネットワーク**では、ネットワーク デバイスとコンピューターまたはサーバー上の設定を管理することができます。

### 機能

ネットワークでは、次の機能がサポートされています。

- 参照し、既存のネットワーク アダプターの検索
- ネットワーク アダプターの詳細を表示します。
- ネットワーク アダプターのプロパティを編集します。
- [Azure ネットワーク アダプター (プレビュー機能)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)の作成します。

[**ネットワークのフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## PowerShell

**PowerShell**では、コンピューターまたは PowerShell セッション経由でサーバーを操作することができます。

### 機能

PowerShell では、次の機能がサポートされています。

- サーバーで対話型 PowerShell セッションを作成します。
- サーバー上の PowerShell セッションから切断します。

[**PowerShell のフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## プロセス

**プロセス**では、コンピューターまたはサーバーで実行中のプロセスを管理することができます。

### 機能

プロセスでは、次の機能がサポートされています。

- 参照し、実行中のプロセスを検索
- プロセスの詳細の表示
- プロセスを開始します。
- プロセスを終了します。
- プロセス ダンプを作成します。
- プロセスのハンドルを見つける

[**ビューのフィードバックとプロセスの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D)します。

## レジストリ

**レジストリ**では、レジストリ キーとコンピューターまたはサーバー上の値を管理することができます。

### 機能

レジストリでは、次の機能がサポートされています。

- レジストリ キーと値を参照します。
- 追加またはレジストリ値を変更します。
- レジストリ値を削除します。

[**ビューのフィードバックとレジストリの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)します。

## リモート デスクトップ

**リモート デスクトップ**では、コンピューターまたは対話型のデスクトップ セッション経由でサーバーを操作することができます。

### 機能

リモート デスクトップでは、次の機能がサポートされています。

- 対話型のリモート デスクトップ セッションを開始します。
- リモート デスクトップ セッションから切断します。
- リモート デスクトップ セッションを Ctrl + Alt + Del を送信します。

[**ビューのフィードバックとリモート デスクトップの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D)します。

## 役割と機能

**役割と機能**を使用すると、役割と機能、サーバーを管理できます。

### 機能

役割と機能では、次の機能がサポートされています。

- 役割と機能をサーバーの一覧を参照します。
- 役割または機能の詳細を表示します。
- 役割または機能をインストールします。
- 役割または機能を削除します。

[**フィードバックを表示し役割と機能の提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D)します。

## スケジュールされたタスク

**スケジュールされたタスク**では、コンピューターまたはサーバー上のスケジュールされたタスクを管理することができます。

### 機能

スケジュールされたタスクでは、次の機能がサポートされています。

- タスク スケジューラ ライブラリを参照します。
- スケジュールされたタスクを編集します。
- _AMP_ 無効にするスケジュールされたタスクを有効にします。
- _AMP_ Stop スケジュールされたタスクを開始します。
- スケジュールされたタスクを作成します。

[**ビューのフィードバックとスケジュールされたタスクの提案された機能**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D)します。

## サービス

**サービス**では、コンピューターまたはサーバー上のサービスを管理することができます。

### 機能

サービスでは、次の機能がサポートされています。

- 参照して、サーバー上のサービスの検索
- サービスの詳細を表示します。
- サービスを開始します。
- サービスを一時停止します。
- サービスのプロパティを編集します。

[**ビューのフィードバックとサービスの機能を提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D)します。

## 設定

**設定**は、コンピューターまたはサーバーの設定を管理するための場所です。

### 機能

- 表示してユーザーとシステム環境変数を変更します。
- [Azure モニター](azure-monitor.md)からアラートを監視するための構成を表示します。
- 表示して、電源構成の変更
- 表示およびリモート デスクトップの設定の変更
- 表示および役割ベースのアクセス制御の設定の変更
- 表示および該当する場合は、HYPER-V ホストの設定を変更

## 記憶域

**記憶域**では、コンピューターまたはサーバー上の記憶域デバイスを管理することができます。

### 機能

記憶域では、次の機能がサポートされています。

- 参照して、サーバー上の既存のディスクを検索
- ディスクの詳細の表示
- ボリュームを作成します。
- ディスクを初期化します。
- 作成し、アタッチ、デタッチ仮想ハード_ディスク (VHD)
- ディスクをオフラインにします。
- ボリュームをフォーマットします。
- ボリュームのサイズを変更します。
- ボリュームのプロパティを編集します。
- ボリュームを削除します。
- クォータの管理をインストールします。

[**記憶域のフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## ストレージ移行サービス

**ストレージ移行サービス**を使用すると、サーバーを移行して、Azure または Windows Server 2019 の共有ファイルが、アプリやユーザーが何も変更を必要とせずします。
[ストレージ移行サービスの概要を確認します。](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>ストレージ移行サービスには、Windows Server 2019 が必要です。

## 記憶域レプリカ

サーバーの記憶域のレプリケーションを管理するのにには、**記憶域レプリカ**を使用します。
[記憶域レプリカについて詳しく知る](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## システム インサイト

**システム インサイト**は、ネイティブの予測分析を紹介を提供する Windows Server は、サーバーの機能に関するインサイトを増加します。
[システム インサイトの概要を確認します。](http://aka.ms/systeminsights)

>[!NOTE]
>システム インサイトは、Windows Server 2019 が必要です。

## アップデート

**更新プログラム**では、コンピューターまたはサーバー上の Microsoft や Windows 更新プログラムを管理することができます。

### 機能

更新プログラムでは、次の機能がサポートされています。

- 利用可能な Windows または Microsoft の更新プログラムを表示します。
- 更新履歴の一覧を表示します。
- 更新プログラムをインストールします。
- Microsoft Update から更新プログラムをオンラインで確認します。
- [Azure アップデート管理](https://docs.microsoft.com/azure/automation/automation-update-management)統合を管理します。

[**更新プログラムのフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## 仮想マシン

[Windows Admin Center で仮想マシンの管理](manage-virtual-machines.md)を参照してください。

## 仮想スイッチ

**仮想スイッチ**には、コンピューターまたはサーバー上の HYPER-V 仮想スイッチを管理することができます。

### 機能

仮想スイッチでは、次の機能がサポートされています。

- 参照して、サーバー上の仮想スイッチの検索
- 新しい仮想スイッチを作成します。
- 仮想スイッチの名前を変更します。
- 既存の仮想スイッチを削除します。
- 仮想スイッチのプロパティを編集します。

[**仮想スイッチのフィードバックと機能の提案を表示します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
