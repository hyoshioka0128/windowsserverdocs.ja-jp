---
title: Windows 管理センターから Azure Backup を使用して Windows サーバーをバックアップする
description: Windows 管理センター (Project ホノルル) を使用して、Windows サーバーを Azure Backup でバックアップする
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.openlocfilehash: 796dfe509b1d24595dd3bc1aedd514789f4a378b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949636"
---
# <a name="backup-your-windows-servers-from-windows-admin-center-with-azure-backup"></a>Windows 管理センターから Azure Backup を使用して Windows サーバーをバックアップする

>適用先:Windows Admin Center Preview、Windows Admin Center

[Azure と Windows 管理センターとの統合の詳細については、こちらを参照してください。](../plan/azure-integration-options.md)

Windows 管理センターでは、Windows サーバーを Azure にバックアップし、偶発的または悪意のある削除、破損、またはランサムウェアから保護するプロセスを効率化します。 セットアップを自動化するには、Windows Admin Center ゲートウェイを Azure に接続できます。

次の情報を使用して、Windows Server のバックアップを構成し、バックアップポリシーを作成して、Windows 管理センターからサーバーのボリュームと Windows システムの状態をバックアップします。

## <a name="what-is-azure-backup-and-how-does-it-work-with-windows-admin-center"></a>Azure Backup とはどのようなものですか。また、Windows 管理センターではどのように動作しますか。

**Azure Backup**は、Microsoft クラウド内のデータのバックアップ (または保護) と復元に使用できる Azure ベースのサービスです。 Azure Backup では、既存のオンプレミスまたはオフサイトのバックアップ ソリューションを、信頼性の高い、セキュリティで保護された、コスト競争力のあるクラウド ベースのソリューションに置き換えます。
[詳細について](https://docs.microsoft.com/azure/backup/backup-overview)は、Azure Backup を参照してください。

Azure Backup には複数のコンポーネントが用意されており、これを適切なコンピューター、サーバー、またはクラウドにダウンロードしてデプロイします。 デプロイするコンポーネント (エージェント) は、何を保護するかによって決まります。 オンプレミスまたは Azure のどちらでデータを保護しているかにかかわらず、すべての Azure Backup コンポーネントを使用して、Azure の Recovery Services コンテナーにデータをバックアップできます。

Windows 管理センターでの Azure Backup の統合は、ボリュームと Windows システム状態のオンプレミス Windows 物理サーバーまたは仮想サーバーをバックアップする場合に最適です。 これにより、ファイルサーバー、ドメインコントローラー、IIS Web サーバーをバックアップするための包括的なメカニズムが実現されます。

Windows 管理センターでは、ネイティブ**バックアップ**ツールを使用して Azure Backup 統合を公開しています。 **バックアップ**ツールは、サーバーのバックアップをすばやく開始し、一般的なバックアップと復元の操作を実行し、Windows サーバーの全体的なバックアップ正常性を監視するためのセットアップ、管理、および監視のためのエクスペリエンスを提供します。

## <a name="prerequisites-and-planning"></a>前提条件と計画

- 少なくとも1つのアクティブなサブスクリプションを持つ Azure アカウント
- バックアップするターゲットの Windows サーバーは、Azure にインターネットにアクセスできる必要があります。
- [Windows 管理センターゲートウェイを Azure に接続する](azure-integration.md)

Windows サーバーをバックアップするためのワークフローを開始するには、サーバー接続を開き、**バックアップ**ツールをクリックして、次の手順に従います。

## <a name="setup-azure-backup"></a>セットアップ Azure Backup
Azure Backup がまだ有効になっていないサーバー接続の**バックアップ**ツールをクリックすると、[ **Azure Backup へようこそ**] 画面が表示されます。 [ **Azure Backup の設定**] ボタンをクリックします。 これにより、Azure Backup セットアップウィザードが開きます。 ウィザードに表示される次の手順に従って、サーバーをバックアップします。

Azure Backup が既に構成されている場合は、**バックアップ**ツールをクリックすると、**バックアップダッシュボード**が開きます。 ダッシュボードから実行できる操作とタスクについては、「([管理と監視](#management-and-monitoring))」セクションを参照してください。

### <a name="step-1-login-to-microsoft-azure"></a>手順 1: Microsoft Azure にログインする
Azure アカウントにサインインします。

> [!NOTE]
> Windows 管理センターゲートウェイを Azure に接続している場合は、自動的に Azure にログインする必要があります。 [**サインアウト**] をクリックすると、別のユーザーとしてさらにサインインできます。

### <a name="step-2-set-up-azure-backup"></a>手順 2:Azure Backup をセットアップする
次に示すように、Azure Backup に適した設定を選択します。

 - **サブスクリプション Id:** Windows Server を Azure にバックアップするために使用する Azure サブスクリプション。 Azure リソースグループ、Recovery Services コンテナーなどのすべての Azure 資産は、選択したサブスクリプションに作成されます。
 - **コンテナー:** サーバーのバックアップが格納される Recovery Services コンテナー。 既存のコンテナーから選択することも、Windows 管理センターで新しいコンテナーを作成することもできます。
 - **[リソース グループ]:** Azure リソース グループは、リソースのコレクションのコンテナーです。 Recovery Services コンテナーが作成されているか、指定されたリソースグループに含まれています。 既存のリソースグループから選択することも、Windows 管理センターで新しいリソースグループを作成することもできます。
 - **[場所]:** Recovery Services コンテナーが作成される Azure リージョン。 Windows Server に最も近い Azure リージョンを選択することをお勧めします。

### <a name="step-3-select-backup-items-and-schedule"></a>手順 3: バックアップ項目とスケジュールを選択する

- サーバーからバックアップする対象を選択します。 Windows 管理センターでは、バックアップ対象として選択されているデータの推定サイズを提供しながら、**ボリューム**と**Windows システムの状態**の組み合わせから選択することができます。

> [!NOTE]
> 最初のバックアップは、選択したすべてのデータの完全バックアップです。 ただし、それ以降のバックアップは増分的に行われ、前回のバックアップ以降のデータへの変更のみが転送されます。

- システム状態やボリュームについて、複数の事前設定された**バックアップスケジュール**から選択します。

### <a name="step-4-enter-encryption-passphrase"></a>手順 4: 暗号化のパスフレーズを入力する

- 任意の**暗号化パスフレーズ**(16 文字以上) を入力します。  **Azure Backup**は、ユーザーが構成し、ユーザーが管理する暗号化パスフレーズを使用してバックアップデータを保護します。 Azure Backup からデータを回復するには、暗号化パスフレーズが必要です。

> [!NOTE]
> パスフレーズは、別のサーバーや[Azure Key Vault](https://docs.microsoft.com/azure/key-vault/quick-create-portal)など、安全なオフサイトの場所に格納する必要があります。 Microsoft はパスフレーズを保存しません。パスフレーズを紛失したり忘れたりした場合、パスフレーズを取得またはリセットすることはできません。

- すべての設定を確認し、[**適用**] をクリックします。

Windows 管理センターは次の操作を実行します

1. Azure リソースグループがまだ存在しない場合は作成する
2. 指定に従って Azure Recovery Services 資格情報コンテナーを作成する
3. Microsoft Azure Recovery Services エージェントをインストールし、コンテナーに登録する
4. 選択したオプションに従ってバックアップと保持のスケジュールを作成し、Windows Server に関連付けます。

## <a name="management-and-monitoring"></a>管理と監視

Azure Backup が正常にセットアップされると、既存のサーバー接続のバックアップツールを開いたときに、**バックアップダッシュボード**が表示されます。 **バックアップダッシュボード**では、次のタスクを実行できます。

- **Azure でのコンテナーへのアクセス:****バックアップダッシュボード**の [**概要**] タブにある [ **Recovery Services コンテナー** ] リンクをクリックすると、Azure のコンテナーに移動して、[豊富な管理操作](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server)を実行することができます。
- アドホック**バックアップを実行する:**[**今すぐバックアップ**] をクリックして、アドホックバックアップを作成します。
- **ジョブを監視し、アラート通知を構成します。** ダッシュボードの [**ジョブ**] タブに移動して、進行中または過去のジョブを監視し、失敗したジョブまたはその他のバックアップ関連のアラートの電子メールを受信するように[アラート通知を構成](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts)します。
- **回復ポイントの表示とデータの回復:** ダッシュボードの [**回復ポイント**] タブをクリックして回復ポイントを表示し、Azure からデータを回復する手順については、[**データの回復**] をクリックします。