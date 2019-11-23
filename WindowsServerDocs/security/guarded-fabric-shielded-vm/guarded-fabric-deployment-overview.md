---
title: 保護されたファブリックの展開のクイックスタート
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 8359532113e04e2247b4af34effc7f5b89d36f34
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402415"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>保護されたファブリックの展開のクイックスタート

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、保護されたファブリックとは何か、その要件、および展開プロセスの概要について説明します。 詳細な展開手順については、「保護され[たホストとシールドされた vm のホストガーディアンサービスの展開](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)」を参照してください。

ビデオがお好みの場合は、 [Windows Server 2016 でシールドされた vm と保護されたファブリックをデプロイする](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)Microsoft Virtual Academy コースを参照してください。

## <a name="what-is-a-guarded-fabric"></a>保護されたファブリックとは

保護された_ファブリック_とは、システム管理者だけでなく、ホスト上で実行されているマルウェアの検査、盗難、改ざんに対してテナントのワークロードを保護できる Windows Server 2016 hyper-v ファブリックです。 これらの仮想化されたテナントワークロードは、保存時と転送中の両方で保護されます。シールドされた_vm_と呼ばれます。 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>保護されたファブリックの要件

保護されたファブリックの要件は次のとおりです。

- **悪意のあるソフトウェアから無償のシールドされた Vm を実行する場所。**

    これらは、_保護_されたホストと呼ばれます。 
    保護されたホストとは、シールドされた Vm を実行できる Windows Server 2016 Datacenter edition の Hyper-v ホストのことです。これは、信頼できる既知の状態で、ホストガーディアンサービス (HGS) と呼ばれる外部機関に対して実行されていることを証明できる場合にのみ実行できます。 
    HGS は、Windows Server 2016 の新しいサーバーロールであり、通常は3ノードクラスターとして展開されます。 

- **ホストが正常な状態であることを確認する方法。**

    HGS は_構成証明_を実行し、保護されたホストの正常性を測定します。

- **正常なホストに対してキーを安全に解放するプロセス。**

    HGS は_キーの保護とキーのリリース_を実行し、キーは正常なホストに戻されます。

- **シールドされた Vm の安全なプロビジョニングとホスティングを自動化するための管理ツール。**

    必要に応じて、次の管理ツールを保護されたファブリックに追加できます。

    - System Center 2016 Virtual Machine Manager (VMM)。 VMM は、Hyper-v と保護されたファブリックワークロードに付属する PowerShell コマンドレットだけを使用した場合に比べて、追加の管理ツールを提供することをお勧めします。
    - System Center 2016 Service Provider Foundation (SPF)。 これは、Windows Azure Pack と VMM の間の API レイヤーであり、Windows Azure Pack を使用するための前提条件です。
    - Windows Azure Pack は、保護されたファブリックとシールドされた Vm を管理するための優れたグラフィカル web インターフェイスを提供します。 

実際には、保護されたファブリックによって使用される[構成証明のモード](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution)であることを事前に決定しておく必要があります。 2つの方法があります。2つの相互排他モードで、HGS は Hyper-v ホストが正常であることを測定できます。 HGS を初期化する場合は、モードを選択する必要があります。  

- ホストキーの構成証明またはキーモードは、安全性は低くなりますが、導入が簡単です。  
- TPM ベースの構成証明 (TPM モード) はより安全ですが、より多くの構成と特定のハードウェアを必要とします。

必要に応じて、Windows Server 2019 Datacenter edition にアップグレードされた既存の Hyper-v ホストを使用してキーモードで展開し、サーバーハードウェア (TPM 2.0 を含む) をサポートする場合はより安全な TPM モードに変換することができます。 

これらの要素について説明したので、次にデプロイモデルの例を見ていきましょう。

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>現在の Hyper-v ファブリックから保護されたファブリックにアクセスする方法

このシナリオを考えてみましょう。次の図に示す Contoso.com のような既存の Hyper-v ファブリックがあり、Windows Server 2016 で保護されたファブリックを構築したいとします。

![既存の Hyper-v ファブリック](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>手順 1: Windows Server 2016 を実行する Hyper-v ホストを展開する 

Hyper-v ホストでは、Windows Server 2016 Datacenter edition 以降を実行する必要があります。 ホストをアップグレードする場合は、Standard edition から Datacenter edition に[アップグレード](https://technet.microsoft.com/windowsserver/dn527667.aspx)できます。

![Hyper-v ホストのアップグレード](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>手順 2: ホストガーディアンサービス (HGS) を展開する

次に、HGS サーバーの役割をインストールし、次の図の relecloud.com の例のように、3ノードクラスターとして展開します。 これには、次の3つの PowerShell コマンドレットが必要です。

- HGS ロールを追加するには、`Install-WindowsFeature` を使用します。 
- HGS をインストールするには、`Install-HgsServer` を使用します。 
- 選択した構成のモードで HGS を初期化するには、`Initialize-HgsServer` を使用します 

既存の Hyper-v サーバーが TPM モードの前提条件を満たしていない場合 (たとえば、TPM 2.0 がない場合) は、管理者ベースの構成証明 (AD モード) を使用して HGS を初期化できます。これには、ファブリックドメインとの Active Directory 信頼関係が必要です。 

この例では、Contoso は、コンプライアンス要件をすぐに満たすために、最初に AD モードで展開し、適切なサーバーハードウェアを購入した後でセキュリティで保護された TPM ベースの構成証明に変換する計画を作成します。 

![HGS のインストール](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>手順 3: id、ハードウェアベースライン、およびコード整合性ポリシーを抽出する

Hyper-v ホストから id を抽出するプロセスは、使用されている構成証明モードによって異なります。

AD モードの場合、ホストの ID はドメインに参加しているコンピューターアカウントであり、ファブリックドメイン内の指定されたセキュリティグループのメンバーである必要があります。
指定されたグループのメンバーシップは、ホストが正常であるかどうかを判断する唯一の方法です。 

このモードでは、ファブリック管理者は Hyper-v ホストの正常性を保証するだけです。 HGS は、実行が許可されているかどうかを判断するためには何も行わないため、マルウェアとデバッガーは設計どおりに機能します。 

ただし、VM のワーカープロセス (VMWP) は保護されたプロセスライト (PPL) であるため、プロセスに直接接続しようとするデバッガー (WinDbg など) は、シールドされた Vm に対してブロックされます。
LiveKd によって使用されるような代替のデバッグ手法はブロックされません。 シールドされた Vm とは異なり、暗号化がサポートされている Vm のワーカープロセスは PPL として実行されないため、WinDbg などの従来のデバッガーは引き続き正常に機能します。

別の方法として、TPM モードで使用される厳密な検証手順は、AD モードでは使用されません。

TPM モードでは、次の3つが必要です。 

1.  各 Hyper-v ホスト上の TPM 2.0 からの_公開保証キー_ (または_EKpub_)。 EKpub をキャプチャするには、`Get-PlatformIdentifier`を使用します。 
2.  _ハードウェアベースライン_。 各 Hyper-v ホストが同一である場合は、1つのベースラインが必要です。 それ以外の場合は、ハードウェアのクラスごとに1つ必要になります。 ベースラインは、信頼できるコンピューティンググループのログファイル (TCGlog) の形式です。 TCGlog には、ホストが完全に起動された場所まで、ホストが UEFI ファームウェアからカーネルを介して実行したすべてのものが含まれています。 ハードウェアのベースラインを取得するには、Hyper-v の役割と Host Guardian Hyper-v サポート機能をインストールし、`Get-HgsAttestationBaselinePolicy`を使用します。 
3.  _コード整合性ポリシー_。 各 Hyper-v ホストが同一である場合、必要なのは1つの CI ポリシーだけです。 それ以外の場合は、ハードウェアのクラスごとに1つ必要になります。 Windows Server 2016 と Windows 10 の両方に、_ハイパーバイザーによって適用されるコード整合性 (HVCI)_ と呼ばれる、CI ポリシーの新しい形式が適用されています。 HVCI は強力な強制を実現し、信頼された管理者が実行を許可したバイナリのみをホストで実行できるようにします。 これらの手順は、HGS に追加される CI ポリシーでラップされます。 HGS は、シールドされた Vm の実行が許可される前に、各ホストの CI ポリシーを測定します。 CI ポリシーをキャプチャするには、`New-CIPolicy`を使用します。 次に、`ConvertFrom-CIPolicy`を使用して、ポリシーをバイナリ形式に変換する必要があります。

![Id、ベースライン、および CI ポリシーを抽出する](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

これはすべて、保護されたファブリックを実行するインフラストラクチャの観点から構築されたものです。  
シールドされた VM テンプレートディスクとシールドデータファイルを作成して、シールドされた Vm を簡単かつ安全にプロビジョニングできるようになりました。 

## <a name="step-4-create-a-template-for-shielded-vms"></a>手順 4: シールドされた Vm のテンプレートを作成する

シールドされた VM テンプレートは、既知の信頼できる時点でディスクの署名を作成することによって、テンプレートディスクを保護します。 
テンプレートディスクがマルウェアによって後で感染した場合、その署名は、セキュリティで保護されたシールドされた VM のプロビジョニングプロセスによって検出される元のテンプレートとは異なります。 
シールドされたテンプレートディスクを作成するには、シールドされたテンプレートディスク**作成ウィザード**を実行するか、通常のテンプレートディスクに対して `Protect-TemplateDisk` します。 

各は、 [Windows 10 のリモートサーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)のシールドされた**VM ツール**機能に含まれています。
RSAT をダウンロードした後、次のコマンドを実行して、シールドされた**VM ツール**機能をインストールします。

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

ファブリック管理者や VM 所有者などの信頼できる管理者は、VHDX テンプレートディスクに署名するために (多くの場合、ホスティングサービスプロバイダーによって提供される) 証明書が必要です。 

![シールドされたテンプレートディスクウィザード](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

ディスク署名は、仮想ディスクの OS パーティションに対して計算されます。
OS パーティションに何らかの変更が加えられると、署名も変更されます。
これにより、ユーザーは適切な署名を指定することで、信頼するディスクを厳密に特定できます。

開始する前に、[テンプレートのディスク要件](guarded-fabric-create-a-shielded-vm-template.md)を確認してください。 

## <a name="step-5-create-a-shielding-data-file"></a>手順 5: シールドデータファイルを作成する 

シールドデータファイルは、pdk ファイルとも呼ばれ、仮想マシンに関する機密情報 (管理者パスワードなど) をキャプチャします。 

![シールドデータ](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

シールドデータファイルには、シールドされた VM のセキュリティポリシー設定も含まれています。 シールドデータファイルを作成するときは、次の2つのセキュリティポリシーのいずれかを選択する必要があります。

- 意識
   
    最も安全なオプション。多くの管理攻撃ベクトルを排除します。

- 暗号化のサポート

    VM を暗号化することによってコンプライアンスのメリットを引き続き提供する一方で、Hyper-v 管理者は VM コンソール接続と PowerShell Direct を使用するなどの操作を行うことができる、より低いレベルの保護。 

    ![新しい暗号化がサポートされている VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

VMM や Windows Azure Pack などのオプションの管理部分を追加できます。 これらのコンポーネントをインストールせずに VM を作成する場合は、「手順[: VMM なしでシールド](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/)された Vm を作成する」を参照してください。

## <a name="step-6-create-a-shielded-vm"></a>手順 6: シールドされた VM を作成する

シールドされた仮想マシンの作成は、通常の仮想マシンとほとんど異なります。 Windows Azure Pack では、通常の VM を作成するよりも簡単です。これは、名前、シールドデータファイル (その他の特殊化された情報を含む)、および VM ネットワークのみを指定する必要があるためです。 

![Windows Azure Pack の新しいシールドされた VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS の前提条件](guarded-fabric-prepare-for-hgs.md)
