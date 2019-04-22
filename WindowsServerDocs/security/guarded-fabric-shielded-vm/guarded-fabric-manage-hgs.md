---
title: ホスト ガーディアン サービスの管理
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: ed3a3d4c5d0e55126f4dae8ecaf0ba1f32e46317
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820223"
---
# <a name="managing-the-host-guardian-service"></a>ホスト ガーディアン サービスの管理

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト ガーディアン サービス (HGS) は、保護されたファブリック ソリューションの中心的な場所です。
ファブリックで HYPER-V ホストがホスト側またはエンタープライズに既知であることを確認および信頼されているソフトウェアを実行するため、シールドされた Vm の起動に使用されるキーを管理するために行います。
テナントは、信頼、シールドされた Vm をホストすることを決定したらの構成と、ホスト ガーディアン サービスの管理での信頼を配置します。
そのため、セキュリティ、可用性と、保護されたファブリックの信頼性を確保する、ホスト ガーディアン サービスを管理するときのベスト プラクティスに従う非常に重要ですが。
次のセクションのガイダンスは、HGS の管理者が直面している最も一般的な運用上の問題に対処します。

## <a name="limiting-admin-access-to-hgs"></a>HGS に管理者のアクセスを制限します。
HGS のセキュリティの重要な性質、により、その管理者が組織のメンバーを信頼性の高いされ、理想的には、ファブリックのリソースの管理者から分離する重要なは。
さらに、HTTPS 経由の WinRM などのセキュリティで保護された通信プロトコルを使用してセキュリティで保護されたワークステーションからのみ HGS を管理することをお勧めします。

### <a name="separation-of-duties"></a>職務の分離
HGS を設定する場合は、HGS 用または HGS を既存の信頼されたドメインに参加させるのには、分離の Active Directory フォレストを作成するオプションが表示されます。
管理者を割り当てるには、組織内のロールと同様に、この決定は、HGS の信頼の境界を決定します。
管理者として直接または間接的に別のもの (例: Active Directory) の管理者は、HGS に影響を与えることができるかどうか、HGS へのアクセスを持つすべてのユーザーは、保護されたファブリック制御できます。
HGS 管理者は、シールドされた Vm を実行して、シールドされた Vm の起動に必要な証明書を管理する権限が、HYPER-V ホストを選択します。
攻撃者や悪意のある管理者 HGS にアクセスできるユーザーは、シールドされた Vm を実行するには、サービス拒否攻撃を開始し、キー マテリアルを削除することによってセキュリティを侵害されたホストを承認するために、この power を使用できます。

このリスクを避けるためには、*強く*(HGS が参加しているドメインを含む)、HGS の管理者の間の重複を制限することをお勧めしますと、HYPER-V 環境。
1 つの管理者がいませんが両方のシステムへのアクセスにより、攻撃者は、HGS ポリシーの変更を彼の任務を完了する 2 つの個別ユーザーからの 2 つの異なるアカウントを侵害する必要があります。
これは、2 つの Active Directory 環境のドメインとエンタープライズ管理者が同一人物をすることはできませんもない必要があります HGS を使用して、同じ Active Directory フォレスト、HYPER-V ホストとしてことも意味します。
すべてのユーザーより多くのリソースへのアクセスを自分自身に付与できますが、セキュリティ リスクが生じます。

### <a name="using-just-enough-administration"></a>Just Enough Administration を使用します。
HGS が付属して[Just Enough Administration](https://aka.ms/JEAdocs) (JEA) の役割より安全に管理するために組み込まれています。
JEA では、HGS ポリシーを管理する担当者がコンピューター全体またはドメインの管理者を実際にはない必要がありますので、管理者以外のユーザーに管理者のタスクを委任できるため、役立ちます。
JEA は、どのようなコマンドを PowerShell セッションで実行できるユーザーを制限して、通常の昇格を必要とするコマンドを実行するバック グラウンドで (一意のユーザー セッションごとに) 一時的なローカル アカウントを使用してによって機能します。

HGS では、構成済みの 2 つの JEA ロールが付属しています。
- **HGS 管理者**シールドされた Vm のユーザーは認証を実行する新しいホストを含め、すべての HGS ポリシーを管理できます。
- **HGS のレビュー担当者**のみのできるユーザーの既存のポリシーを監査する権限。 変更を加えます HGS の構成にすることはできません。

JEA を使用するには、まず、新しい標準ユーザーを作成し、HGS 管理者または HGS レビュー担当者のグループのメンバーにすることを必要があります。
使用した場合`Install-HgsServer`HGS の新しいフォレストを設定するにこれらのグループの名前は"*servicename*管理者"と"*servicename*レビュー担当者"をそれぞれ、 *servicename* HGS クラスターのネットワーク名を指定します。
HGS を既存のドメインに参加した場合に指定したグループ名を参照してください`Initialize-HgsServer`します。

**HGS 管理者とレビュー担当者の役割の標準ユーザーを作成します。**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**レビュー担当者の役割を持つ監査ポリシー**

HGS にネットワーク接続されているリモート コンピューター上には、レビュー担当者の資格情報を使って JEA セッションを入力する PowerShell で次のコマンドを実行します。
レビュー担当者のアカウントは、標準のユーザーだけであるため、使用できないこと正規の Windows PowerShell リモート処理、HGS などへのリモート デスクトップ アクセス用に注意してください。 重要です。

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

セッションでコマンドが許可されているを確認することができますし、`Get-Command`し、構成を監査する、許可されているコマンドを実行します。
次の例を確認しています HGS でどのポリシーが有効にします。

```powershell
Get-Command

Get-HgsAttestationPolicy
```

コマンドを入力`Exit-PSSession`またはそのエイリアスで`exit`が済んだら、JEA セッションを使用します。 

**HGS 管理者の役割を使用する新しいポリシーを追加します。**

実際には、ポリシーを変更するには、'hgsAdministrators' グループに属している、id を持つ JEA エンドポイントに接続する必要があります。
次の例を紹介 HGS に新しいコード整合性ポリシーをコピーし、JEA を使用して登録する方法。
構文を使用している異なる可能性があります。
これは、完全なファイル システムにアクセスできないように JEA の制限の一部に対応します。

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
### <a name="event-sources-and-forwarding"></a>イベント ソースと転送
HGS からのイベントが表示されます、Windows イベント ログの 2 つのソース。
- **HostGuardianService-Attestation**
- **HostGuardianService-KeyProtection**

これらのイベントは、イベント ビューアを開くと、Microsoft Windows HostGuardianService 証明と Microsoft Windows HostGuardianService KeyProtection に移動して表示できます。

大規模な環境でのイベントの分析を簡単にサーバーの全体の Windows イベント コレクターにイベントを転送することをお勧めは多くの場合。
詳細については、チェック アウト、[ドキュメントの Windows イベント転送](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx)します。

### <a name="using-system-center-operations-manager"></a>System Center Operations Manager の使用
また、HGS と保護されたホストを監視する Operations Manager、System Center 2016 - を使用することもできます。
保護されたファブリックの管理パックには、ホストの構成証明と HGS サーバーがエラーの報告を渡していないなど、データ センターのダウンタイムを招く可能性のある一般的な構成ミスをチェックするイベントのモニターがあります。

最初に、[のインストールし、構成の SCOM 2016](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager)と[保護されたファブリックの管理パックをダウンロード](https://www.microsoft.com/download/details.aspx?id=52764)します。
含まれる管理パック ガイドには、管理パックを構成し、そのモニターのスコープを理解する方法について説明します。

## <a name="backing-up-and-restoring-hgs"></a>バックアップと復元の HGS
### <a name="disaster-recovery-planning"></a>ディザスター リカバリー計画
ドラフト、ディザスター リカバリー計画を作成、それが、保護されたファブリック ホスト ガーディアン サービスの一意の要件を考慮する重要です。
HGS ノードの一部またはすべてをなくした場合、ユーザーが、シールドされた Vm を起動するを妨げるは即時可用性問題に直面する可能性があります。
HGS クラスター全体を紛失した場合は HGS クラスターを復元し、通常の操作を再開する一方で、HGS の構成の完全なバックアップを作成する必要があります。
このセクションでは、このようなシナリオの準備に必要な手順について説明します。

まず、HGS がバックアップに重要なのかを理解しておく必要が。
HGS 保持いくつかののに役立つ情報を決定するホストがシールドされた Vm を実行する権限が。
たとえば、次のようなアニメーションや効果を作成できます。
1. 含むグループの active Directory セキュリティ識別子 (Active Directory の構成証明を使用) する場合のホストを信頼します。
2. TPM の一意の識別子、環境内の各ホストを
3. 各ホストの一意の構成の TPM ポリシーそして
4. コード整合性ポリシーをホストで実行する必要のあるソフトウェアが許可されているかを決定します。

これらの構成証明の成果物には、可能性のある困難災害後にもう一度この情報を取得するのには、ホスティング ファブリック内の管理者と調整が必要です。

さらに、HGS では、暗号化し、シールドされた VM (キー保護機能) の起動に必要な情報の署名に使用される 2 つ以上の証明書へのアクセスが必要です。
これらの証明書は、よく知られています (シールドされた Vm の所有者が各自の Vm を実行するファブリックを承認するために使用) と、エクスペリエンスをシームレスに回復の障害発生後に復元する必要があります。
各 VM は復元しないでくださいする HGS は同じ証明書で、障害発生後、その情報を復号化する、新しいキーを承認するために更新する必要は。
セキュリティ上の理由から、VM 所有者のみがこれらの新しいキーの各自の Vm を再実行を取得するアクションを実行する必要がある各 VM 所有者に障害が発生した後、キーの復元に失敗する意味を承認するために、VM 構成を更新できます。

#### <a name="preparing-for-the-worst"></a>最悪の事態に備える
HGS の完全な損失を防ぐを準備するには、2 つの手順を行う必要がありますがあります。
1. HGS 構成証明書のポリシーをバックアップします。
2. HGS キーをバックアップします。

これらの手順を実行する方法に関するガイダンスが提供される、 [HGS バックアップ](#backing-up-hgs)セクション。

さらに、お勧めですが必須ではありません、Active Directory ドメインでの HGS または Active Directory 自体を管理する権限を持つユーザーの一覧をバックアップすること。

バックアップを定期的に実行する情報が最新の状態および改ざんや盗難を避けるために安全に格納されていることを確認する必要があります。

**しないで**をバックアップまたは HGS ノードのシステム全体のイメージを復元しようとしています。
クラスター全体を紛失した場合に、HGS のまったく新しいノードを設定およびだけ HGS 状態全体のサーバー OS いないを復元することをお勧めします。

#### <a name="recovering-from-the-loss-of-one-node"></a>1 つのノードの損失からの回復
単に HGS クラスターで 1 つまたは複数のノード (ただし、すべてのノード) を紛失した場合は[、クラスターにノードを追加](guarded-fabric-configure-additional-hgs-nodes.md)『 展開ガイド」のガイダンスに従っています。
構成証明書ポリシーは、パスワードを伴う HGS を PFX ファイルとして提供されたすべての証明書が自動的に同期されます。
証明書の拇印を使用して HGS に追加 (エクスポートできないハードウェアを基盤に証明書をよくと)、新しい各ノードが各証明書の秘密キーにアクセスすることを確認する必要があります。

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>クラスター全体の損失からの回復
HGS クラスター全体がダウンしたにオンラインに戻すをできない場合は、HGS をバックアップから復元する必要があります。
新しい HGS クラスターあたりの最初の設定は、HGS をバックアップから復元する、[展開ガイド」のガイダンス](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)します。
を強くお勧めしますが、ホストからの名前解決を支援するために、回復 HGS 環境をセットアップするときに、同じクラスター名を使用する必要ありません。
同じ名前を使用するには、新しい構成証明およびキーの保護の Url のホストを再構成することが回避できます。
HGS をバックアップする Active Directory ドメインにオブジェクトを復元した場合は、HGS サーバーを初期化する前に、HGS クラスター、コンピューター、サービス アカウントおよび JEA のグループを表すオブジェクトを削除することをお勧めします。

最初、HGS ノードを設定すると (例: これをインストールして初期化されます)、下の手順に従います[バックアップから復元 HGS](#restoring-hgs-from-a-backup)構成証明書ポリシーとキーの保護のパブリック部分を復元するには証明書。
証明書プロバイダーのガイダンスに従って手動で証明書の秘密キーを復元する必要があります (例:、Windows で証明書をインポートまたは HSM を基盤と証明書へのアクセスを構成する)。
最初のノードを設定した後に進んで[追加ノードをクラスターにインストール](guarded-fabric-configure-additional-hgs-nodes.md)容量と回復性の目的に到達するまで。

### <a name="backing-up-hgs"></a>HGS のバックアップ
HGS 管理者は、HGS の定期的にバックアップを担当する必要があります。
完全なバックアップでは、適切に保護する必要が機密のキー マテリアルが格納されます。
信頼されていないエンティティがこれらのキーへのアクセスを得る必要があります、シールドされた Vm を侵害するために悪意のある HGS 環境を設定するマテリアルを使用することができます。

**構成証明書ポリシーをバックアップする**戻る HGS の構成証明書ポリシーをどの作業 HGS サーバー ノードで、次のコマンドを実行します。
パスワードの入力を求めるメッセージが表示されます。
このパスワードは、すべての証明書は、HGS (証明書の拇印) ではなく、PFX ファイルを使用する追加の暗号化に使用されます。

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> 管理者によって信頼された構成証明を使用している場合は、個別に HGS によって保護されたホストを承認するために使用されるセキュリティ グループのメンバーシップをバックアップする必要があります。
> HGS では、セキュリティ グループの SID をそれらに含まれるグループのみがバックアップされます。
> 障害時にこれらのグループが失われた場合に、グループを再作成し、それらに保護された各ホストを再度追加する必要があります。

**証明書のバックアップ**

`Export-HgsServerState`コマンドは、PFX に基づく証明書をバックアップ時点での HGS に追加コマンドを実行します。
HGS に証明書を追加した場合 (エクスポートできないとハードウェアを基盤と証明書の一般的な) の拇印を使用する必要があります証明書の秘密キーを手動でバックアップします。
証明書が HGS に登録されているしを手動でバックアップする必要がありますを識別するには、どの作業 HGS サーバー ノードで次の PowerShell コマンドを実行します。

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

表示されている証明書ごとに、秘密キーを手動でバックアップする必要があります。
エクスポートできないのソフトウェア ベースの証明書を使用している場合、証明書のバックアップやオンデマンドに再発行できることを確認する証明機関に問い合わせてください。
証明書の作成し、ハードウェア セキュリティ モジュールに格納されている場合は、ディザスター リカバリー計画に関するガイダンスについては、デバイスのマニュアルを参照する必要があります。

両方の部分を一緒に復元できるように、安全な場所に、構成証明書ポリシーのバックアップと共に証明書のバックアップを格納する必要があります。

**追加の構成をバックアップするには**

バックアップされたサーバーの状態が、Active Directory からの情報、HGS のクラスターの名前を含めないで HGS をまたは HGS Api との通信をセキュリティで保護する SSL 証明書を使用します。
これらの設定とは、一貫性を保つのために重要ですが、障害発生後の HGS のクラスターをオンラインに戻すの取得に重要でないです。

HGS のサービスの名前をキャプチャするには、次のように実行します。`Get-HgsServer`し、構成証明とキー保護の Url でフラットな名前をメモします。
たとえば、次の構成証明 URL は"http://hgs.contoso.com/Attestation"、"hgs"は、HGS サービス名。

その他の Active Directory ドメインのように HGS によって使用される Active Directory ドメインを管理する必要があります。
HGS を復元するには、障害発生後、必要はありません必ずしもを現在のドメインに存在する厳密なオブジェクトを再作成します。
ただし、Active Directory をバックアップし、管理者によって信頼された構成証明書によって保護されたホストを承認するために使用するすべてのセキュリティ グループのメンバーシップだけでなく、システム管理権限を持つ JEA ユーザーの一覧を保持する場合は、回復が容易にされます。

HGS 用に構成された SSL 証明書の拇印を識別するためには、PowerShell で次のコマンドを実行します。
証明書プロバイダーの指示に従ってこれらの SSL 証明書をバックアップできます。

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>HGS をバックアップから復元します。
次の手順では、HGS 設定をバックアップから復元する方法について説明します。
手順は、関連して、前の 1 つの完全な喪失後にまったく新しい HGS クラスターを構築するときに、既に実行中の HGS のインスタンスに加えられた変更を元に戻す先の両方の場合。

#### <a name="set-up-a-replacement-hgs-cluster"></a>置換 HGS クラスターを設定します。
HGS を復元するには、初期化された HGS クラスター構成を戻すことができますがある必要があります。
既存の (実行中) クラスターに誤って削除された設定を単にインポートする場合は、この手順をスキップすることができます。
HGS の完全な損失から回復する場合は、インストールおよび少なくとも 1 つの HGS ノード以下を初期化する必要があります、[展開ガイド」のガイダンス](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)します。

具体的には、する必要があります。
1. [HGS ドメイン設定](guarded-fabric-choose-where-to-install-hgs.md)も HGS を既存のドメインに参加させる
2. [HGS サーバーの初期化](guarded-fabric-initialize-hgs.md)既存のキーを使用して*または*一時キーのセット。 できます[一時キーの削除](#renewing-or-replacing-keys)HGS から、実際のキーをインポートした後、ファイルをバックアップします。
3. [HGS 設定をインポート](#import-settings-from-a-backup)信頼されたホスト グループ、コード整合性ポリシー、TPM の基準、および TPM の識別子を復元するバックアップから

> [!TIP]
> 新しい HGS クラスターは、バックアップ ファイルのエクスポート元の HGS インスタンスとして同じ証明書、サービス名、またはドメインを使用する必要はありません。

#### <a name="import-settings-from-a-backup"></a>バックアップからの設定をインポートします。

構成証明書を復元するには、ポリシー、証明書の PFX ベースおよびを HGS ノードに、バックアップ ファイルからの非 PFX 証明書の公開キーは、初期化された HGS サーバー ノードで次のコマンドを実行します。
バックアップの作成時に指定したパスワードを入力するように促されます。

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

管理者によって信頼された構成証明書ポリシーまたは TPM によって信頼された構成証明書ポリシーをインポートする場合は、これを行う指定することによって、`-ImportActiveDirectoryModeState`または`-ImportTpmModeState`フラグ[インポート HgsServerState](https://technet.microsoft.com/library/mt652168.aspx)します。

Windows Server 2016 が実行する前にインストールされているは、最新の累積的な更新プログラムを確認します`Import-HgsServerState`します。
そのためにはエラーは、インポート中にエラーがあります。

> [!NOTE]
> 既にインストールされているこれらのポリシーの 1 つ以上の既存の HGS ノード上のポリシーを復元する場合、import コマンドにはポリシーごとに重複するエラーが表示されます。
> これは、想定される動作であり、ほとんどの場合に安全に無視されます。

#### <a name="reinstall-private-keys-for-certificates"></a>証明書の秘密キーを再インストールします。
拇印を使用して追加されたバックアップが作成された HGS で使用される証明書のいずれかの場合は、バックアップ ファイルにこれらの証明書の公開キーのみに含まれています。
これは、手動でインストールまたは HGS に HYPER-V ホストからの要求を処理できる前に、各証明書の秘密キーへのアクセスを許可する必要があることを意味します。
その手順を完了するために必要なアクションは、証明書が最初に発行された方法によって異なります。
ソフトウェアを基盤と証明書の証明機関によって発行された CA に連絡して、秘密キーを取得し、インストールする必要があります**各**HGS ノードごとの指示します。
同様に、証明書は、ハードウェアを基盤は、HSM に接続し、秘密キーには、各マシン アクセスを許可するには、各 HGS ノードに必要なドライバーをインストールするハードウェア セキュリティ モジュール製造元のマニュアルを参照する必要があります。

念のため、証明書の拇印を使用して HGS に追加に手動で各ノードに秘密キーのレプリケーションが必要です。
復元された HGS クラスターに追加する各ノードでは、この手順を繰り返す必要があります。

#### <a name="review-imported-attestation-policies"></a>インポートされた構成証明書ポリシーを確認してください。
使用して、インポートされたポリシーを詳しくレビューすべてをバックアップからの設定をインポートしたら後をお勧め`Get-HgsAttestationPolicy`をシールドされた Vm の実行を信頼するホストのみが正常に証明できるかどうかを確認します。
場合は、セキュリティの状態と一致するすべてのポリシーが見つかったら、[無効にするか、または削除](#review-attestation-policies)します。

#### <a name="run-diagnostics-to-check-system-state"></a>診断を実行してシステム状態を確認してください。
設定して、HGS ノードの状態の復元が完了したら後、は、システムの状態を確認する HGS 診断ツールを実行する必要があります。
これを行うには、構成を復元した HGS ノードで、次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics
```

「合格」しない「全体的な結果」の場合は、システムの構成を完了する追加手順が必要です。
詳細については、失敗した subtest(s) で報告されるメッセージを確認します。

## <a name="patching-hgs"></a>HGS 修正プログラムの適用
に関しては、最新の累積的な更新プログラムをインストールすることによって、ホスト ガーディアン サービス ノードを最新に保つために重要です。HGS のまったく新しいノードを設定する場合は、HGS の役割をインストールまたは構成する前に利用可能な更新をインストールすることを強くお勧めします。
これにより、新規または変更された機能がすぐに反映します。

保護されたファブリックを修正するには、ときに最初にアップグレードすることは厳密に推奨される*すべて*HYPER-V ホスト**HGS をアップグレードする前に**します。
これで HGS 構成証明書ポリシーに変更が行われることにより、*後*それらに必要な情報を提供する HYPER-V ホストが更新されました。
更新プログラムがポリシーの動作を変更する場合が自動的に無効になります、ファブリックの中断を回避します。
このような更新プログラムは、新規または変更された構成証明書ポリシーをアクティブ化する次のセクションのガイダンスに従うことが必要です。
Windows Server およびポリシーの更新が必要な場合にチェックするをインストールする累積更新プログラムのリリース ノートを参照することをお勧めします。

### <a name="updates-requiring-policy-activation"></a>ポリシーのアクティブ化を必要とする更新プログラム
HGS の更新プログラムが導入されていますまたは構成証明書のポリシーの動作が大幅に変更は、変更したポリシーをアクティブ化する追加の手順が必要です。
ポリシーの変更は、エクスポートとインポート HGS 状態の後にのみ施行されます。
環境内のすべてのホストを HGS のすべてのノード、累積的な更新プログラムを適用した後にのみ、新しいまたは変更されたポリシーを有効にする必要があります。
すべてのコンピューターが更新されたら、アップグレード プロセスをトリガーする任意の HGS ノードで、次のコマンドを実行します。

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

新しいポリシーが導入された場合は、既定で無効化されます。
新しいポリシーを有効にするには、最初の (プレフィックス 'HGS_' で) Microsoft ポリシーの一覧で検索し、次のコマンドを使用して有効にします。

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>構成証明書ポリシーの管理
HGS では、ホストが「正常」と判断し、シールドされた Vm の実行を許可するために満たす必要がありますの要件の最小セットを定義するいくつかの構成証明書ポリシーを保持します。
これらのポリシーの一部は、Microsoft によって定義は、環境内で使用可能なコード整合性ポリシー、TPM の基準、およびホストを定義することによって他のユーザーが追加されます。
これらのポリシーの定期的なメンテナンスでは、ホストを続ける証明正しくことを確認する、信頼されていないホストや構成が正常に証明からブロックされます、更新、およびそれを置換する必要があります。

管理者によって信頼された構成証明書は、ホストが正常であるかどうかを 1 つだけポリシー: 既知の信頼されたセキュリティ グループのメンバーシップ。
TPM 構成証明でありより複雑なコードと正常な状態である場合を決定する前に、システムの構成を測定するさまざまなポリシーが含まれます。

1 つの HGS を 1 回では、Active Directory と TPM の両方のポリシーで構成できますが、サービス ホストが構成証明を試みると用に構成されている現在のモードのポリシーをことだけが確認します。
HGS サーバーのモードを確認するには、実行`Get-HgsServer`します。

### <a name="default-policies"></a>既定のポリシー
構成証明の TPM によって信頼された HGS で構成されているいくつかの組み込みのポリシーがあります。
これらのポリシーの一部は「ロック」- つまり、セキュリティ上の理由から無効にできません。
次の表では、各既定ポリシーの目的について説明します。

ポリシー名                    | 目的
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | セキュア ブートが有効になっているホストが必要です。 これは、スタートアップのバイナリとその他の UEFI ロックされている設定を測定する必要があります。
Hgs_UefiDebugDisabled          | により、ホストは、カーネル デバッガーを有効にはありません。 ユーザー モード デバッガーは、コード整合性ポリシーによってブロックされます。
Hgs_SecureBootSettings         | ホストを確保するための負のポリシーは、少なくとも 1 つ (管理者が定めた) TPM の基準を照合します。
Hgs_CiPolicy                   | ホストは、管理者が定義した CI ポリシーの 1 つを使用していることを確認するポリシーを負の値。
Hgs_HypervisorEnforcedCiPolicy | ハイパーバイザーによって適用されるコード整合性ポリシーが必要です。 このポリシーを無効にすると、保護カーネル モード コード整合性ポリシーの攻撃に対して脆弱になります。
Hgs_FullBoot                   | により、ホストがスリープまたは休止状態から再開できませんでした。 ホストする必要があります正しく再起動またはシャット ダウンこのポリシーに準拠します。
Hgs_VsmIdkPresent              | ホストが実行されている仮想化ベースのセキュリティが必要です。 IDK では、ホストのセキュリティで保護されたメモリ領域に送信される情報を暗号化するために必要なキーを表します。
Hgs_PageFileEncryptionEnabled  | ページファイルをホストで暗号化する必要があります。 このポリシーを無効にする場合は、テナントのシークレットの暗号化されていないページファイルを検査する場合に公開する情報をなる可能性があります。
Hgs_BitLockerEnabled           | BitLocker、HYPER-V ホストで有効にする必要があります。 このポリシーは、パフォーマンス上の理由から既定で無効にしを有効にするのには推奨されません。 このポリシーは、シールドされた Vm 自体の暗号化には影響を与えません。
Hgs_IommuEnabled               | ホストでは、ダイレクト メモリ アクセスの攻撃を防ぐために使用で IOMMU デバイスがある必要があります。 このポリシーを無効にして、ホストを使用して有効になっている、IOMMU なしには、メモリの攻撃に出力するためのテナント VM の秘密を公開できます。
Hgs_NoHibernation              | 休止状態を HYPER-V ホスト上で無効にする必要があります。 このポリシーを無効にすると、シールドされた VM のメモリを暗号化されていない休止状態ファイルに保存するホストを許可できます。
Hgs_NoDumps                    | メモリ ダンプを HYPER-V ホスト上で無効にする必要があります。 このポリシーを無効にした場合は、シールドされた VM のメモリが暗号化されていないクラッシュ ダンプ ファイルに保存されていることを防ぐために、ダンプ暗号化を構成することをお勧めします。
Hgs_DumpEncryption             | HGS によって信頼されている暗号化キーで暗号化された HYPER-V ホストでは、有効になっている場合、メモリ ダンプが必要です。 このポリシーは、ホストのダンプが有効でない場合に適用されません。 場合はこのポリシーと*Hgs\_NoDumps*両方とも無効、シールドされた VM のメモリは暗号化されていないダンプ ファイルに保存できます。
Hgs_DumpEncryptionKey          | 負の値のポリシーをホストのダンプは、HGS を既知の管理者が定義したダンプ ファイルの暗号化キーを使用しているメモリを許可するように構成します。 このポリシーが適用されない場合に*Hgs\_DumpEncryption*は無効です。

### <a name="authorizing-new-guarded-hosts"></a>保護されたホストを新しい承認
保護されたホストに新しいホストを承認する (例: 証言正常)、HGS は、ホストを信頼する必要があります (TPM によって信頼された構成証明を使用するように構成) の場合とで実行されているソフトウェア。
新しいホストを承認する手順は、HGS が構成された現在の構成証明モードによって異なります。
保護されたファブリックの構成証明モードを確認するには、実行`Get-HgsServer`HGS の任意のノード上。

#### <a name="software-configuration"></a>ソフトウェアの構成
新しい HYPER-V ホストでは、その Windows Server 2016 Datacenter edition がインストールされていることを確認します。
Windows Server 2016 Standard はことはできません、保護されたファブリックで実行のシールドされた Vm。
ホストは、デスクトップ エクスペリエンスまたは Server Core がインストールされている可能性があります。

デスクトップ エクスペリエンス搭載サーバー、および Server Core、Hyper-v ホストと Host Guardian HYPER-V サポート サーバーの役割をインストールする必要があります。

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>管理者によって信頼された構成証明
管理者によって信頼された構成証明を使用する場合は、HGS で新しいホストを登録するには、最初が参加しているドメイン内のセキュリティ グループにホストを追加する必要があります。
通常、各ドメインでは、保護されたホストの 1 つのセキュリティ グループがあります。
HGS で、そのグループが既に登録されている場合、唯一のアクションを実行する必要がありますはそのグループのメンバーシップを更新するホストを再起動するは。

次のコマンドを実行してどのセキュリティ グループが HGS によって信頼されているを確認できます。

```powershell
Get-HgsAttestationHostGroup
```

まずを HGS に新しいセキュリティ グループを登録するには、ホストのドメイン内のグループのセキュリティ識別子 (SID) をキャプチャし、SID を HGS に登録します。

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

ホストのドメインと HGS の間の信頼を設定する方法については、展開ガイドで利用できます。

#### <a name="tpm-trusted-attestation"></a>TPM によって信頼された構成証明
TPM モードでは、HGS を構成する場合、ホストは、すべてのロックされているポリシーおよび"Hgs_"だけでなく、少なくとも 1 つの TPM ベースライン、TPM id、およびコード整合性ポリシーの付いた"enabled"のポリシーに渡す必要があります。
新しいホストを追加するたびに新しい TPM id を HGS に登録する必要があります。
ホストで同じソフトウェアが実行されている (およびが同じコード整合性ポリシーの適用) 限り、環境内の別のホストとして TPM ベースライン、する必要はありません新しい CI ポリシーまたは基準に追加するとします。

**新しいホストの TPM id を追加する**新しいホストでは、TPM id をキャプチャするには、次のコマンドを実行します。
HGS で検索するのに役立つ、ホストの一意の名前を指定することを確認します。
ホストの使用を停止するか、または HGS でシールドされた Vm を実行するを防ぐために必要な場合は、この情報を必要があります。

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

このファイルをホストを HGS に登録するには、次のコマンドを実行し、HGS サーバーにコピーします。

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**追加する新しい TPM ベースライン**新しいホストが新しいハードウェアまたは環境のファームウェア構成を実行している場合は、新しい TPM ベースラインを実行する必要があります。
これを行うには、ホストで、次のコマンドを実行します。

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> ホストが検証に失敗したし、構成証明が正常にないというエラーが発生した場合は、考慮する必要はありません。
> これは、ホストが実行できるかどうかを確認する前提条件チェックのシールドされた Vm、および可能性があるがまだ適用していないコード整合性ポリシーまたはその他の設定が必要です。
> エラー メッセージを読み取る、投稿者、加えることはもう一度やり直してください。
> または、追加することでこの時点で検証をスキップすることができます、`-SkipValidation`コマンド フラグ。

HGS サーバーに TPM ベースラインをコピーし、次のコマンドに登録します。
このクラスは、HYPER-V ホストのハードウェアおよびファームウェア構成を理解するのに役立つ名前付け規則を使用することをお勧めします。

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**新しいコード整合性ポリシーを追加する**HYPER-V ホストで実行されているコード整合性ポリシーを変更した場合、それらのホストが正常に証明できる前に、新しいポリシーを HGS に登録する必要があります。
新しい CI ポリシーを使用して、キャプチャを参照ホストでは、環境内で信頼された HYPER-V マシン用のマスター イメージとなる、`New-CIPolicy`コマンド。
使用するようお願い、 **FilePublisher**レベルと**ハッシュ**HYPER-V ホストの CI ポリシーにフォールバックします。
まず、すべて、正しく動作することを確認する監査モードで CI ポリシーを作成する必要があります。
システム上のサンプルのワークロードを検証した後は、ポリシーを適用し、HGS に適用されるバージョンをコピーできます。
コード整合性ポリシーの構成オプションの完全な一覧を参照して、 [Device Guard ドキュメント](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)します。

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

ポリシーを作成したら、テストし適用、HGS サーバーにバイナリ ファイル (.p7b) をコピーし、ポリシーを登録します。

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**メモリ ダンプ暗号化キーを追加します。**

ときに、 *Hgs\_NoDumps*ポリシーを無効にし、 *Hgs\_DumpEncryption*ポリシーが有効になっている、保護されたホストが しなければなりません (クラッシュ ダンプを含む) メモリ ダンプすることができますそれらのダンプが暗号化されている限り有効になります。 メモリ ダンプを無効になっているがある、または、HGS が知っているキーを使用して暗号化が場合、保護されたホストは証明書を渡すだけです。 既定では、ダンプ暗号化キーが構成されていません HGS にします。

HGS には、ダンプ暗号化キーを追加するには、使用、`Add-HgsAttestationDumpPolicy`ダンプ暗号化キーのハッシュを HGS に提供するコマンドレットです。
ダンプ暗号化で構成されている HYPER-V ホスト上の TPM ベースラインをキャプチャする場合は、ハッシュは、tcglog が用意されておりに提供できる、`Add-HgsAttestationDumpPolicy`コマンドレット。

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

または、コマンドレットにハッシュの文字列表現を直接指定できます。

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

保護されたファブリックの間で異なるキーを使用する場合は、HGS を各一意のダンプ暗号化キーを追加してください。
ホストで認識されないため、HGS キーを使用してメモリ ダンプを暗号化するには、構成証明は渡しません。

についての詳細については、HYPER-V のドキュメントを参照してください[ホストでの暗号化をダンプ構成](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)します。

#### <a name="check-if-the-system-passed-attestation"></a>構成証明書がシステムに渡されたかどうかの確認します。
必要な情報を HGS に登録すると後、は、ホストが、構成証明に合格をチェックする必要があります。
新しく追加された HYPER-V ホストで、次のように実行します。`Set-HgsClientConfiguration`し、HGS クラスターの正しい Url を指定します。
実行して、これらの Url を取得できる`Get-HgsServer`HGS の任意のノード上。

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

結果の状態を示していない場合"IsHostGuarded:True"、構成のトラブルシューティングを行う必要があります。
構成証明が失敗したホストで、失敗した構成証明の解決に役立つ問題に関する詳細なレポートを取得するには、次のコマンドを実行します。

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Windows Server 2019 または Windows 10、バージョンは 1809 を使用しているコードの整合性ポリシーを使用している場合`Get-HgsTrace`のエラーを返す可能性があります、**コード整合性ポリシー Active**診断します。
> だけ失敗した診断がある場合に、この結果を無視してかまいません。

### <a name="review-attestation-policies"></a>構成証明書ポリシーを確認してください。
HGS を構成したポリシーの現在の状態を確認するには、HGS の任意のノードで、次のコマンドを実行します。

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

(たとえば、古いコード整合性ポリシーを今すぐ安全でないと判断)、セキュリティ要件に適合しないポリシーが有効になっている場合は、次のコマンドで、ポリシーの名前を置き換えることで無効にできます。

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

同様に、使用`Enable-HgsAttestationPolicy`ポリシーを再度有効にします。

実行ポリシーと HGS のすべてのノードから削除するが不要になった、`Remove-HgsAttestationPolicy -Name 'PolicyName'`ポリシーを完全に削除します。

## <a name="changing-attestation-modes"></a>構成証明モードを変更します。
管理者によって信頼された構成証明を使用して、保護されたファブリックを開始した場合、環境内に十分な TPM 2.0 と互換性のあるホストがあるとすぐにほど強力な TPM 構成証明モードをアップグレードするは可能性があります。
切り替える準備ができたら、することができますを事前に読み込むすべて HGS の構成証明書アイテム (CI ポリシー、TPM ベースラインおよび TPM の識別子) の構成証明の管理者によって信頼された HGS を実行する継続します。
これを行うには、単に以下の指示に従ってで、[新しい保護されたホストを承認する](#authorizing-new-guarded-hosts)セクション。

HGS には、すべてのポリシーを追加したら、次の手順を TPM モードで構成証明書を渡されるかどうかは、ホストで、代理の構成証明試行を実行することです。
これには、HGS の現在の操作状態は影響しません。
次のコマンドは、環境と少なくとも 1 つの HGS ノード内のホストのすべてにアクセスできるコンピューターで実行する必要があります。
ファイアウォールまたは他のセキュリティ ポリシーは、これを防ぐため、この手順をスキップすることができます。
可能であれば、かどうかを TPM モードの「反転」ダウンタイムが発生、Vm の手掛かりを提供する統合の構成証明の実行をお勧めします。 

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

診断完了後に、すべてのホストには TPM モードでの構成証明が失敗したかどうかを判断する出力される情報を確認します。
各のホストから"pass"を取得し、HGS を TPM モードに変更を続行するまで、診断を再実行します。

**TPM のモードに変更する**はすぐに完了します。
HGS の任意のノード構成証明モードを更新するには、次のコマンドを実行します。

```powershell
Set-HgsServer -TrustTpm
```

問題に Active Directory モードに戻す必要があることを実行する場合は、これを行うを実行して`Set-HgsServer -TrustActiveDirectory`します。

すべて予想どおりに動作を確認した後は、HGS からすべての信頼された Active Directory ホスト グループを削除し、HGS およびファブリックのドメインの間の信頼を削除します。
Active Directory の信頼がの場合、だれかが、信頼を再度有効にして、HGS をチェックされていない、保護されたホスト上で実行するコードが信頼されていない Active Directory のモードに切り替えがリスクです。

## <a name="key-management"></a>キーの管理
保護されたファブリック ソリューションでは、ソリューションのさまざまなコンポーネントの整合性を検証し、テナントのシークレットを暗号化するいくつかの公開/秘密キー ペアを使用します。
ホスト ガーディアン サービスは、署名とシールドされた Vm の起動に使用されるキーの暗号化に使用される (パブリックとプライベートのキー) を持つ 2 つ以上の証明書で構成されます。
これらのキーは、慎重に管理する必要があります。
攻撃者が秘密キーが取得されると場合、ファブリックで実行されているすべての Vm を unshield または場所に配置する防御を迂回する弱い構成証明書ポリシーを使用するなりすまし HGS クラスターを設定できるようされます。
必要があります、障害発生時に秘密キーが失われ、バックアップに見つかりません、新しいキーのペアを設定し、新しい証明書を承認するために再キーと各 VM がある必要があります。

このセクションでは、機能とセキュリティで保護されるため、キーを構成する際に全般的なキー管理のトピックについて説明します。

### <a name="adding-new-keys"></a>新しいキーの追加
HGS は、1 つの一連のキーで初期化する必要があります、中には、1 つ以上の暗号化と署名キーを HGS を追加できます。
なぜ HGS に新しいキーを追加する場合、2 つの最も一般的な理由は次のとおりです。
1. テナントが、ハードウェア セキュリティ モジュールに、秘密キーをコピーし、シールドされた Vm の起動キーのみが認証されますに"bring your own key"のシナリオをサポートします。
2. HGS を最初に新しいキーを追加し、各 VM まで、キーの両方のセットを維持することによって、既存のキーを置き換える新しいキーを使用する構成が更新されました。

新しいキーを追加するプロセスは、使用している証明書の種類によって異なります。

**オプション 1:HSM に格納されている証明書の追加**

HGS キー保護するための推奨されるアプローチは、ハードウェア セキュリティ モジュール (HSM) で作成した証明書を使用することです。
Hsm は、データ センター内のセキュリティに影響するデバイスに物理的にアクセスする、キーの使用が関連付けられているかを確認します。
各 HSM とは異なり、一意な証明書を作成し、それらを HGS に登録するプロセスがあります。
次の手順は、HSM を使用するための大まかなガイダンスについては、証明書をバックアップするため。
正確な手順と機能を HSM ベンダーのドキュメントを参照してください。

1. クラスター内の各 HGS ノードには、HSM ソフトウェアをインストールします。 かどうか、ネットワークまたはローカルの HSM デバイスが、によっては、そのキー ストアに、マシンのアクセスを許可する HSM を構成する必要があります。
2. HSM で 2 つの証明書を作成**2048 ビット RSA キー**暗号化および署名
    1. 暗号化証明書を作成、**データの暗号化**キー、HSM での使用法プロパティ
    2. 署名証明書を作成、**デジタル署名**キー、HSM での使用法プロパティ
3. HSM ベンダーのガイダンスによって各 HGS ノードのローカル証明書ストアに証明書をインストールします。
4. HSM は、特定のアプリケーションやユーザーの秘密キーを使用するアクセス許可を付与する詳細なアクセス許可を使用している場合は、証明書を HGS グループ管理サービス アカウントのアクセス許可する必要があります。 HGS の gMSA アカウントの名前を実行して確認できます。 `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
5. HGS に証明書の次のコマンドの拇印を置き換えることで、署名と暗号化証明書を追加します。

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**オプション 2:エクスポートできないソフトウェア証明書を追加します。**

エクスポートできないプライベート キーを持つ公的証明機関、その拇印を使用して HGS に、証明書を追加する必要がある、会社のソフトウェアを基盤とする証明書がある場合。
1. 証明機関の指示に従ってコンピューターに証明書をインストールします。
2. HGS グループ管理サービス アカウントへの読み取りアクセス証明書の秘密キーを付与します。 HGS の gMSA アカウントの名前を実行して確認できます。 `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
3. 次のコマンドを使用し、証明書の拇印で置換 HGS で、証明書を登録する (変更*暗号化*に*署名*署名証明書の)。

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> 手動で秘密キーをインストールし、HGS の各ノードで、gMSA アカウントに対する読み取りアクセス権を付与する必要があります。
> HGS での秘密キーを自動的に複製できません*任意*サムプリントによって登録された証明書。

**オプション 3:PFX ファイルに格納されている証明書の追加**

ソフトウェアを基盤と証明書を PFX ファイル形式で格納されているし、パスワードで保護されていることができますが、エクスポート可能な秘密キーであれば、HGS できますの証明書の管理に自動的にします。
PFX ファイルに追加された証明書は、HGS クラスターのすべてのノードに自動的にレプリケートし、HGS が秘密キーへのアクセスをセキュリティで保護します。
PFX ファイルを使用して新しい証明書を追加するには、HGS の任意のノードで、次のコマンドを実行 (変更*暗号化*に*署名*証明書に署名するため)。

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**識別とプライマリ証明書を変更**HGS には、複数の署名と暗号化の証明書をサポートできますが、中に「プライマリ」の証明書として 1 つのペアを使用します。
これらは、ユーザーがその HGS クラスター ガーディアン メタデータをダウンロードした場合に使用される証明書です。
証明書は、プライマリ証明書としてマークされていることを確認するには、次のコマンドを実行します。

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

新しい主な暗号化または署名証明書を設定するには、必要な証明書のサムプリントを確認し、次のコマンドを使用してプライマリとしてマークします。

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>更新またはキーを置き換える
HGS で使用される証明書を作成するときに、証明書には、証明機関のポリシーと、要求情報に従って、有効期限が割り当てられます。
通常、証明書の有効性がなどの HTTP 通信をセキュリティで保護する重要なシナリオで、サービスの中断や厄介なエラー メッセージを回避するために有効期限が切れる前になる証明書を更新する必要があります。
HGS では、その意味で証明書を使用しません。
HGS が作成して、非対称キー ペアを格納する便利な方法として証明書の使用だけです。
有効期限が切れた暗号化または署名の証明書 HGS で脆弱性またはシールドされた Vm の保護の損失は示されません。
さらに、証明書失効チェックは、HGS では行われません。
HGS の証明書または発行する機関の証明書が取り消された場合、証明書の HGS の使用は影響しません。

HGS の証明書について心配する必要があるだけの時間は、その秘密キーがあると思われる理由がある場合盗まれました。
その場合は、HGS 暗号化と署名キーのペアの秘密の半分を所有しているが、VM でシールドの保護を削除または弱い構成証明書ポリシーがある偽 HGS サーバーを作成するのに十分なため、シールドされた Vm の整合性に危険にさらさが。

そのような状況を検出するか、またはコンプライアンスの標準証明書のキーを定期的に更新するために必要な場合、HGS サーバーでキーを変更するプロセスの概要、次の手順。
次のガイダンスが HGS クラスターによって処理される各 VM にサービスの中断の原因となる重要な取り組みを表すことに注意してください。
サービスの中断を最小限に抑えるし、テナントの Vm のセキュリティを確保するには、HGS キーを変更するための適切な計画が必要です。

HGS ノードでは、新しい暗号化と署名証明書のペアを登録するには、次の手順を実行します。
参照してください[新しいキーの追加](#adding-new-keys)の詳細については、さまざまな方法 HGS に新しいキーを追加します。
1. 新しい暗号化と署名証明書、HGS サーバーのペアを作成します。 理想的には、これらは、ハードウェア セキュリティ モジュールで作成されます。
2. 新しい暗号化機能を登録し、署名証明書で**追加 HgsKeyProtectionCertificate**

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. 拇印を使用した場合は、秘密キーをインストールし、キーに HGS gMSA へのアクセス許可をクラスター内の各ノードに移動する必要があります。
4. HGS で既定の証明書の新しい証明書を作成します。

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

この時点では、シールド HGS ノードから取得したメタデータで作成されたデータは新しいの証明書を使用しますが、既存の Vm は引き続き以前の証明書は引き続き行われますのでの機能します。
既存のすべての Vm は新しいキーを使用して動作を確保するためには、各 VM にキー保護機能を更新する必要があります。
これは、関与する VM の所有者 (個人または団体「所有者」ガーディアンを所有している) が必要な操作です。
シールドされた vm ごとに、次の手順に従います。
5. VM をシャット ダウンします。 VM は、繰り返し処理を開始する必要があります。 そう、残りの手順が完了するまで戻るにことはできません。
6. 現在のキー保護機能をファイルに保存します。 `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. VM 所有者への転送、KP
8. 所有者ダウンロード HGS からガーディアンが更新された情報があり、ローカル システム上のインポート
9. 現在 KP をメモリに読み込まれる、KP に新しいガーディアンへのアクセスを許可し、次のコマンドを実行して、新しいファイルに保存します。

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. コピー ホスティング ファブリックに更新された KP
11. 元の VM に、KP が適用されます。

    ```powershell
    $updatedKP = Get-Content -Path .\updatedVM001.kp
    Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
    ```
12. 最後に、VM を起動し、正常に実行することを確認します。

> [!NOTE]
> VM 所有者が、VM での不適切なキー保護機能の設定、VM の実行に、ファブリックが承認しない場合、シールドされた VM を起動することはできません。
> 最後の正常なキー プロテクターに戻り、次のように実行します。 `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`

すべての Vm を新しいガーディアン キーの承認を更新すると、無効にし、古いキーを削除できます。

13. 古い証明書の拇印を取得します。 `Get-HgsKeyProtectionCertificate -IsPrimary $false`

14. 次のコマンドを実行して、各証明書を無効にします。  

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
    ```

15. Vm が最初にできないことを確認した後は、無効にすると、証明書は、次のコマンドを実行して、証明書を HGS から削除します。

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM のバックアップは、VM を起動するために使用するには、古い証明書を許可する古いキー保護機能情報が格納されます。
> 対応の秘密キーが侵害されている場合は、VM のバックアップが侵害される可能性が、すぎる、し、適切な措置を想定してください。
> バックアップ (.vmcx) からの VM 構成を破棄すると、BitLocker 回復パスワードを使用して、次に、VM を起動する必要があるが、キー プロテクターが削除されます。

### <a name="key-replication-between-nodes"></a>ノード間でキーのレプリケーション
同じの暗号化、署名、および (構成されている) 場合は、HGS クラスター内のすべてのノードを構成する必要がある SSL 証明書。
これは、正常に処理された、要求を持つことができます、HYPER-V ホストをクラスター内の任意のノードに問い合わせることを確認する必要があります。

**証明書の PFX ベースでの HGS サーバーが初期化されるかどうか**HGS は、クラスター内のすべてのノード間でこれらの証明書の公開および秘密キーの両方を自動的にレプリケートします。 その後です。
のみ、1 つのノードにキーを追加する必要があります。

**証明書の参照を含む HGS サーバーが初期化されている場合**拇印、し、HGS のみがレプリケートされますか、*パブリック*の各ノードに証明書のキー。
さらに、HGS を与えることはできません自体にこのシナリオでは、任意のノードで秘密キーにアクセスします。
したがって、ユーザーの責任は。
1. HGS の各ノードに秘密キーをインストールします。
2. HGS グループ管理サービス アカウント (gMSA) へのアクセス許可、秘密キーの各ノードでこれらのタスクは、余分な運用上の負担を追加 HSM バックアップ キーと秘密キーをエクスポートできない証明書に必要な場合がします。

**SSL 証明書**はどのような形式はレプリケートされません。
ユーザーの責任で同じ SSL 証明書では、各 HGS サーバーを初期化し、SSL 証明書を置換または更新するたびに、各サーバーを更新することをお勧めします。
SSL 証明書を交換するときを使用して実行することをお勧めしますが、[セット HgsServer](https://technet.microsoft.com/library/mt652180.aspx)コマンドレット。

## <a name="unconfiguring-hgs"></a>HGS の構成解除しています

使用を停止または大幅に HGS サーバーを再構成する必要がある場合を使用して行うことができます、[クリア HgsServer](https://technet.microsoft.com/library/mt652176.aspx)または[アンインストール HgsServer](https://technet.microsoft.com/library/mt652182.aspx)コマンドレット。

### <a name="clearing-the-hgs-configuration"></a>HGS の構成をクリアします。

HGS クラスターからノードを削除するには、使用、[クリア HgsServer](https://technet.microsoft.com/library/mt652176.aspx)コマンドレット。
このコマンドレットが実行されているサーバーで、次の変更になります。

- 構成証明およびキー保護サービスの登録を解除します。
- "Microsoft.windows.hgs"JEA の管理エンドポイントを削除します。
- HGS のフェールオーバー クラスターからローカル コンピューターを削除します。

サーバーがクラスター内の最後の HGS ノードの場合、クラスターとその対応する分散ネットワーク名リソースも破棄されます。

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

HGS サーバーに再初期化できる消去操作が完了すると、 [Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx)します。
使用した場合[インストール HgsServer](https://technet.microsoft.com/library/mt652169.aspx) Active Directory Domain Services ドメインを設定するにそのドメインは維持され構成されていると運用クリア操作の完了後します。

### <a name="uninstalling-hgs"></a>HGS のアンインストール

HGS クラスターからノードを削除する**と**ことで実行されている、Active Directory ドメイン コントローラの降格を使用して、[アンインストール HgsServer](https://technet.microsoft.com/library/mt652182.aspx)コマンドレット。
このコマンドレットが実行されているサーバーで、次の変更になります。

- 構成証明およびキー保護サービスの登録を解除します。
- "Microsoft.windows.hgs"JEA の管理エンドポイントを削除します。
- HGS のフェールオーバー クラスターからローカル コンピューターを削除します。
- 構成されている場合は、Active Directory ドメイン コント ローラーを降格します。

サーバーがクラスター内の最後の HGS ノードの場合は、ドメイン、フェールオーバー クラスターおよびクラスターの分散ネットワーク名リソースも破棄されます。

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

に対して、HGS を使用してを再インストールできる、アンインストール操作が完了し、コンピューターが再起動されて、[インストール HgsServer](https://technet.microsoft.com/library/mt652169.aspx)コンピューターをドメインに参加させるし、そのドメインに HGS サーバーを初期化または[Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx)します。

不要になったコンピューター HGS ノードとして使用する場合は、Windows からロールを削除できます。

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
