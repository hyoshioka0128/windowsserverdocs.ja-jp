---
title: 保護されたファブリックの展開のクイック スタートします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 8e1ef34370b1459cd55705bc0069b49a572de303
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447533"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>保護されたファブリックの展開のクイック スタートします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックではどのような保護されたファブリックは、その要件、および展開プロセスの概要。 展開の詳しい手順については、次を参照してください。[保護されたホストとシールドされた Vm のホスト ガーディアン サービスを展開する](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)します。

ビデオがお好みの場合は、 Microsoft Virtual Academy コースを参照して[シールドされた Vm の展開と Windows Server 2016 で保護されたファブリック](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)します。

## <a name="what-is-a-guarded-fabric"></a>保護されたファブリックとは

A_保護され、fabric_ Windows Server 2016 HYPER-V ファブリックを検査、盗難、およびシステム管理者および、ホストで実行されているマルウェアからの改ざんに対してテナントのワークロードを保護することができます。 これらの仮想化されたテナントのワークロード: 残りの部分とフライトの両方で保護されている: と呼ばれます_シールドされた Vm_。 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>保護されたファブリックを要件します。

保護されたファブリックの要件は次のとおりです。

- **実行する場所のシールドされた Vm は悪意のあるソフトウェアから無料です。**

    これらと呼ばれる_保護されたホスト_します。 
    保護されたホストは、ホスト ガーディアン サービス (HGS) と呼ばれる外部の機関に既知の信頼された状態で実行されているを証明する場合にのみ、シールドされた Vm を実行できる Windows Server 2016 Datacenter edition の HYPER-V ホスト。 
    HGS で Windows Server 2016 では、新しいサーバーの役割は、一般的な 3 ノード クラスターとして展開します。 

- **正常な状態では、ホストを確認します。**

    HGS を実行します_構成証明_、場所、保護されたホストの正常性を測定します。

- **正常なホストにキーを安全に解放するプロセス。**

    HGS を実行します_キーの保護とキーを離す_をキーを正常なホストを解放します。

- **シールドされた Vm の安全なプロビジョニングとのホストを自動化する管理ツールです。**

    必要に応じて、これらの管理ツールは、保護されたファブリックに追加できます。

    - System Center 2016 Virtual Machine Manager (VMM)。 VMM が推奨ツールから Hyper-v ホストと保護されたファブリックのワークロードに付属する PowerShell コマンドレットだけを使用して取得した内容を超える追加の管理を提供するため)。
    - System Center 2016 Service Provider Foundation (SPF)。 これは、Windows Azure Pack と VMM では、Windows Azure Pack を使用するための前提条件と、API レイヤーです。
    - Windows Azure Pack は、保護されたファブリックを管理する適切なグラフィカル web インターフェイスを提供し、シールドされた Vm。 

実際には、1 つの意思決定を前面を行う必要があります。[構成証明モード](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution)保護されたファブリックで使用します。 2 つの方法があります、相互に排他的な 2 つのモード: を HGS を測定できます、HYPER-V ホストが正常な状態でします。 HGS を初期化するときに、モードを選択する必要があります。  

- ホスト キーの構成証明とキー モードのどちらが簡単に調整が安全性が低い  
- TPM ベースの構成証明または TPM モードでは、安全性が高まりますが、構成および特定のハードウェアの詳細が必要です。

必要に応じては、Windows Server 2019 Datacenter edition にアップグレードされた既存の HYPER-V ホストを使用してキーのモードで展開しより安全な TPM モードへの変換し (TPM 2.0 を含む) のサーバー ハードウェアのサポートがある場合。 

わかったら、部分は、デプロイ モデルの例を見てみましょう。

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>保護されたファブリックに現在 HYPER-V ファブリックから取得する方法

このシナリオを想像してみましょう-次の図では、Contoso.com のような既存の HYPER-V ファブリックがあるし、Windows Server 2016 の保護されたファブリックを構築します。

![既存の HYPER-V ファブリック](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>手順 1:Windows Server 2016 を実行している HYPER-V ホストを展開します。 

HYPER-V ホストが Windows Server 2016 Datacenter edition を実行する必要がありますまたはそれ以降。 ホストにアップグレードする場合は、[アップグレード](https://technet.microsoft.com/windowsserver/dn527667.aspx)Datacenter edition を Standard edition から。

![HYPER-V ホストをアップグレードします。](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>手順 2:ホスト ガーディアン サービス (HGS) のデプロイします。

HGS サーバーの役割をインストールし、次の図の relecloud.com 例のように、3 ノード クラスターとしてデプロイします。 これには、次の 3 つの PowerShell コマンドレットが必要です。

- HGS の役割を追加するには、次のように使用します。 `Install-WindowsFeature` 
- HGS をインストールするには、次のように使用します。 `Install-HgsServer` 
- 構成証明書の選択したモードでの HGS を初期化するために次のように使用します。 `Initialize-HgsServer` 

既存の HYPER-V サーバーは、TPM のモードの前提条件を満たしていない場合 (たとえばがない TPM 2.0)、HGS fabric ドメインと Active Directory の信頼を必要とする管理者ベースの証明 (AD モード) を使用して初期化できます。 

この例でと Contoso は、最初にすぐに、コンプライアンス要件を満たすために AD モードで配置し、適切なサーバー ハードウェアを購入した後より安全なの TPM ベースの構成証明に変換することを計画します。 

![HGS のインストール](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>手順 3:Id、ハードウェアの基準、およびコード整合性ポリシーを抽出します。

HYPER-V ホストからの id を抽出するプロセスは、使用されている構成証明モードによって異なります。

AD モードでは、ホストの ID はそのコンピューターをドメインに参加しているアカウントは、fabric ドメイン内の指定したセキュリティ グループのメンバーである必要があります。
指定されたグループのメンバーシップは、ホストが正常であるかどうかの決定がのみです。 

このモードでは、ファブリック管理者は、HYPER-V ホストの正常性を確保するため責任を負うものです。 HGS は何かを実行することはできませんを決定するときに役割を果たしますありません、ためマルウェアとデバッガーが機能に設計されています。 

ただし、デバッガー (WinDbg.exe) などのプロセスに直接アタッチするには、VM のワーカー プロセス (VMWP.exe) が保護されているプロセス light (PPL) であるために、シールドされた Vm のブロックされます。
LiveKd.exe で使用されるものなど、別のデバッグ技術はブロックされません。 シールドされた Vm とは異なり、従来のデバッガーよう WinDbg.exe、PPL が引き続き正常に機能の暗号化サポート Vm ワーカー プロセスは実行されません。

別の方法を説明した TPM モードに使用される厳密な検証手順は任意の方法で AD モードは使用されません。

TPM モードでは、次の 3 つが必要です。 

1.  A_公開保証キー_ (または_EKpub_)、各 HYPER-V ホスト上の TPM 2.0 から。 使用して、EKpub をキャプチャするには、`Get-PlatformIdentifier`します。 
2.  A_ハードウェア ベースライン_します。 HYPER-V ホストの各フィールドが同一の場合、1 つのベースラインは必要です。 そうでない場合は、ハードウェアの各クラスのいずれかを必要があります。 ベースラインは、Trustworthy Computing Group のログ ファイル、または TCGlog の形式のことです。 TCGlog では、すべてのホストがまったく起動まで、カーネルで、UEFI ファームウェアからのホストが含まれています。 ハードウェアのベースラインをキャプチャするには、HYPER-V の役割と Host Guardian HYPER-V サポート機能をインストールして使用`Get-HgsAttestationBaselinePolicy`します。 
3.  A_コード整合性ポリシー_します。 各 HYPER-V ホストが同一の場合、1 つの CI ポリシーだけです。 そうでない場合は、ハードウェアの各クラスのいずれかを必要があります。 Windows Server 2016 および Windows 10 と呼ばれる CI ポリシーの強制の新しいフォームがある_ハイパーバイザーによって適用されるコードの整合性 (HVCI)_ します。 HVCI は強力な強制を提供し、ホストが信頼された管理者が実行するように許可されているバイナリの実行にのみ許可されているようにします。 これらの手順については、HGS に追加される CI ポリシーでラップされます。 HGS は、許可されているシールドされた Vm を実行する前に、各ホストの CI ポリシーを測定します。 CI ポリシーを取得するには、`New-CIPolicy`します。 ポリシーは、バイナリ形式を使用してそのにし、変換する必要があります`ConvertFrom-CIPolicy`します。

![Id、ベースラインおよび CI ポリシーを抽出します。](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

すべて、それを実行するインフラストラクチャの観点から、保護されたファブリックを構築します。  
シールドされた VM テンプレート ディスク、シールドされたため、シールド データ ファイルを作成できるようになりました容易かつ安全に Vm をプロビジョニングすることができます。 

## <a name="step-4-create-a-template-for-shielded-vms"></a>手順 4:シールドされた Vm のテンプレートを作成します。

シールドされた VM テンプレートは、既知の信頼できる時点でのディスクの署名を作成して、テンプレート ディスクを保護します。 
テンプレート ディスクがマルウェアに感染した後で、その署名がセキュリティで保護されたシールドされた VM のプロビジョニング プロセスでは検出が元のテンプレートに異なります。 
シールドされたテンプレート ディスクは、実行によって作成される、**シールドされたテンプレート ディスクの作成ウィザード**または`Protect-TemplateDisk`に対して通常のテンプレート ディスク。 

含まれている各、**シールドされた VM ツール**機能、[リモート サーバー管理ツールの Windows 10](https://www.microsoft.com/download/details.aspx?id=45520)します。
RSAT をダウンロードした後は、インストールするには、このコマンドを実行、**シールドされた VM ツール**機能。

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

ファブリック管理者や VM の所有者などの信頼できる管理者は、(多くの場合は、ホスティング サービス プロバイダーによって提供される) 証明書を VHDX テンプレート ディスクを署名する必要があります。 

![シールドされたテンプレート ディスク ウィザード](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

仮想ディスクの OS パーティション上で、ディスク署名が計算されます。
OS パーティションの変更が行われる、シグネチャも変更されます。
これにより、厳密に適切なシグネチャを指定することで信頼するどのディスクを識別できます。

レビュー、[テンプレート ディスク要件](guarded-fabric-create-a-shielded-vm-template.md)開始する前にします。 

## <a name="step-5-create-a-shielding-data-file"></a>手順 5:シールド データ ファイルを作成します。 

シールド データ ファイル、.pdk ファイルとも呼ばれますが、管理者パスワードなど、仮想マシンに関する機密情報をキャプチャします。 

![シールド データ](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

シールド データ ファイルには、シールドされた VM のセキュリティ ポリシーの設定も含まれています。 シールド データ ファイルを作成するときに、2 つのセキュリティ ポリシーのいずれかを選択する必要があります。

- シールドされました。
   
    多くの管理の攻撃ベクトルを排除する最も安全なオプションです。

- 暗号化をサポート

    低いレベルのコンプライアンス VM を暗号化できるという利点は、HYPER-V 管理者のような作業を行うことを許可する保護は、VM コンソール接続や PowerShell ダイレクトを使用します。 

    ![新しい暗号化サポート VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

VMM または Windows Azure Pack のようなオプションの管理情報を追加することができます。 これらの項目をインストールせずに VM を作成、表示するかかどうか[ステップ バイ ステップ: VMM なしのシールドされた Vm の作成](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/)です。

## <a name="step-6-create-a-shielded-vm"></a>手順 6:シールドされた VM を作成します。

わずかなシールドされたバーチャル マシンの作成とは異なる標準の仮想マシンから。 Windows Azure pack、操作は、通常の VM を作成するだけで済むため、名前を指定する (他の特殊化情報を含む)、データ ファイルと、VM ネットワークをシールドよりも簡単です。 

![Windows Azure Pack 内で新しいシールドされた VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS の前提条件](guarded-fabric-prepare-for-hgs.md)
