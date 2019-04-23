---
title: 既存の要塞フォレスト内での HGS をインストールします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 147610d9dcb36dfedab3aca11ee1a64731715519
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842223"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>既存の要塞フォレスト内での HGS をインストールします。 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS サーバーを既存のドメインに参加させる

既存の要塞フォレストのルート ドメインに HGS を追加する必要があります。 サーバー マネージャーを使用してまたは[Add-computer](https://go.microsoft.com/fwlink/?LinkId=821564) HGS サーバーをルート ドメインに参加させる。

## <a name="add-the-hgs-server-role"></a>HGS サーバーの役割を追加します。

管理者特権の PowerShell セッションで、このトピックのすべてのコマンドを実行します。

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

データ センターに HGS ノードを追加するセキュリティで保護された要塞フォレストがある場合は、以下の手順を実行します。
同じドメインに参加している 2 つまたは複数の独立した HGS クラスターを構成するのに手順を使用することもできます。

## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS サーバーを既存のドメインに参加させる

サーバー マネージャーを使用してまたは[Add-computer](https://go.microsoft.com/fwlink/?LinkId=821564) HGS サーバーを目的のドメインに参加させる。

## <a name="prepare-active-directory-objects"></a>Active Directory オブジェクトを準備します。

グループの管理されたサービス アカウントと 2 つのセキュリティ グループを作成します。
またをプレステージングできるクラスター オブジェクトでの HGS を初期化するアカウントがドメインにコンピューター オブジェクトを作成する権限を持たない場合です。

## <a name="group-managed-service-account"></a>グループ管理サービス アカウント

グループ管理サービス アカウント (gMSA) は、HGS を取得し、その証明書を使用して、使用する id です。 使用[New-adserviceaccount](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adserviceaccount) gMSA を作成します。
ドメイン内の最初の gMSA の場合は、キー配布サービスのルート キーを追加する必要があります。

HGS の各ノードは、gMSA パスワードにアクセスできるようにする必要があります。
これを構成する最も簡単な方法は、すべての HGS ノードを含むセキュリティ グループを作成して、gMSA パスワードを取得するセキュリティ グループ アクセスを許可します。

その新しいグループのメンバーシップを取得することを確認するセキュリティ グループに追加した後は、HGS サーバーを再起動する必要があります。

```powershell
# Check if the KDS root key has been set up
if (-not (Get-KdsRootKey)) {
    # Adds a KDS root key effective immediately (ignores normal 10 hour waiting period)
    Add-KdsRootKey -EffectiveTime ((Get-Date).AddHours(-10))
}

# Create a security group for HGS nodes
$hgsNodes = New-ADGroup -Name 'HgsServers' -GroupScope DomainLocal -PassThru

# Add your HGS nodes to this group
# If your HGS server object is under an organizational unit, provide the full distinguished name instead of "HGS01"
Add-ADGroupMember -Identity $hgsNodes -Members "HGS01"

# Create the gMSA
New-ADServiceAccount -Name 'HGSgMSA' -DnsHostName 'HGSgMSA.yourdomain.com' -PrincipalsAllowedToRetrieveManagedPassword $hgsNodes
```

GMSA は、各 HGS サーバー上のセキュリティ ログにイベントを生成する権限が必要です。
グループ ポリシーを使用してユーザー権利の割り当てを構成する場合は、gMSA アカウントが許可されていることを確認、[イベントの監査の特権を生成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29)HGS サーバー。

> [!NOTE]
> グループ管理サービス アカウントとは、以降、Windows Server 2012 の Active Directory スキーマで利用可能です。
> 詳細については、次を参照してください。[グループ管理サービス アカウント要件](https://technet.microsoft.com/library/jj128431.aspx)します。

## <a name="jea-security-groups"></a>JEA セキュリティ グループ

HGS を構成するときに、 [Just Enough Administration (JEA)](https://aka.ms/JEAdocs) PowerShell エンドポイントの完全なローカル管理者権限が必要なく HGS を管理する管理者の許可されています。
JEA を使用して、HGS を管理する必要はありませんが、まだ必要があります構成初期化 HgsServer を実行している場合。
HGS 管理者および HGS のレビュー担当者を含む 2 つのセキュリティ グループを指定する場合に、JEA エンドポイントの構成で構成されます。
管理グループに属しているユーザーは、追加、変更、または HGS; 上のポリシーの削除レビュー担当者は、現在の構成のみを表示できます。

Active Directory 管理ツールを使用してこれらの JEA グループに対して 2 つのセキュリティ グループを作成または[New-adgroup](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adgroup)します。

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>クラスター オブジェクト

HGS の設定を使用しているアカウントがドメインに新しいコンピューター オブジェクトを作成する権限を持たない場合は、クラスター オブジェクトを事前に展開する必要があります。
次の手順についてで[Active Directory Domain Services で Prestage Cluster Computer Objects](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)します。

最初、HGS ノードを設定するには 1 つのクラスター名オブジェクト (CNO) と 1 つの仮想コンピューター オブジェクト (VCO) を作成する必要があります。
CNO は、クラスターの名前を表すし、フェールオーバー クラスタ リングによって内部的に使用が主にします。
VCO は、クラスター上に存在する HGS サービスを表し、DNS サーバーに登録されている名前になります。

> [!IMPORTANT]
> 実行するユーザー`Initialize-HgsServer`必要があります**フル コントロール**Active Directory 内の CNO と VCO オブジェクト。

CNO と VCO をプレステージ迅速に、次の PowerShell コマンドを実行して Active Directory 管理者があります。

```powershell
# Create the CNO
$cno = New-ADComputer -Name 'HgsCluster' -Description 'HGS CNO' -Enabled $false -Passthru

# Create the VCO
$vco = New-ADComputer -Name 'HgsService' -Description 'HGS VCO' -Passthru

# Give the CNO full control over the VCO
$vcoPath = Join-Path "AD:\" $vco.DistinguishedName
$acl = Get-Acl $vcoPath
$ace = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $cno.SID, "GenericAll", "Allow"
$acl.AddAccessRule($ace)
Set-Acl -Path $vcoPath -AclObject $acl

# Allow time for your new CNO and VCO to replicate to your other Domain Controllers before continuing
```

## <a name="security-baseline-exceptions"></a>セキュリティ ベースラインの例外

HGS を展開する、高ロックダウンの環境には、特定のグループ ポリシー設定によって HGS が正常に動作できない可能性があります。
次の設定、グループ ポリシー オブジェクトをチェックし、影響を受ける場合の指示に従います。

### <a name="network-logon"></a>ネットワークへのログオン

**ポリシーのパス:** コンピューター構成 \windows 設定 \ セキュリティ settings \local policies \user 権利の割り当て

**ポリシー名:** ネットワークからのこのコンピューターへのアクセスを拒否する

**必要な値:** 値がすべてのローカル アカウントのネットワーク ログオンをブロックしないことを確認します。 ただし、ローカル管理者アカウントに安全にブロックできます。

**理由:** フェールオーバー クラスタ リングは、クラスター ノードを管理する CLIUSR と呼ばれる管理者以外のローカル アカウントに依存します。 このユーザーのブロックのネットワーク ログオンすると、クラスターが正常に動作できなくなります。

### <a name="kerberos-encryption"></a>Kerberos の暗号化

**ポリシーのパス:** コンピューターの構成\Windows の設定\セキュリティの設定\ローカル ポリシー\セキュリティ オプション

**ポリシー名:** ネットワーク セキュリティ:Kerberos で許可する暗号化の種類を構成します。

**アクション**:このポリシーが構成されている場合で、gMSA アカウントを更新する必要があります[Set-adserviceaccount](https://docs.microsoft.com/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps)このポリシーでサポートされている暗号化の種類のみを使用します。 たとえば、ポリシーでは、AES128 のみが許可する場合\_HMAC\_SHA1 および AES256\_HMAC\_実行するには SHA1、`Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256`します。



## <a name="next-steps"></a>次のステップ

- TPM ベースの構成証明を設定する次の手順を参照してください。 [HGS クラスターを既存の要塞フォレスト内の TPM のモードを使用して初期化](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)します。
- ホスト キーの構成証明を設定する次の手順を参照してください。 [HGS クラスター キーのモードを使用して、既存の要塞フォレスト内の初期化](guarded-fabric-initialize-hgs-key-mode-bastion.md)します。
- (Windows Server 2019 で非推奨) 管理ベースの認証、設定する手順を参照してください、次の[初期化 AD モードを使用して、既存の要塞フォレストの HGS クラスター](guarded-fabric-initialize-hgs-ad-mode-bastion.md)します。

