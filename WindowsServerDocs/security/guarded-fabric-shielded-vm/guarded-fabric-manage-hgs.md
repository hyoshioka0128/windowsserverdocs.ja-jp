---
title: ホストガーディアンサービスの管理
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 41912c90beacbb0c0c285ea4da8305c1afdf2a51
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322604"
---
# <a name="managing-the-host-guardian-service"></a>ホストガーディアンサービスの管理

> 適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホストガーディアンサービス (HGS) は、保護されたファブリックソリューションの中心的な場所です。
これは、ファブリック内の Hyper-v ホストがホスト側またはエンタープライズ向けに認識され、信頼されたソフトウェアが実行されていることを確認し、シールドされた Vm を起動するために使用するキーを管理する役割を担います。
テナントは、シールドされた Vm をホストすることを信頼することを決定した場合、ホストガーディアンサービスの構成と管理に信頼を配置します。
そのため、保護されたファブリックのセキュリティ、可用性、および信頼性を確保するために、ホストガーディアンサービスを管理するときは、ベストプラクティスに従うことが非常に重要です。
以下のセクションのガイダンスでは、HGS の管理者が直面する最も一般的な操作上の問題について説明します。

## <a name="limiting-admin-access-to-hgs"></a>管理者アクセスを HGS に制限する
HGS のセキュリティが重要な性質のため、管理者が組織の高度に信頼されたメンバーであり、ファブリックリソースの管理者とは別に管理者であることを確認することが重要です。
また、セキュリティで保護された通信プロトコル (たとえば、HTTPS 経由の WinRM) を使用して、セキュリティで保護されたワークステーションからのみ HGS を管理することをお勧めします。

### <a name="separation-of-duties"></a>職務の分離
HGS を設定するときに、HGS 専用の分離 Active Directory フォレストを作成するか、既存の信頼されたドメインに HGS を参加させるかを選択できます。
この決定と、組織内で管理者を割り当てる役割によって、HGS の信頼境界が決定されます。
Hgs にアクセスできるユーザーは、管理者として直接、または HGS に影響を与える可能性のある他の管理者 (Active Directory など) の管理者として、保護されたファブリックを制御できます。
HGS 管理者は、シールドされた Vm を実行する権限がある Hyper-v ホストを選択し、シールドされた Vm を起動するために必要な証明書を管理します。
HGS にアクセスできる攻撃者や悪意のある管理者は、この機能を使用して、シールドされた Vm を実行したり、キーマテリアルを削除してサービス拒否攻撃を開始したりするために、侵害されたホストを承認できます。

このリスクを回避するには、HGS の管理者 (HGS が参加するドメインを含む) と Hyper-v 環境の重複を制限することを*強く*お勧めします。
どちらの管理者も両方のシステムにアクセスできないようにするために、攻撃者は2人の異なる2つのアカウントを侵害し、その任務を完了して HGS ポリシーを変更する必要があります。
これは、2つの Active Directory 環境の domain と enterprise admins を同じユーザーにすることも、HGS で Hyper-v ホストと同じ Active Directory フォレストを使用することもできないことを意味します。
より多くのリソースへのアクセス権を自分に付与できるユーザーは、セキュリティ上のリスクになります。

### <a name="using-just-enough-administration"></a>十分な管理だけを使用する
HGS には、より安全に管理するのに役立つ[十分な管理](https://aka.ms/JEAdocs)(jea) ロールが組み込まれています。
JEA は、管理者のタスクを管理者以外のユーザーに委任できるようにするために役立ちます。つまり、HGS ポリシーを管理するユーザーは、実際には、コンピューターまたはドメイン全体の管理者である必要はありません。
JEA は、ユーザーが PowerShell セッションで実行できるコマンドを制限し、バックグラウンドの背後にある一時的なローカルアカウント (各ユーザーセッションで一意) を使用して、通常は昇格が必要なコマンドを実行します。

HGS には、あらかじめ構成される2つの JEA ロールが付属しています。
- **Hgs 管理者**。ユーザーは、シールドされた vm を実行する新しいホストの承認など、すべての hgs ポリシーを管理できます。
- 既存のポリシーを監査する権限をユーザーにのみ許可する**HGS レビュー担当者**。 HGS の構成に変更を加えることはできません。

JEA を使用するには、最初に新しい標準ユーザーを作成し、そのユーザーを HGS 管理者グループまたは HGS レビュー担当者グループのメンバーにする必要があります。
`Install-HgsServer` を使用して HGS の新しいフォレストを設定した場合、これらのグループにはそれぞれ "*servicename*Administrators" と "*servicename*レビューアー" という名前が付けられます。ここで、 *servicename*は hgs クラスターのネットワーク名です。
HGS を既存のドメインに参加させた場合は、`Initialize-HgsServer`で指定したグループ名を参照する必要があります。

**HGS 管理者ロールとレビューアーロールの標準ユーザーを作成する**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**レビュー担当者ロールを持つ監査ポリシー**

HGS にネットワーク接続されているリモートコンピューターで、PowerShell で次のコマンドを実行して、レビュー担当者の資格情報を持つ JEA セッションに入力します。
レビュー担当者アカウントは標準ユーザーであるため、通常の Windows PowerShell リモート処理、HGS へのリモートデスクトップアクセスなどでは使用できないことに注意してください。

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

その後、`Get-Command` でセッションで許可されているコマンドを確認し、許可されたコマンドを実行して構成を監査できます。
次の例では、HGS で有効になっているポリシーを確認しています。

```powershell
Get-Command

Get-HgsAttestationPolicy
```

JEA セッションの操作が完了したら、コマンド `Exit-PSSession` またはそのエイリアスである `exit`を入力します。 

**管理者ロールを使用して HGS に新しいポリシーを追加する**

ポリシーを実際に変更するには、' hgsAdministrators ' グループに属している id を使用して JEA エンドポイントに接続する必要があります。
次の例では、新しいコード整合性ポリシーを HGS にコピーし、JEA を使用して登録する方法を示します。
構文は、使用したものとは異なる場合があります。
これは、完全なファイルシステムにアクセスできないなど、JEA のいくつかの制限に対応するためです。

```powershell
$cipolicy = Get-Item "C:\temp\cipolicy.p7b"
$session = New-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsadmin01' -ConfigurationName 'microsoft.windows.hgs'
Copy-Item -Path $cipolicy -Destination 'User:' -ToSession $session

# Now that the file is copied, we enter the interactive session to register it with HGS
Enter-PSSession -Session $session
Add-HgsAttestationCiPolicy -Name 'New CI Policy via JEA' -Path 'User:\cipolicy.p7b'

# Confirm it was added successfully
Get-HgsAttestationPolicy -PolicyType CiPolicy

# Finally, remove the PSSession since it is no longer needed
Exit-PSSession
Remove-PSSession -Session $session
```

## <a name="monitoring-hgs"></a>HGS の監視
### <a name="event-sources-and-forwarding"></a>イベントソースと転送
HGS からのイベントは、次の2つのソースの Windows イベントログに表示されます。
- **HostGuardianService-構成証明**
- **HostGuardianService-KeyProtection**

これらのイベントを表示するには、イベントビューアーを開き、HostGuardianService と HostGuardianService の順に移動します。

大規模な環境では、イベントを簡単に分析できるように、中央の Windows イベントコレクターにイベントを転送することをお勧めします。
詳細については、 [Windows イベント転送](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx)に関するドキュメントを参照してください。

### <a name="using-system-center-operations-manager"></a>System Center Operations Manager の使用
System Center 2016-Operations Manager を使用して、HGS と保護されたホストを監視することもできます。
保護されたファブリック管理パックには、データセンターのダウンタイムにつながる可能性がある一般的な構成ミスをチェックするイベントモニターがあります。これには、構成証明を通過しないホストや、エラーを報告する HGS サーバーが含まれます。

まず、 [SCOM 2016 をインストールして構成](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager)し、保護され[たファブリック管理パックをダウンロード](https://www.microsoft.com/download/details.aspx?id=52764)します。
付属の管理パックガイドでは、管理パックを構成し、そのモニタの範囲を理解する方法について説明しています。

## <a name="backing-up-and-restoring-hgs"></a>HGS のバックアップと復元
### <a name="disaster-recovery-planning"></a>ディザスターリカバリーの計画
ディザスターリカバリー計画を作成するときは、保護されたファブリックのホストガーディアンサービスの固有の要件を考慮することが重要です。
HGS ノードの一部またはすべてを紛失した場合、ユーザーがシールドされた Vm を起動できなくなる可能性がある、すぐに可用性の問題が発生する可能性があります。
Hgs クラスター全体が失われるシナリオでは、hgs クラスターを復元して通常の操作を再開するために、HGS 構成の完全なバックアップが必要になります。
このセクションでは、このようなシナリオを準備するために必要な手順について説明します。

まず、HGS のバックアップが重要であることを理解しておくことが重要です。
HGS では、シールドされた Vm の実行を承認されているホストを特定するのに役立ついくつかの情報が保持されます。
たとえば、次のようなアニメーションや効果を作成できます。
1. 信頼されたホストを含むグループのセキュリティ識別子を Active Directory します (Active Directory 構成証明を使用する場合)。
2. 環境内の各ホストの一意の TPM 識別子。
3. ホストの一意の構成ごとの TPM ポリシー。そして
4. ホストで実行を許可するソフトウェアを決定するコード整合性ポリシー。

これらの構成証明アーティファクトは、ホスティングファブリックの管理者と連携してを取得する必要があります。これにより、障害発生後にこの情報を再度取得することが困難になる可能性があります。

さらに、HGS は、シールドされた VM (キープロテクター) を起動するために必要な情報の暗号化と署名に使用する2つ以上の証明書へのアクセスを必要とします。
これらの証明書はよく知られており (シールドされた Vm の所有者が Vm を実行するためにファブリックを承認するために使用されます)、シームレスな回復エクスペリエンスのために障害が発生した後に復元する必要があります。
障害発生後に同じ証明書を使用して HGS を復元しない場合は、各 VM を更新して、情報の暗号化を解除するために新しいキーを承認する必要があります。
セキュリティ上の理由により、vm の所有者のみが VM 構成を更新してこれらの新しいキーを承認できます。つまり、障害発生後にキーを復元しようとすると、各 VM 所有者は vm を再び実行するためのアクションを実行する必要があります。

#### <a name="preparing-for-the-worst"></a>最悪の準備
HGS の完全な損失を準備するには、次の2つの手順を実行する必要があります。
1. HGS 構成証明ポリシーをバックアップする
2. HGS キーをバックアップする

これらの手順を実行する方法については、「 [HGS のバックアップ](#backing-up-hgs)」を参照してください。

また、Active Directory ドメインまたは Active Directory 自体で HGS を管理する権限を持つユーザーの一覧をバックアップすることも推奨されますが、必須ではありません。

情報が最新であり、改ざんや盗難を防ぐために安全に保管されていることを確認するために、バックアップを定期的に作成する必要があります。

HGS ノードのシステムイメージ全体をバックアップしたり復元したりする**ことはお勧めしません**。
クラスター全体が失われた場合、ベストプラクティスは、新しい HGS ノードを設定し、サーバー OS 全体ではなく、HGS 状態のみを復元することです。

#### <a name="recovering-from-the-loss-of-one-node"></a>1つのノードの損失からの復旧
HGS クラスター内の1つまたは複数のノード (すべてのノードではありません) が失われた場合は、展開ガイドのガイダンスに従って、簡単[にクラスターにノードを追加](guarded-fabric-configure-additional-hgs-nodes.md)できます。
構成証明ポリシーは自動的に同期されます。これは、HGS に提供されたすべての証明書が、パスワードが付随する PFX ファイルとして提供されるためです。
拇印を使用して HGS に追加された証明書 (エクスポートできない、ハードウェアによってサポートされる証明書など) については、各新しいノードが各証明書の秘密キーにアクセスできることを確認する必要があります。

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>クラスター全体の損失からの復旧
HGS クラスター全体が停止し、オンラインに戻すことができない場合は、バックアップから HGS を復元する必要があります。
バックアップから HGS を復元する[には、まず、展開ガイドのガイダンスに](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)従って新しい hgs クラスターをセットアップします。
ホストからの名前解決を支援するために、recovery HGS 環境を設定するときに同じクラスター名を使用することを強くお勧めしますが、必須ではありません。
同じ名前を使用すると、新しい構成証明およびキー保護 Url でホストを再構成する必要がなくなります。
オブジェクトを Active Directory ドメインをバッキングする HGS に復元した場合は、hgs サーバーを初期化する前に、HGS クラスター、コンピューター、サービスアカウント、および JEA グループを表すオブジェクトを削除することをお勧めします。

最初の HGS ノード (インストールおよび初期化済みなど) を設定したら、「[バックアップから hgs を復元](#restoring-hgs-from-a-backup)する」の手順に従って、構成証明ポリシーと、キー保護証明書の公開部分を復元します。
証明書プロバイダーのガイダンスに従って、証明書の秘密キーを手動で復元する必要があります (たとえば、Windows で証明書をインポートするか、HSM によってサポートされる証明書へのアクセスを構成します)。
最初のノードがセットアップされたら、必要な容量と回復性に達するまで、[クラスターに追加のノードをインストール](guarded-fabric-configure-additional-hgs-nodes.md)し続けることができます。

### <a name="backing-up-hgs"></a>HGS をバックアップしています
Hgs 管理者は、HGS のバックアップを定期的に行う必要があります。
完全バックアップには、適切に保護する必要がある重要な重要な情報が含まれています。
信頼されていないエンティティがこれらのキーにアクセスできるようになると、シールドされた Vm を危険にさらすために、そのマテリアルを使用して悪意のある HGS 環境をセットアップすることができます。

**構成証明ポリシーのバックアップ**HGS 構成証明ポリシーをバックアップするには、任意の有効な HGS サーバーノードで次のコマンドを実行します。
パスワードを入力するように求められます。
このパスワードは、(証明書の拇印ではなく) PFX ファイルを使用して HGS に追加されたすべての証明書を暗号化するために使用されます。

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> 管理者によって信頼された構成証明を使用している場合は、保護されたホストを承認するために、HGS が使用するセキュリティグループのメンバーシップを個別にバックアップする必要があります。
> HGS では、セキュリティグループの SID のみがバックアップされ、その中のメンバーシップはバックアップされません。
> これらのグループが障害発生時に失われた場合は、グループを再作成し、保護された各ホストを再度追加する必要があります。

**証明書のバックアップ**

`Export-HgsServerState` コマンドは、コマンドの実行時に HGS に追加された PFX ベースの証明書をバックアップします。
拇印を使用して証明書を HGS に追加した場合 (エクスポート可能な証明書とハードウェアベースの証明書の場合は通常)、証明書の秘密キーを手動でバックアップする必要があります。
HGS に登録されていて、手動でバックアップする必要がある証明書を特定するには、任意の有効な HGS サーバーノードで次の PowerShell コマンドを実行します。

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

一覧表示された各証明書について、秘密キーを手動でバックアップする必要があります。
エクスポートできないソフトウェアベースの証明書を使用している場合は、証明機関に連絡して証明書のバックアップがあることを確認するか、必要に応じて再発行する必要があります。
ハードウェアセキュリティモジュールで作成および保存された証明書については、ディザスターリカバリー計画のガイダンスについて、デバイスのドキュメントを参照してください。

証明書のバックアップをセキュリティで保護された場所に保存し、両方の部分をまとめて復元できるようにする必要があります。

**バックアップする追加の構成**

バックアップされた HGS サーバーの状態には、HGS クラスターの名前、Active Directory の情報、または HGS Api との通信をセキュリティで保護するために使用される SSL 証明書は含まれません。
これらの設定は整合性のために重要ですが、障害発生後に HGS クラスターをオンラインに戻すには重要ではありません。

HGS サービスの名前を取得するには、`Get-HgsServer` を実行し、構成証明とキー保護の Url のフラット名をメモします。
たとえば、構成証明 URL が "<http://hgs.contoso.com/Attestation>" の場合、"hgs" は HGS サービス名です。

HGS で使用される Active Directory ドメインは、他の Active Directory ドメインと同様に管理する必要があります。
障害発生後に HGS を復元する場合、現在のドメインに存在するオブジェクトを正確に再作成する必要はありません。
ただし、Active Directory をバックアップして、システムを管理することが許可されている JEA ユーザーの一覧と、保護されたホストを承認するために管理者によって信頼された構成証明によって使用されるセキュリティグループのメンバーシップを維持すると、回復が容易になります。

HGS 用に構成された SSL 証明書の拇印を特定するには、PowerShell で次のコマンドを実行します。
その後、証明書プロバイダーの指示に従って、これらの SSL 証明書をバックアップできます。

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>バックアップからの HGS の復元
次の手順では、バックアップから HGS 設定を復元する方法について説明します。
手順は、既に実行されている HGS インスタンスに対して行われた変更を元に戻す場合と、前回の hgs クラスターが完全に失われた後に新しい HGS クラスターを起動しようとする場合の両方に関連します。

#### <a name="set-up-a-replacement-hgs-cluster"></a>置換される HGS クラスターをセットアップする
HGS を復元する前に、構成を復元できる初期化済みの HGS クラスターが必要です。
既存の (実行中の) クラスターに誤って削除された設定をインポートするだけの場合は、この手順を省略できます。
HGS の完全な損失から回復する場合は、[展開ガイドのガイダンス](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)に従って、少なくとも1つの hgs ノードをインストールし、初期化する必要があります。

具体的には、次のことを行う必要があります。
1. [Hgs ドメインをセットアップ](guarded-fabric-choose-where-to-install-hgs.md)するか、既存のドメインに hgs を参加させます
2. 既存のキー*または*一連の一時キーを使用して[、HGS サーバーを初期化](guarded-fabric-initialize-hgs.md)します。 HGS バックアップファイルから実際のキーをインポートした後[に、一時キーを削除](#renewing-or-replacing-keys)できます。
3. バックアップから[HGS 設定をインポート](#import-settings-from-a-backup)して、信頼されたホストグループ、コード整合性ポリシー、tpm ベースライン、および tpm 識別子を復元します。

> [!TIP]
> 新しい HGS クラスターでは、バックアップファイルのエクスポート元の HGS インスタンスと同じ証明書、サービス名、またはドメインを使用する必要はありません。

#### <a name="import-settings-from-a-backup"></a>バックアップから設定をインポートする

バックアップファイルから、構成証明ポリシー、PFX ベースの証明書、および非 PFX 証明書の公開キーを HGS ノードに復元するには、初期化された HGS サーバーノードで次のコマンドを実行します。
バックアップの作成時に指定したパスワードを入力するように求められます。

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

管理者によって信頼された構成証明ポリシーまたは TPM によって信頼された構成証明ポリシーをインポートするだけの場合は、 [HgsServerState](https://technet.microsoft.com/library/mt652168.aspx)に `-ImportActiveDirectoryModeState` または `-ImportTpmModeState` フラグを指定することによってこれを行うことができます。

`Import-HgsServerState`を実行する前に、Windows Server 2016 用の最新の累積的な更新プログラムがインストールされていることを確認します。
これを行わないと、インポートエラーが発生する可能性があります。

> [!NOTE]
> これらのポリシーのうち1つ以上が既にインストールされている既存の HGS ノードでポリシーを復元すると、インポートコマンドによって重複するポリシーごとにエラーが表示されます。
> これは想定される動作であり、ほとんどの場合、無視しても問題ありません。

#### <a name="reinstall-private-keys-for-certificates"></a>証明書の秘密キーを再インストールする
バックアップの作成元である HGS で使用される証明書のいずれかが、拇印を使用して追加された場合、それらの証明書の公開キーのみがバックアップファイルに含まれます。
つまり、HGS が Hyper-v ホストからの要求を処理できるようにするには、これらの各証明書の秘密キーへのアクセス権を手動でインストールするか、付与する必要があります。
この手順を完了するために必要な操作は、証明書が最初に発行された方法によって異なります。
証明機関によって発行されたソフトウェアベースの証明書については、CA に連絡して秘密キーを取得し、それぞれの手順に従って**各**HGS ノードにインストールする必要があります。
同様に、証明書がハードウェアで保護されている場合は、ハードウェアセキュリティモジュールベンダーのドキュメントを参照して、各 HGS ノードに必要なドライバーをインストールし、HSM に接続し、各コンピューターに秘密キーへのアクセス権を付与する必要があります。

注意して、拇印を使用して HGS に追加した証明書には、各ノードへの秘密キーの手動レプリケーションが必要です。
復元した HGS クラスターに追加する各ノードについて、この手順を繰り返す必要があります。

#### <a name="review-imported-attestation-policies"></a>インポートされた構成証明ポリシーを確認する
バックアップから設定をインポートした後は、`Get-HgsAttestationPolicy` を使用してインポートされたすべてのポリシーを厳密に確認して、シールドされた Vm を実行するために信頼されているホストのみが正常に証明できるようにすることをお勧めします。
セキュリティ体制に一致しなくなったポリシーが見つかった場合は、[無効に](#review-attestation-policies)することも削除することもできます。

#### <a name="run-diagnostics-to-check-system-state"></a>診断を実行してシステム状態を確認する
HGS ノードの状態の設定と復元が完了したら、HGS 診断ツールを実行してシステムの状態を確認する必要があります。
これを行うには、構成を復元した HGS ノードで次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics
```

"全体の結果" が "Pass" でない場合は、システムの構成を完了するために追加の手順が必要になります。
詳細については、subtest に報告されたメッセージを確認してください。

## <a name="patching-hgs"></a>HGS の修正プログラム適用
最新の累積的な更新プログラムをインストールして、ホストガーディアンサービスノードを最新の状態に保つことが重要です。新しい HGS ノードを設定する場合は、HGS の役割をインストールする前、または構成する前に、使用可能な更新プログラムをインストールすることを強くお勧めします。
これにより、新しいまたは変更された機能が直ちに有効になります。

保護されたファブリックに修正プログラムを適用する場合は、まず、 **HGS をアップグレードする前に***すべて*の hyper-v ホストをアップグレードすることを強くお勧めします。
これは、必要な情報を提供するために Hyper-v ホストが更新され*た後*に、hgs の構成証明ポリシーに変更が加えられるようにするためです。
更新によってポリシーの動作が変更された場合、ファブリックの中断を回避するために自動的に有効になることはありません。
このような更新を行うには、次のセクションのガイダンスに従って、新規または変更された構成証明ポリシーをアクティブ化する必要があります。
ポリシーの更新が必要かどうかを確認するために、Windows Server のリリースノートとインストールした累積的な更新プログラムをお読みになることをお勧めします。

### <a name="updates-requiring-policy-activation"></a>ポリシーのアクティブ化が必要な更新プログラム
HGS の更新プログラムによって構成証明ポリシーの動作が導入または大幅に変更された場合は、変更したポリシーをアクティブ化するための追加の手順が必要になります。
ポリシーの変更は、HGS 状態をエクスポートしてインポートした後にのみ実行されます。
新しいポリシーまたは変更されたポリシーは、環境内のすべてのホストとすべての HGS ノードに累積的な更新プログラムを適用した後にのみ、アクティブ化する必要があります。
すべてのコンピューターが更新されたら、任意の HGS ノードで次のコマンドを実行して、アップグレードプロセスを開始します。

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

新しいポリシーが導入された場合、既定では無効になります。
新しいポリシーを有効にするには、最初に Microsoft ポリシーの一覧 ("HGS_" で始まる) を見つけて、次のコマンドを使用して有効にします。

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>構成証明ポリシーの管理
HGS はいくつかの構成証明ポリシーを保持しており、ホストが "健全" と見なされ、シールドされた Vm の実行が許可されるために満たす必要がある最小要件セットを定義します。
これらのポリシーの中には、Microsoft によって定義されているものがあります。また、お客様の環境で許容されるコード整合性ポリシー、TPM ベースライン、およびホストを定義するためにユーザーが追加します。
これらのポリシーを定期的に保守する必要があります。これは、ホストを更新して置き換えるときに、ホストの証明を正常に続行し、信頼されていないホストや構成が正常に証明にブロックされることを保証するために必要です。

管理者によって信頼された構成証明については、ホストが正常かどうかを判断するポリシーが1つだけあります。信頼された既知のセキュリティグループのメンバーシップ。
TPM 構成証明はより複雑であり、システムが正常かどうかを判断する前に、さまざまなポリシーによってシステムのコードと構成が測定されます。

1つの HGS は Active Directory ポリシーと TPM ポリシーの両方で一度に構成できますが、サービスは、ホストが証明を試行したときに構成されている現在のモードのポリシーのみをチェックします。
HGS サーバーのモードを確認するには、`Get-HgsServer`を実行します。

### <a name="default-policies"></a>既定のポリシー
TPM によって信頼された構成証明の場合、HGS にはいくつかの組み込みポリシーが構成されています。
これらのポリシーには、セキュリティ上の理由から無効にできないことを意味する "ロック" があります。
次の表では、各既定のポリシーの目的について説明します。

[ポリシー名]                    | 目的
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | ホストでセキュアブートが有効になっている必要があります。 これは、スタートアップバイナリとその他の UEFI ロック設定を測定するために必要です。
Hgs_UefiDebugDisabled          | ホストでカーネルデバッガーが有効になっていないことを確認します。 ユーザーモードのデバッガーは、コード整合性ポリシーでブロックされます。
Hgs_SecureBootSettings         | ホストが少なくとも1つの (管理者が定義した) TPM ベースラインに一致するようにするためのネガティブポリシー。
Hgs_CiPolicy                   | ホストが管理者によって定義されたいずれかの CI ポリシーを使用していることを確認するためのネガティブポリシー。
Hgs_HypervisorEnforcedCiPolicy | では、ハイパーバイザーによってコード整合性ポリシーが適用される必要があります。 このポリシーを無効にすると、カーネルモードのコード整合性ポリシーの攻撃からの保護が弱くなります。
Hgs_FullBoot                   | ホストがスリープまたは休止状態から再開されていないことを確認します。 このポリシーを成功させるには、ホストを正しく再起動するか、シャットダウンする必要があります。
Hgs_VsmIdkPresent              | では、仮想化ベースのセキュリティがホストで実行されている必要があります。 IDK は、ホストのセキュリティで保護されたメモリ領域に返される情報を暗号化するために必要なキーを表します。
Hgs_PageFileEncryptionEnabled  | では、ホスト上での、の暗号化を必要とします。 このポリシーを無効にすると、テナントシークレットの暗号化されていないページファイルを検査した場合に情報が漏えいする可能性があります。
Hgs_BitLockerEnabled           | では、Hyper-v ホストで BitLocker を有効にする必要があります。 このポリシーは、パフォーマンス上の理由で既定で無効になっているため、有効にしないことをお勧めします。 このポリシーは、シールドされた Vm 自体の暗号化には影響しません。
Hgs_IommuEnabled               | ダイレクトメモリアクセス攻撃を防ぐために、ホストに使用されている IOMMU デバイスが必要です。 このポリシーを無効にし、IOMMU が有効になっていないホストを使用すると、テナント VM シークレットを公開してメモリ攻撃を直接行うことができます。
Hgs_NoHibernation              | Hyper-v ホストで休止状態を無効にする必要があります。 このポリシーを無効にすると、ホストは、シールドされた VM メモリを暗号化されていない休止ファイルに保存することができます。
Hgs_NoDumps                    | では、Hyper-v ホストでメモリダンプを無効にする必要があります。 このポリシーを無効にした場合は、シールドされた VM メモリが暗号化されていないクラッシュダンプファイルに保存されないように、ダンプの暗号化を構成することをお勧めします。
Hgs_DumpEncryption             | では、HGS によって信頼されている暗号化キーを使用して暗号化されるように、Hyper-v ホストで有効になっている場合、メモリダンプが必要です。 このポリシーは、ホストでダンプが有効になっていない場合は適用されません。 このポリシーと*Hgs\_nodumps*の両方が無効になっている場合は、シールドされた VM メモリを暗号化されていないダンプファイルに保存できます。
Hgs_DumpEncryptionKey          | 否定ポリシー。メモリダンプを許可するように構成されたホストが、HGS に知られている管理者定義のダンプファイル暗号化キーを使用していることを確認します。 *Hgs\_DumpEncryption*が無効になっている場合、このポリシーは適用されません。

### <a name="authorizing-new-guarded-hosts"></a>新しい保護されたホストの承認
新しいホストが保護されたホストになることを承認する (たとえば、正常に動作している) 場合、HGS はホストを信頼する必要があり、(TPM に信頼された構成証明を使用するように構成されている場合) そのホストで実行されているソフトウェアを信頼します
新しいホストを承認する手順は、HGS が現在構成されている構成証明モードによって異なります。
保護されたファブリックの構成証明モードを確認するには、任意の HGS ノードで `Get-HgsServer` を実行します。

#### <a name="software-configuration"></a>ソフトウェアの構成
新しい Hyper-v ホストで、Windows Server 2016 Datacenter edition がインストールされていることを確認します。
Windows Server 2016 Standard では、保護されたファブリックでシールドされた Vm を実行することはできません。
ホストがデスクトップエクスペリエンスまたは Server Core にインストールされている可能性があります。

デスクトップエクスペリエンスと Server Core を搭載したサーバーでは、Hyper-v および Host Guardian Hyper-v サポートサーバーの役割をインストールする必要があります。

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>管理者-信頼された構成証明
管理者によって信頼された構成証明を使用するときに新しいホストを HGS に登録するには、最初にホストを参加させるドメインのセキュリティグループに追加する必要があります。
通常、各ドメインには、保護されたホストに対して1つのセキュリティグループがあります。
このグループを HGS で既に登録している場合、実行する必要がある操作は、ホストを再起動してグループのメンバーシップを更新することだけです。

次のコマンドを実行して、HGS によって信頼されているセキュリティグループを確認できます。

```powershell
Get-HgsAttestationHostGroup
```

新しいセキュリティグループを HGS に登録するには、最初にホストのドメイン内のグループのセキュリティ識別子 (SID) をキャプチャし、その SID を HGS に登録します。

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

ホストドメインと HGS の間の信頼を設定する方法については、展開ガイドを参照してください。

#### <a name="tpm-trusted-attestation"></a>TPM-信頼された構成証明
HGS が TPM モードで構成されている場合、ホストは、"Hgs_" で始まるすべてのロックされたポリシーと "有効" ポリシーを、少なくとも1つの TPM ベースライン、TPM 識別子、およびコード整合性ポリシーに渡す必要があります。
新しいホストを追加するたびに、新しい TPM 識別子を HGS に登録する必要があります。
ホストが同じソフトウェア (および同じコード整合性ポリシーが適用されている) を実行していて、TPM ベースラインが環境内の別のホストとして使用されている場合は、新しい CI ポリシーまたはベースラインを追加する必要はありません。

**新しいホストの TPM 識別子を追加する**新しいホストで、次のコマンドを実行して TPM 識別子をキャプチャします。
HGS での検索に役立つ一意のホスト名を指定してください。
この情報は、ホストの使用を停止する場合、または HGS でシールドされた Vm を実行できないようにする場合に必要になります。

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

このファイルを HGS サーバーにコピーし、次のコマンドを実行して、ホストを HGS に登録します。

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**新しい TPM ベースラインの追加**新しいホストで環境の新しいハードウェアまたはファームウェアの構成が実行されている場合は、新しい TPM ベースラインを取得する必要があります。
これを行うには、ホストで次のコマンドを実行します。

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> ホストが検証に失敗し、証明できないというエラーが表示される場合は、心配しないでください。
> これは、ホストがシールドされた Vm を実行できることを確認するための前提条件のチェックです。また、コード整合性ポリシーやその他の必要な設定をまだ適用していないことを意味します。
> エラーメッセージを読み取り、それによって提案された変更を加えてから、再試行してください。
> または、`-SkipValidation` フラグをコマンドに追加して、この時点で検証をスキップすることもできます。

TPM ベースラインを HGS サーバーにコピーし、次のコマンドを使用して登録します。
このクラスの Hyper-v ホストのハードウェアとファームウェアの構成を理解するのに役立つ名前付け規則を使用することをお勧めします。

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**新しいコード整合性ポリシーを追加**するHyper-v ホストで実行されているコード整合性ポリシーを変更した場合は、そのホストが正常に証明できるように、新しいポリシーを HGS に登録する必要があります。
環境内の信頼された Hyper-v コンピューターのマスターイメージとして機能する参照ホストで、`New-CIPolicy` コマンドを使用して新しい CI ポリシーをキャプチャします。
Hyper-v ホストの CI ポリシーには、 **Filepublisher**レベルと**ハッシュ**フォールバックを使用することをお勧めします。
最初に監査モードで CI ポリシーを作成し、すべてが正常に動作していることを確認する必要があります。
システムでサンプルワークロードを検証した後、ポリシーを適用し、強制バージョンを HGS にコピーできます。
コード整合性ポリシーの構成オプションの完全な一覧については、 [Device Guard のドキュメント](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)を参照してください。

```powershell
# Capture a new CI policy with the FilePublisher primary level and Hash fallback and enable user mode code integrity protections
New-CIPolicy -FilePath 'C:\temp\ws2016-hardware01-ci.xml' -Level FilePublisher -Fallback Hash -UserPEs

# Apply the CI policy to the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer

# Check the event log for any untrusted binaries and update the policy if necessary
# Consult the Device Guard documentation for more details

# Change the policy to be in enforced mode
Set-RuleOption -FilePath 'C:\temp\ws2016-hardare01-ci.xml' -Option 3 -Delete

# Apply the enforced CI policy on the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer
```

ポリシーを作成し、テストして、適用したら、バイナリファイル (p7b) を HGS サーバーにコピーし、ポリシーを登録します。

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**メモリダンプの暗号化キーを追加しています**

*Hgs\_NoDumps*ポリシーが無効になっていて、 *Hgs\_dumpencryption*ポリシーが有効になっている場合、保護されたホストは、これらのダンプが暗号化されている限り、メモリダンプ (クラッシュダンプを含む) を有効にすることができます。 保護されたホストは、メモリダンプが無効になっているか、または HGS に知られているキーでそれらを暗号化している場合にのみ、構成証明を渡します。 既定では、HGS にはダンプ暗号化キーが構成されていません。

HGS にダンプ暗号化キーを追加するには、`Add-HgsAttestationDumpPolicy` コマンドレットを使用して、HGS にダンプ暗号化キーのハッシュを指定します。
Dump encryption を使用して構成された Hyper-v ホスト上で TPM ベースラインをキャプチャする場合、ハッシュは tcglog に含まれており、`Add-HgsAttestationDumpPolicy` コマンドレットに提供できます。

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

または、ハッシュの文字列形式をコマンドレットに直接渡すこともできます。

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

保護されたファブリックで異なるキーを使用する場合は、必ず一意のダンプ暗号化キーをそれぞれ HGS に追加してください。
HGS で認識されていないキーを使用してメモリダンプを暗号化しているホストは、構成証明に合格しません。

[ホストでのダンプ暗号化の構成](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)の詳細については、hyper-v のドキュメントを参照してください。

#### <a name="check-if-the-system-passed-attestation"></a>システムが構成証明に合格したかどうかを確認する
必要な情報を HGS に登録した後、ホストが構成証明に合格したかどうかを確認する必要があります。
新しく追加された Hyper-v ホストで `Set-HgsClientConfiguration` を実行し、HGS クラスターの正しい Url を指定します。
これらの Url を取得するには、任意の HGS ノードで `Get-HgsServer` を実行します。

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

結果の状態が "IsHostGuarded: True" を示していない場合は、構成のトラブルシューティングを行う必要があります。
構成証明に失敗したホストで次のコマンドを実行して、失敗した構成証明の解決に役立つ可能性のある問題に関する詳細なレポートを取得します。

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Windows Server 2019 または Windows 10 バージョン1809を使用していて、コード整合性ポリシーを使用している場合、`Get-HgsTrace` によって**コード整合性ポリシーのアクティブ**な診断でエラーが返されることがあります。
> 失敗した診断が唯一の場合は、この結果を無視しても問題ありません。

### <a name="review-attestation-policies"></a>構成証明ポリシーを確認する
HGS で構成されているポリシーの現在の状態を確認するには、任意の HGS ノードで次のコマンドを実行します。

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

セキュリティ要件を満たしていないポリシーが有効になっている場合 (たとえば、unsafe と見なされる古いコード整合性ポリシー)、次のコマンドでポリシーの名前を置き換えて無効にすることができます。

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

同様に、`Enable-HgsAttestationPolicy` を使用してポリシーを再度有効にすることもできます。

ポリシーが不要になり、すべての HGS ノードから削除する場合は、`Remove-HgsAttestationPolicy -Name 'PolicyName'` を実行してポリシーを完全に削除します。

## <a name="changing-attestation-modes"></a>構成証明モードの変更
管理者によって信頼された構成証明を使用して保護されたファブリックを開始した場合、環境内で TPM 2.0 互換のホストが十分になるとすぐに、より強力な TPM 構成証明モードにアップグレードすることをお勧めします。
切り替える準備ができたら、管理者によって信頼された構成証明を使用して HGS を実行し続けながら、HGS のすべての構成証明アイテム (CI ポリシー、TPM ベースライン、TPM 識別子) を事前に読み込むことができます。
これを行うには、「[新しい保護されたホストの承認](#authorizing-new-guarded-hosts)」セクションの手順に従います。

すべてのポリシーを HGS に追加したら、次の手順では、ホストで合成構成証明を実行して、TPM モードで構成証明書に合格するかどうかを確認します。
これは、HGS の現在の動作状態には影響しません。
次のコマンドは、環境内のすべてのホストと1つ以上の HGS ノードにアクセスできるコンピューターで実行する必要があります。
ファイアウォールまたはその他のセキュリティポリシーによってこれが妨げられる場合は、この手順を省略できます。
可能であれば、統合構成証明を実行して、TPM モードに "切り替える" ことで Vm のダウンタイムが発生するかどうかを適切に示すことをお勧めします。 

```powershell
# Get information for each host in your environment
$hostNames = 'host01.contoso.com', 'host02.contoso.com', 'host03.contoso.com'
$credential = Get-Credential -Message 'Enter a credential with admin privileges on each host'
$targets = @()
$hostNames | ForEach-Object { $targets += New-HgsTraceTarget -Credential $credential -Role GuardedHost -HostName $_ }

$hgsCredential = Get-Credential -Message 'Enter an admin credential for HGS'
$targets += New-HgsTraceTarget -Credential $hgsCredential -Role HostGuardianService -HostName 'HGS01.bastion.local'

# Initiate the synthetic attestation attempt
Get-HgsTrace -RunDiagnostics -Target $targets -Diagnostic GuardedFabricTpmMode 
```

診断が完了したら、出力された情報を確認して、どのホストも TPM モードで構成に失敗したかどうかを判断します。
各ホストから "pass" を取得するまで診断を再実行してから、HGS を TPM モードに変更します。

**TPM モードに変更**するには、次の手順を完了する必要があります。
任意の HGS ノードで次のコマンドを実行して、構成証明モードを更新します。

```powershell
Set-HgsServer -TrustTpm
```

問題が発生し、Active Directory モードに切り替える必要がある場合は、`Set-HgsServer -TrustActiveDirectory`を実行して実行できます。

すべてが正常に動作していることを確認したら、すべての信頼された Active Directory ホストグループを HGS から削除し、HGS ドメインとファブリックドメイン間の信頼を削除する必要があります。
Active Directory の信頼を設定したままにした場合は、他のユーザーが信頼を再度有効にし、HGS を Active Directory モードに切り替えるリスクがあります。これにより、保護されたホストで信頼されていないコードを実行できなくなる可能性があります。

## <a name="key-management"></a>キーの管理
保護されたファブリックソリューションでは、複数の公開キーと秘密キーのペアを使用して、ソリューション内のさまざまなコンポーネントの整合性を検証し、テナントシークレットを暗号化します。
ホストガーディアンサービスは、シールドされた Vm を起動するために使用されるキーの署名と暗号化に使用される、少なくとも2つの証明書 (公開キーと秘密キー) を使用して構成されています。
これらのキーは慎重に管理する必要があります。
秘密キーが敵対者によって獲得されると、ファブリックで実行されているすべての Vm のシールドを解除したり、なりすまし HGS クラスターを設定して、その場で保護された構成を回避することができます。
障害発生時に秘密キーが失われ、バックアップに見つからない場合は、新しいキーペアを設定し、新しい証明書を承認するために各 VM を再キーする必要があります。

このセクションでは、キーを構成して機能とセキュリティを確保するための一般的なキー管理のトピックについて説明します。

### <a name="adding-new-keys"></a>新しいキーの追加
HGS は1セットのキーで初期化する必要がありますが、複数の暗号化と署名キーを HGS に追加することができます。
HGS に新しいキーを追加する最も一般的な理由は、次の2つです。
1. テナントが自分の秘密キーをハードウェアセキュリティモジュールにコピーし、そのキーを承認してシールドされた Vm を起動するような、"独自のキーを持ち込む" シナリオをサポートする。
2. HGS の既存のキーを置き換えるには、最初に新しいキーを追加し、各 VM 構成が新しいキーを使用するように更新されるまで、両方のキーセットを保持します。

新しいキーを追加するプロセスは、使用している証明書の種類によって異なります。

**オプション 1: HSM に格納されている証明書を追加する**

HGS キーを保護するための推奨される方法は、ハードウェアセキュリティモジュール (HSM) で作成された証明書を使用することです。
Hsm は、データセンター内のセキュリティを重視するデバイスへの物理的なアクセスに、キーの使用を確実にします。
各 HSM は異なり、証明書を作成して HGS に登録するための固有のプロセスがあります。
以下の手順は、HSM でサポートされる証明書を使用するための大まかなガイダンスを提供することを目的としています。
正確な手順と機能については、HSM ベンダーのドキュメントを参照してください。

1. クラスター内の各 HGS ノードに HSM ソフトウェアをインストールします。 ネットワークまたはローカルの HSM デバイスがあるかどうかに応じて、そのキーストアへのアクセス権をコンピューターに付与するように HSM を構成する必要がある場合があります。
2. 暗号化と署名のために**2048 ビット RSA キー**を使用して、HSM に2つの証明書を作成します。
    1. HSM で**データ**暗号化キー使用法プロパティを使用して暗号化証明書を作成する
    2. HSM で**デジタル署名**キー使用法プロパティを使用して署名証明書を作成する
3. HSM ベンダーのガイダンスに従って、各 HGS ノードのローカル証明書ストアに証明書をインストールします。
4. HSM で詳細なアクセス許可を使用して、特定のアプリケーションまたはユーザーに秘密キーを使用するアクセス許可を付与する場合は、HGS グループの管理されたサービスアカウントに証明書へのアクセス権を付与する必要があります。 を実行すると、HGS gMSA アカウントの名前を確認でき `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
5. 次のコマンドで、署名証明書と暗号化証明書を HGS に追加します。このとき、拇印を証明書のものに置き換えます。

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**オプション 2: エクスポートできないソフトウェア証明書の追加**

会社または公共の証明機関によって発行されたソフトウェアベースの証明書がある場合は、その拇印を使用して HGS に証明書を追加する必要があります。
1. 証明機関の指示に従って、コンピューターに証明書をインストールします。
2. HGS グループの管理されたサービスアカウントに、証明書の秘密キーへの読み取りアクセスを許可します。 を実行すると、HGS gMSA アカウントの名前を確認でき `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
3. 次のコマンドを使用して HGS に証明書を登録し、証明書の拇印に置き換えます (署名証明書の*署名*に*暗号化*を変更します)。

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> 秘密キーを手動でインストールし、各 HGS ノードの gMSA アカウントに読み取りアクセス権を付与する必要があります。
> HGS は、拇印によって登録され*た証明書*の秘密キーを自動的にレプリケートすることはできません。

**オプション 3: PFX ファイルに格納されている証明書を追加する**

ソフトウェアで保護された証明書を、PFX ファイル形式で保存してパスワードで保護することができる、エクスポート可能な秘密キーを持っている場合、HGS は証明書を自動的に管理することができます。
PFX ファイルで追加された証明書は、HGS クラスターのすべてのノードに自動的にレプリケートされ、HGS は秘密キーへのアクセスをセキュリティで保護します。
PFX ファイルを使用して新しい証明書を追加するには、任意の HGS ノードで次のコマンドを実行します (署名証明書の*署名*に*暗号化*を変更します)。

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**プライマリ証明書の識別と変更**HGS は複数の署名証明書と暗号化証明書をサポートできますが、"プライマリ" 証明書として1つのペアを使用します。
これらは、他のユーザーがその HGS クラスターのガーディアンメタデータをダウンロードするときに使用される証明書です。
現在プライマリ証明書としてマークされている証明書を確認するには、次のコマンドを実行します。

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

新しいプライマリ暗号化証明書または署名証明書を設定するには、次のコマンドを使用して、目的の証明書の拇印を検索し、プライマリとしてマークします。

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>キーの更新または置換
HGS によって使用される証明書を作成すると、証明機関のポリシーと要求情報に従って証明書の有効期限が割り当てられます。
通常、証明書の有効性が HTTP 通信のセキュリティ保護などの重要なシナリオでは、サービスの中断または気がかりエラーメッセージを回避するために、証明書を期限切れにする前に更新する必要があります。
HGS は、その意味では証明書を使用しません。
HGS は、非対称キーペアを作成して格納するための便利な方法として、単に証明書を使用します。
HGS の有効期限が切れた暗号化または署名証明書は、シールドされた Vm の脆弱性または保護の損失を示していません。
さらに、HGS では証明書の失効確認は実行されません。
HGS 証明書または発行機関の証明書が失効している場合は、HGS の証明書の使用に影響しません。

HGS 証明書について心配する必要があるのは、秘密キーが盗まれたと思われる理由がある場合のみです。
この場合、HGS 暗号化と署名キーのペアのプライベートな半分を所有していると、VM のシールド保護を削除したり、構成証明ポリシーが弱い HGS サーバーを立ち上げたりするので、シールドされた Vm の整合性は危険にさらされます。

証明書キーを定期的に更新するために、そのような状況が発生した場合、または準拠基準によって要求された場合は、次の手順に従って、HGS サーバーのキーを変更するプロセスの概要を確認してください。
次のガイダンスは、HGS クラスターによって提供される各 VM へのサービスの中断につながる重要な作業を示しています。
サービスの中断を最小限に抑え、テナント Vm のセキュリティを確保するために、HGS キーの変更を適切に計画する必要があります。

HGS ノードで、次の手順を実行して、新しい暗号化証明書と署名証明書のペアを登録します。
新しいキーを HGS に追加するさまざまな方法の詳細については、[新しいキーの追加](#adding-new-keys)に関するセクションを参照してください。
1. HGS サーバーの新しい暗号化証明書と署名証明書のペアを作成します。 これらは、ハードウェアセキュリティモジュールで作成するのが理想的です。
2. **HgsKeyProtectionCertificate**を使用して新しい暗号化証明書と署名証明書を登録する

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. 拇印を使用した場合は、クラスター内の各ノードにアクセスして秘密キーをインストールし、HGS gMSA にキーへのアクセスを許可する必要があります。
4. 新しい証明書を HGS の既定の証明書にする

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

この時点で、HGS ノードから取得したメタデータで作成されたシールドデータは新しい証明書を使用しますが、古い証明書がまだ存在するため、既存の Vm は引き続き動作します。
すべての既存の Vm が新しいキーで動作するようにするには、各 VM でキープロテクターを更新する必要があります。
これは、関連する VM 所有者 ("所有者" ガーディアンを所有しているユーザーまたはエンティティ) を必要とするアクションです。
シールドされた VM ごとに、次の手順を実行します。
5. VM をシャットダウンします。 残りの手順が完了するまで VM を再び有効にすることはできません。それ以外の場合は、もう一度プロセスを開始する必要があります。
6. 現在のキー保護機能をファイルに保存します。 `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. KP を VM 所有者に転送する
8. 所有者が更新されたガーディアン情報を HGS からダウンロードし、ローカルシステムにインポートする
9. 現在の KP をメモリに読み取り、新しいガーディアンに KP へのアクセスを許可し、次のコマンドを実行して新しいファイルに保存します。

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. 更新された KP をホストしているファブリックにコピーします。
11. KP を元の VM に適用します。

   ```powershell
   $updatedKP = Get-Content -Path .\updatedVM001.kp
   Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
   ```
12. 最後に、VM を起動し、正常に動作することを確認します。

> [!NOTE]
> Vm の所有者が vm で正しくないキープロテクターを設定し、VM を実行するためにファブリックを承認していない場合、シールドされた VM を起動することはできません。
> 前回正常起動時のキー保護機能に戻るには、を実行し `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`

すべての Vm を更新して新しいガーディアンキーを承認したら、古いキーを無効にして削除することができます。

13. 以前の証明書の拇印を取得 `Get-HgsKeyProtectionCertificate -IsPrimary $false`

14. 次のコマンドを実行して、各証明書を無効にします。  

   ```powershell
   Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
   Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
   ```

15. 証明書を無効にして Vm が引き続き開始できることを確認した後、次のコマンドを実行して、HGS から証明書を削除します。

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM のバックアップには、古い証明書を使用して VM を起動できるようにする古いキープロテクター情報が含まれます。
> 秘密キーが侵害されたことがわかっている場合は、VM のバックアップも侵害される可能性があることを前提として、適切な操作を行う必要があります。
> VM 構成をバックアップ (vmcx) から破棄すると、キープロテクターが削除されます。 BitLocker 回復パスワードを使用して次回 VM を起動することが必要になります。

### <a name="key-replication-between-nodes"></a>ノード間のキーレプリケーション
HGS クラスター内のすべてのノードは、SSL 証明書と同じ暗号化、署名、および (構成されている場合) 構成されている必要があります。
これは、Hyper-v ホストがクラスター内の任意のノードに到達するために、要求が正常に処理されるようにするために必要です。

**PFX ベースの証明書を使用して hgs サーバーを初期化した場合**、hgs はクラスター内のすべてのノード間でこれらの証明書の公開キーと秘密キーの両方を自動的にレプリケートします。
キーを追加する必要があるのは、1つのノードだけです。

証明書の参照または拇印を**使用して hgs サーバーを初期化した場合**、hgs は証明書の*公開*キーのみを各ノードにレプリケートします。
さらに、HGS は、このシナリオのどのノードでも秘密キーへのアクセスを許可することはできません。
そのため、次のことを行う必要があります。
1. 各 HGS ノードに秘密キーをインストールする
2. HGS グループの管理されたサービスアカウント (gMSA) に、各ノードの秘密キーへのアクセス権を付与します。これらのタスクは、余分な運用負荷を追加します。ただし、HSM ベースのキーと、エクスポートできない秘密キーを持つ証明書には必要です。

**SSL 証明書**はどのような形式でもレプリケートされません。
同じ SSL 証明書を使用して各 HGS サーバーを初期化し、SSL 証明書の更新または置換を選択するたびに各サーバーを更新する必要があります。
SSL 証明書を置き換えるときは、 [HgsServer](https://technet.microsoft.com/library/mt652180.aspx)コマンドレットを使用することをお勧めします。

## <a name="unconfiguring-hgs"></a>HGS の解除

HGS サーバーを使用停止または大幅に再構成する必要がある場合は、 [HgsServer](https://technet.microsoft.com/library/mt652176.aspx)または[HgsServer](https://technet.microsoft.com/library/mt652182.aspx)コマンドレットを使用して実行できます。

### <a name="clearing-the-hgs-configuration"></a>HGS 構成をクリアしています

HGS クラスターからノードを削除するには、 [HgsServer](https://technet.microsoft.com/library/mt652176.aspx)コマンドレットを使用します。
このコマンドレットは、実行されるサーバーで次の変更を行います。

- 構成証明とキー保護サービスの登録を解除します
- "Microsoft. windows" JEA 管理エンドポイントを削除します。
- ローカルコンピューターを HGS フェールオーバークラスターから削除します。

サーバーがクラスター内の最後の HGS ノードである場合は、クラスターとそれに対応する分散ネットワーク名リソースも破棄されます。

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

クリア操作が完了したら、 [HgsServer](https://technet.microsoft.com/library/mt652185.aspx)を使用して HGS サーバーを再初期化できます。
[HgsServer](https://technet.microsoft.com/library/mt652169.aspx)を使用して Active Directory Domain Services ドメインを設定した場合、そのドメインは、消去操作後も構成され、操作可能な状態のままになります。

### <a name="uninstalling-hgs"></a>HGS のアンインストール

HGS クラスターからノードを削除**し**、そのノードで実行されている Active Directory ドメインコントローラーを降格する場合は、 [HgsServer](https://technet.microsoft.com/library/mt652182.aspx)コマンドレットを使用します。
このコマンドレットは、実行されるサーバーで次の変更を行います。

- 構成証明とキー保護サービスの登録を解除します
- "Microsoft. windows" JEA 管理エンドポイントを削除します。
- ローカルコンピューターを HGS フェールオーバークラスターから削除します。
- Active Directory ドメインコントローラーを降格します (構成されている場合)

サーバーがクラスター内の最後の HGS ノードである場合、ドメイン、フェールオーバークラスター、およびクラスターの分散ネットワーク名リソースも破棄されます。

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

アンインストール操作が完了し、コンピューターが再起動されたら、 [HgsServer](https://technet.microsoft.com/library/mt652169.aspx)を使用して addc と hgs を再インストールするか、コンピューターをドメインに参加させて、 [HgsServer](https://technet.microsoft.com/library/mt652185.aspx)を使用してそのドメインの hgs サーバーを初期化します。

コンピューターを HGS ノードとして使用する予定がなくなった場合は、Windows から役割を削除できます。

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
