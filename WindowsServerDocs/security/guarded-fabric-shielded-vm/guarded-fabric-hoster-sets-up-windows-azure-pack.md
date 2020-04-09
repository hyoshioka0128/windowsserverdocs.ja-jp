---
title: シールドされた VM - ホスティング サービス プロバイダーで Windows Azure Pack をセットアップする
ms.prod: windows-server
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 1d759af575f98d305a67734d0e23680f701f6b72
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856715"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>シールドされた VM - ホスティング サービス プロバイダーで Windows Azure Pack をセットアップする

このトピックでは、ホスティングサービスプロバイダーが Windows Azure Pack を構成して、テナントがシールドされた Vm をデプロイできるようにする方法について説明します。 Windows Azure Pack は、System Center Virtual Machine Manager の機能を拡張する web ポータルで、テナントが簡単な web インターフェイスを使用して独自の Vm をデプロイして管理できるようにします。 Windows Azure Pack は、シールドされた Vm を完全にサポートし、テナントがシールドデータファイルを作成および管理することをさらに容易にします。

このトピックがシールドされた Vm のデプロイプロセス全体にどのように適合するかを理解するには、「保護された[ホストとシールドされた vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)」を参照してください。

## <a name="setting-up-windows-azure-pack"></a>Windows Azure Pack の設定

環境に Windows Azure Pack を設定するには、次のタスクを実行します。

1. ホストしているファブリックの System Center 2016-Virtual Machine Manager (VMM) の構成を完了します。 これには、VM テンプレートと VM クラウドの設定が含まれます。これは Windows Azure Pack を通じて公開されます。

    [シナリオ-VMM で保護されたホストとシールドされたバーチャルマシンを展開する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. System Center 2016-Service Provider Foundation (SPF) をインストールして構成します。 このソフトウェアを使用すると、Windows Azure Pack が VMM サーバーと通信できるようになります。

    [Service Provider Foundation の展開-SPF](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Windows Azure Pack をインストールし、SPF と通信するように構成します。

    - [Windows Azure Pack のインストール](#install-windows-azure-pack)(このトピック)
    - [Windows Azure Pack を構成する](#configure-windows-azure-pack)(このトピック)

4. Windows Azure Pack に1つ以上のホスティングプランを作成して、テナントが VM クラウドにアクセスできるようにします。

    [Windows Azure Pack でプランを作成](#create-a-plan-in-windows-azure-pack)する (このトピック)

## <a name="install-windows-azure-pack"></a>Windows Azure Pack のインストール

テナントの web ポータルをホストするコンピューターに Windows Azure Pack (WAP) をインストールして構成します。 このコンピューターは、SPF サーバーにアクセスし、テナントから到達できる必要があります。

1.  [WAP のシステム要件](https://technet.microsoft.com/library/dn296442.aspx)を確認し、[前提条件](https://technet.microsoft.com/library/dn469335.aspx)となるソフトウェアをインストールします。

2.  [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)をダウンロードしてインストールします。 コンピューターがインターネットに接続されていない場合は、[オフラインインストールの手順](https://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release)に従います。

3.  Web Platform Installer を開き、[Products] \ (**製品**\) タブで**Windows Azure Pack: ポータルと API Express**を見つけます。 **[追加]** をクリックし、ウィンドウの下部にある **[インストール]** をクリックします。

4.  インストールを続行します。 インストールが完了すると、構成サイト (*https://&lt;wapserver&gt;: 30101/* ) が web ブラウザーで開きます。 この web サイトで、SQL server に関する情報を提供し、WAP の構成を完了します。

Windows Azure Pack の設定の詳細については、「 [Windows Azure Pack の高速展開のインストール](https://technet.microsoft.com/dn296439.aspx)」を参照してください。

> [!NOTE]
> 環境内で既に Windows Azure Pack を実行している場合は、既存のインストールを使用できます。 ただし、最新のシールドされた VM 機能を使用するには、インストールを少なくとも更新プログラムのロールアップ10にアップグレードする必要があります。

### <a name="configure-windows-azure-pack"></a>Windows Azure Pack の構成

Windows Azure Pack を使用する前に、インフラストラクチャ用にインストールして構成しておく必要があります。

1.  *Https://&lt;wapserver&gt;: 30091*で Windows Azure Pack 管理ポータルに移動し、管理者の資格情報を使用してログインします。

2.  左側のウィンドウで、 **[VM クラウド]** をクリックします。

3.  **[System Center Service Provider Foundation の登録]** をクリックして、Windows Azure Pack を Service Provider Foundation インスタンスに接続します。 Service Provider Foundation の URL と、ユーザー名とパスワードを指定する必要があります。

    ![System Center Service Provider Foundation の登録](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  完了すると、VMM 環境で設定されている VM クラウドを確認できるようになります。 続行する前に、WAP で使用可能なシールドされた Vm をサポートする VM クラウドが少なくとも1つあることを確認してください。

### <a name="create-a-plan-in-windows-azure-pack"></a>Windows Azure Pack でプランを作成する

テナントが WAP で Vm を作成できるようにするには、まず、テナントがサブスクライブできるホスティングプランを作成する必要があります。 プランでは、テナントに許可されている VM クラウド、テンプレート、ネットワーク、および課金エンティティを定義します。

1. ポータルの下のウィンドウで、[ **+ 新規**&gt;**計画**&gt; 作成] をクリックしてプランを**作成**します。

2. ウィザードの最初の手順で、プランの名前を選択します。 これは、テナントがサブスクライブするときに表示される名前です。

3. 2番目の手順では、プランで提供するサービスの1つとして **[仮想マシンクラウド]** を選択します。

4. プランのアドオンの選択に関する手順をスキップします。

5. プランを作成するには、[ **OK]** (チェックマーク) をクリックします。 これによってプランが作成されますが、まだ構成された状態ではありません。

   ![Windows Azure Pack のプラン](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. プランの構成を開始するには、その名前をクリックします。

7. 次のページの **[プランサービス]** で、 **[仮想マシンクラウド]** をクリックします。 これにより、このプランのクォータを構成できるページが開きます。

8. **[基本]** で、テナントに提供する VMM 管理サーバーと仮想マシンクラウドを選択します。 シールドされた Vm を提供できるクラウドは、名前の横に **(シールドがサポートされている)** と共に表示されます。

9. この計画で適用するクォータを選択します。 (たとえば、CPU コアおよび RAM 使用率の制限)。 **[Virtual Machines がシールドされることを許可する]** チェックボックスはオンのままにしてください。

   ![Windows Azure Pack の仮想マシンクラウドの設定](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)
    
10. **[テンプレート]** というセクションまで下にスクロールし、テナントに提供する1つ以上のテンプレートを選択します。 シールドされたテンプレートとシールドされていないテンプレートの両方をテナントに提供できますが、VM とそのシークレットの整合性に関してテナントのエンドツーエンドの保証を提供するには、シールドされたテンプレートを用意する必要があります。

11. **[ネットワーク]** セクションで、テナント用に1つまたは複数のネットワークを追加します。

12. プランのその他の設定またはクォータを設定したら、下部にある **[保存]** をクリックします。

13. 画面の左上にある矢印をクリックして、 **[プラン]** ページに戻ります。

14. 画面の下部で、テナントがプランにサブスクライブできるように、プランを**プライベート**から**パブリック**に変更します。

    ![Windows Azure Pack でプランのアクセス権を変更する](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    この時点で、Windows Azure Pack が構成され、テナントは作成したプランにサブスクライブして、シールドされた Vm をデプロイできるようになります。 テナントの完了に必要な追加の手順については、「[テナントのシールドされた vm-Windows Azure Pack を使用](guarded-fabric-shielded-vm-windows-azure-pack.md)したシールドされた Vm のデプロイ」を参照してください。

## <a name="see-also"></a>参照

- [保護されたホストとシールドされた Vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
