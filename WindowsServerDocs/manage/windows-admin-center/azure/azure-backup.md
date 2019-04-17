---
title: Azure のバックアップと Windows Admin Center から、Windows サーバーをバックアップします。
description: Azure のバックアップのバックアップ Windows サーバーを使用して Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 3983d0b65bc69ef9fd40f3c8e196d40534b1b8f9
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296981"
---
# Azure のバックアップと Windows Admin Center から、Windows サーバーをバックアップします。

>適用対象: Windows Admin Center Preview、Windows Admin Center

[Windows Admin Center での Azure 統合の詳細](../plan/azure-integration-options.md)

Windows Admin Center は、Azure、Windows サーバーをバックアップし、偶発的なまたは悪意のある削除、破損でもランサムウェアから保護するプロセスを効率化します。 セットアップを自動化するには、Windows Admin Center ゲートウェイを Azure に接続できます。

Windows Server のバックアップを構成し、サーバーのボリュームと Windows Admin Center から Windows システムの状態のバックアップをバックアップ ポリシーを作成するには、次の情報を使用します。

## Azure Backup とどのように動作する Windows Admin center かどうか。 

**Azure Backup**バックアップ (またはを保護する) を使用できる Azure ベースのサービスは、Microsoft cloud で、データを復元します。 Azure のバックアップは、信頼性の高い、安全、かつコスト競争力のあるは、クラウド ベースのソリューションを使用して、既存のオンプレミスまたはオフサイトのバックアップ ソリューションを置き換えます。
[Azure Backup について詳しく説明します](https://docs.microsoft.com/azure/backup/backup-overview)。

Azure のバックアップをダウンロードして、適切なコンピューターに展開する複数のコンポーネントは、サーバー、またはクラウドにします。 コンポーネント、またはエージェントは、展開を保護する内容によって異なります。 Azure での Recovery Services コンテナーにデータをバックアップするすべての Azure Backup コンポーネント (オンプレミスでデータを保護しているかどうかに関係なく、または Azure 内) を使用できます。

Windows Admin Center での Azure Backup の統合は、ボリュームと、Windows システムの状態、オンプレミス Windows 物理または仮想サーバー バックアップに最適です。 これにより、ファイル サーバー、ドメイン コント ローラーと IIS Web サーバー バックアップを作成するための包括的なメカニズムです。

Windows Admin Center は、ネイティブの**バックアップ**ツールによって Azure Backup 統合を公開します。 **バックアップ**のツールでは、管理の設定と、サーバーのバックアップをすばやく開始するエクスペリエンスを監視するには、一般的なバックアップと復元実行操作と、Windows サーバーの全体的なバックアップの正常性を監視します。

## 前提条件と計画

- 1 つ以上のアクティブなサブスクリプションを持つ Azure アカウント
- ターゲットにする Windows サーバー バックアップは Azure にインターネット アクセスが必要
- [Azure に、Windows Admin Center ゲートウェイに接続します。](azure-integration.md)

Windows サーバーのバックアップをワークフローを開始するには、サーバーの接続を開く**バックアップ**ツールで、手順を以下に説明します。

## Azure のバックアップをセットアップします。
Azure Backup がまだ有効でないサーバー接続の**バックアップ**ツールをクリックすると、 **Azure Backup へようこそ**画面が表示されます。 **Azure バックアップの設定**] ボタンをクリックします。 これにより、Azure Backup セットアップ ウィザードが開きます。 サーバーをバックアップするウィザードで、以下に示す手順に従います。

Azure Backup が既に構成されている場合、**バックアップ**ツールをクリックすると、**ダッシュ ボードのバックアップ**が開きます。 操作と、ダッシュ ボードから実行できるタスクを検出する ([管理および監視](#management-and-monitoring)) セクションをご覧ください。

### 手順 1: Microsoft Azure ログイン
Azure アカウントにサインインします。 

> [!NOTE]
> 場合は、Windows Admin Center ゲートウェイを Azure を接続すると、する必要がありますが自動的にログインした Azure します。 クリックしてできる**サインアウト**さらにサインインするのには、別のユーザーとしてします。

### 手順 2: Azure Backup を設定します。
以下のように、Azure Backup の適切な設定を選択します。

 - **サブスクリプション Id:** Azure に、Windows Server バックアップを使用する Azure サブスクリプションです。 Azure リソース グループなどのすべての Azure アセット、選択したサブスクリプションで Recovery Services コンテナーが作成されます。
 - **資格情報コンテナー:** サーバーのバックアップの保存場所 Recovery Services コンテナーです。 Windows Admin Center は新しい資格情報コンテナーを作成または既存のボルトから選択できます。  
 - **リソース グループ:** Azure リソース グループは、リソースのコレクションのコンテナーです。 Recovery Services コンテナーが作成または指定したリソース グループに含まれています。 既存のリソース グループから選択できるまたは Windows Admin Center は新しいものを作成します。
 - **場所:** Azure リージョン Recovery Services コンテナーが作成されます。 Windows Server に最も近い Azure リージョンを選択することをお勧めします。

### 手順 3: バックアップ アイテムとスケジュールを選択します。

- サーバーからをバックアップするを選択します。 Windows Admin Center では、バックアップのサイズの見積もり選択されているデータを提供しながら**ボリューム**と**Windows システムの状態**の組み合わせを選択することができます。

> [!NOTE]
> 最初のバックアップでは、選択したすべてのデータの完全バックアップです。 ただし、それ以降のバックアップでは、本質的に増分し、以前のバックアップからデータへの変更のみを転送します。

- システムの状態やボリュームの複数の**バックアップのスケジュール**を事前設定から選択します。

### 手順 4: 暗号化パスフレーズを入力します。

- 選択した (最小 16 文字)、**暗号化パスフレーズ**を入力します。  **Azure のバックアップ**は、ユーザー設定し、ユーザーで管理される暗号化パスフレーズでは、バックアップ データを保護します。 Azure Backup からデータを回復するには、暗号化パスフレーズが必要です。

> [!NOTE]
> パスフレーズは、別のサーバーまたは[Azure Key Vault](https://docs.microsoft.com/azure/key-vault/quick-create-portal)などのオフサイトの安全な場所に格納する必要があります。 Microsoft は、パスフレーズを格納し、できません取得やしませんが紛失または忘れてパスフレーズをリセットします。

- すべての設定を確認し、**適用**] をクリックしてください

Windows Admin Center は次の操作を実行し、

1. 既に存在しない場合は、Azure リソース グループを作成します。
2. 指定されている Azure Recovery Services コンテナーを作成します。
3. インストールして、資格情報コンテナーに Microsoft Azure 回復サービス エージェントの登録
4. 選択したオプションに従ったバックアップおよび保存のスケジュールを作成し、Windows Server に関連付けます。

## 管理と監視

したら正常にセットアップ Azure Backup ときに、表示する**バックアップ ダッシュ ボード**の既存のサーバー接続をバックアップ ツールを開きます。 **バックアップ ダッシュ ボード**から、次のタスクを実行することができます。

- **Azure で資格情報コンテナーにアクセス:**[豊富な管理操作](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server)を実行する Azure で資格情報コンテナーを実行する**バックアップのダッシュ ボード**の [**概要**] タブで**Recovery Services コンテナー**のリンクをクリックすることができます。
- **アドホック バックアップを実行する:****今すぐバックアップ**アドホックのバックアップをクリックします。 
- **ジョブの監視およびを構成するアラートの通知:** 継続的に監視するためのダッシュ ボードの **[ジョブ**] タブに移動または過去のジョブと[アラートの通知を構成する](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts)すべてのメールを受信するジョブまたはその他のバックアップの関連するアラートに失敗しました。
- **ビュー回復ポイントと回復データ:** 回復ポイントを表示し、Azure からデータを回復する手順については、**データの回復**をクリックして、ダッシュ ボードの**回復ポイント**] タブをクリックします。