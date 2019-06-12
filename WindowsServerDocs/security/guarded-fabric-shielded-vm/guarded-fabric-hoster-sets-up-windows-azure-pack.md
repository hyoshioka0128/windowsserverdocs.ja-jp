---
title: シールドされた VM - ホスティング サービス プロバイダーで Windows Azure Pack をセットアップする
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 156832087bc7af0c95a92cab9a0c1501264d47a5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447507"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>シールドされた VM - ホスティング サービス プロバイダーで Windows Azure Pack をセットアップする

このトピックでは、ホスティング サービス プロバイダーを構成方法 Windows Azure Pack テナントを使用するとシールドされた Vm のデプロイに使用できるようにについて説明します。 Windows Azure パックは、web ポータルの System Center Virtual Machine Manager の展開および単純な web インターフェイスを通じて、各自の Vm を管理するテナントを許可する機能を拡張します。 Windows Azure Pack は、完全にシールドされた Vm をサポートしているし、テナントを作成して、シールド データ ファイルの管理も容易になります。

このトピックがシールドされた Vm の展開の全体的なプロセスがどのように適合するしくみを理解するのを参照してください。[保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしている](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)します。

## <a name="setting-up-windows-azure-pack"></a>Windows Azure Pack のセットアップ

環境内で Windows Azure Pack を設定する次のタスクを行います。

1. System Center 2016 - ホスティング ファブリックを Virtual Machine Manager (VMM) の構成を完了します。 これには、VM テンプレートと、Windows Azure パックを通じて公開される VM クラウドの設定が含まれます。

    [シナリオ - 保護されたホストと VMM のシールドされた仮想マシンのデプロイ](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. インストールし、System Center 2016 - Service Provider Foundation (SPF) を構成します。 このソフトウェアは、VMM サーバーと通信するために Windows Azure Pack を有効にします。

    [Service Provider Foundation の SPF の展開](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Windows Azure Pack をインストールし、SPF と通信するように構成します。

    - [Windows Azure Pack インストール](#install-windows-azure-pack)(」を参照)
    - [Windows Azure Pack を構成する](#configure-windows-azure-pack)(」を参照)

4. テナントの VM クラウドへのアクセスを許可する Windows Azure Pack では、1 つまたは複数のホスティング プランを作成します。

    [Windows Azure Pack の計画を作成](#create-a-plan-in-windows-azure-pack)(」を参照)

## <a name="install-windows-azure-pack"></a>インストールの Windows Azure Pack

インストールし、テナントの web ポータルをホストするコンピューターで Windows Azure パック (WAP) を構成します。 このマシンは、SPF サーバーに到達し、テナントで到達可能である必要があります。

1.  レビュー [WAP のシステム要件](https://technet.microsoft.com/library/dn296442.aspx)をインストールし、[前提条件のソフトウェア](https://technet.microsoft.com/library/dn469335.aspx)します。

2.  ダウンロードしてインストール、 [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)します。 次のコンピューターがインターネットに接続されていない場合、[オフライン インストール手順](http://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release)します。

3.  Web Platform Installer を開き、検索**Windows Azure Pack:ポータルおよび API Express**下、**製品**タブ。クリックして**追加**、し**インストール**ウィンドウの下部にあります。

4.  インストールを続行します。 インストールが完了したら、構成サイト (*https://&lt;wapserver&gt;: 30101/* )、web ブラウザーで開きます。 この web サイトで、SQL server に関する情報を提供し、WAP の構成を完了します。

Windows Azure パックのヘルプ設定は、次を参照してください。 [Windows Azure Pack のデプロイの高速インストール](https://technet.microsoft.com/dn296439.aspx)します。

> [!NOTE]
> 環境内で既に Windows Azure Pack を実行する場合は、既存のインストールを使用する可能性があります。 シールドされた VM の機能を最新バージョンを使用するには、少なくともにインストールをアップグレードする必要があります、ただし、更新プログラム ロールアップ 10。

### <a name="configure-windows-azure-pack"></a>構成の Windows Azure Pack

Windows Azure Pack を使用する前にインストールされているし、インフラストラクチャ用に構成されたことを既にがあります。

1.  Windows Azure Pack 管理者ポータルに移動*https://&lt;wapserver&gt;: 30091*、し、管理者の資格情報を使用してログインします。

2.  左側のウィンドウで次のようにクリックします。 **VM クラウド**します。

3.  Windows Azure Pack をクリックして、Service Provider Foundation のインスタンスに接続**System Center の Service Provider Foundation を登録**します。 Service Provider foundation では、URL だけでなく、ユーザー名とパスワードを指定する必要があります。

    ![登録の System Center Service Provider Foundation](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  完了すると、VM クラウドが VMM 環境内で設定を参照してください。 はずです。 続行する前にシールドされた Vm の WAP で利用できるをサポートするには少なくとも 1 つの VM クラウドがあることを確認します。

### <a name="create-a-plan-in-windows-azure-pack"></a>Windows Azure Pack の計画を作成します。

テナントの WAP での Vm の作成を許可するためには、まずテナントのサブスクライブ、ホスティング プランを作成する必要があります。 プランは、テナントの VM クラウドが許可されている、テンプレート、ネットワーク、および課金エンティティを定義します。

1. ポータルの下のウィンドウで、をクリックして **+ 新規** &gt; **計画** &gt; **プランの作成**です。

2. ウィザードの最初の手順では、プランの名前を選択します。 これは、名前のテナントがサブスクライブしているときに表示されます。

3. 2 番目の手順では、次のように選択します。**仮想マシン クラウド**として、プランで提供するサービスの 1 つ。

4. プランのアドオンを選択する方法について手順をスキップします。

5. をクリックして**OK** (チェック マーク)、プランを作成します。 これには、プランが作成されます、これがまだ構成されている状態には

   ![Windows Azure でのプランをパック](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. プランの構成を開始するには、その名前をクリックします。

7. 次のページで [**プラン サービス**、] をクリックして**仮想マシン クラウド**します。 このプランのクォータを構成するページが開きます。

8. **基本**、VMM 管理サーバーと、テナントに提供する仮想マシン クラウドを選択します。 シールドされた Vm が提供できるクラウドが表示されます **(シールドはサポートされている)** 名前の横にあります。

9. このプランを適用するクォータを選択します。 (たとえば、制限の CPU コアと RAM 使用量)。 ままにすることを確認、**を許可する仮想マシンをシールドする**チェック ボックスをオンします。

   ![Windows Azure Pack での仮想マシン クラウドの設定](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)
    
10. 」のセクションまで下へスクロール**テンプレート**、テナントに提供する 1 つまたは複数のテンプレートを選択します。 両方のシールドされ、テナントの VM とその秘密情報の整合性に関するエンド ツー エンドの保証を提供するが、シールドされていないテナントでは、テンプレート、シールドされたテンプレートを提供する必要がありますを提供することができます。

11. **ネットワーク**セクションで、テナントの 1 つまたは複数のネットワークを追加します。

12. プランの他の設定またはクォータを設定した後は、クリックして**保存**下部にあります。

13. 画面の左上で、バックアップする矢印をクリックして、**計画**ページ。

14. 画面の下部には、プランを変更されてから**プライベート**に**パブリック**プランにテナントがサブスクライブできるようにします。

    ![Windows Azure Pack のプランのアクセスを変更します。](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    この時点では、Windows Azure Pack が構成され、テナントが作成したプランをサブスクライブして、シールドされた Vm をデプロイすることになります。 テナントが完了する必要がある追加の手順では、次を参照してください。[テナント - Windows Azure Pack を使用して、シールドされた VM を展開するためのシールドされた Vm](guarded-fabric-shielded-vm-windows-azure-pack.md)します。

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしています。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
