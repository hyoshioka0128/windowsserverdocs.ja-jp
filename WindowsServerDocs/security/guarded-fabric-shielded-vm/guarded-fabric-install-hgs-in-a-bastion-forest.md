---
title: 既存の要塞フォレストに HGS をインストールする
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 331fc5a4e825dc4e7faf6f0a65605d7aaebf8314
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181698"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>既存の要塞フォレストに HGS をインストールする

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS サーバーを既存のドメインに参加させる

既存の要塞フォレストでは、HGS をルートドメインに追加する必要があります。 サーバーマネージャーまたは[コンピューターの追加](https://go.microsoft.com/fwlink/?LinkId=821564)を使用して、HGS サーバーをルートドメインに参加させます。

## <a name="add-the-hgs-server-role"></a>HGS サーバーロールを追加する

管理者特権の PowerShell セッションで、このトピックのすべてのコマンドを実行します。

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)]

データセンターに、HGS ノードを参加させるセキュリティで保護された要塞フォレストがある場合は、次の手順を実行します。
これらの手順を使用して、同じドメインに参加している2つ以上の独立した HGS クラスターを構成することもできます。

## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS サーバーを既存のドメインに参加させる

サーバーマネージャーまたは[コンピューターの追加](https://go.microsoft.com/fwlink/?LinkId=821564)を使用して、HGS サーバーを目的のドメインに参加させます。

## <a name="prepare-active-directory-objects"></a>Active Directory オブジェクトを準備する

グループの管理されたサービスアカウントと2つのセキュリティグループを作成します。
HGS を初期化するアカウントにドメイン内のコンピューターオブジェクトを作成するためのアクセス許可がない場合は、クラスターオブジェクトを事前にステージングすることもできます。

## <a name="group-managed-service-account"></a>グループの管理されたサービス アカウント

グループの管理されたサービスアカウント (gMSA) は、HGS が証明書を取得して使用するために使用する id です。 GMSA を作成するには、 [New-ADServiceAccount](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adserviceaccount)を使用します。
ドメイン内の最初の gMSA の場合は、キー配布サービスのルートキーを追加する必要があります。

各 HGS ノードには、gMSA パスワードへのアクセスが許可されている必要があります。
これを構成する最も簡単な方法は、すべての HGS ノードを含むセキュリティグループを作成し、そのセキュリティグループに gMSA パスワードを取得するアクセス権を付与することです。

新しいグループメンバーシップが確実に取得されるようにするには、セキュリティグループに追加した後で HGS サーバーを再起動する必要があります。

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

GMSA は、各 HGS サーバーのセキュリティログにイベントを生成する権限を必要とします。
グループポリシーを使用してユーザー権利の割り当てを構成する場合は、HGS サーバーで gMSA アカウントに "[監査イベントの生成" 権限](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29)が付与されていることを確認してください。

> [!NOTE]
> グループの管理されたサービスアカウントは、Windows Server 2012 Active Directory スキーマから使用できます。
> 詳細については、「グループの管理された[サービスアカウントの要件](https://technet.microsoft.com/library/jj128431.aspx)」を参照してください。

## <a name="jea-security-groups"></a>JEA セキュリティグループ

HGS を設定すると、[十分な管理 (JEA)](https://aka.ms/JEAdocs) PowerShell エンドポイントが構成され、管理者は完全なローカル管理者特権を必要とせずに hgs を管理できるようになります。
HGS を管理するために JEA を使用する必要はありませんが、HgsServer の実行時に構成する必要があります。
JEA エンドポイントの構成は、HGS 管理者と HGS レビューアーを含む2つのセキュリティグループを指定することで構成されます。
管理者グループに属するユーザーは、HGS でポリシーを追加、変更、または削除できます。レビュー担当者は、現在の構成のみを表示できます。

Active Directory 管理ツールまたは[新しい-ADGroup](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adgroup)を使用して、これらの jea グループに2つのセキュリティグループを作成します。

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>クラスター オブジェクト

HGS のセットアップに使用しているアカウントに、ドメインに新しいコンピューターオブジェクトを作成するためのアクセス許可がない場合は、クラスターオブジェクトを事前にステージングする必要があります。
これらの手順については、「 [Active Directory Domain Services でクラスターコンピューターオブジェクトをプレステージ](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)する」をご説明します。

最初の HGS ノードを設定するには、1つのクラスター名オブジェクト (CNO) と1つの仮想コンピューターオブジェクト (VCO) を作成する必要があります。
CNO はクラスターの名前を表し、主にフェールオーバークラスタリングによって内部的に使用されます。
VCO は、クラスター上に存在する HGS サービスを表し、DNS サーバーに登録されている名前になります。

> [!IMPORTANT]
> を実行するユーザーは、 `Initialize-HgsServer` Active Directory の CNO オブジェクトと VCO オブジェクトを**完全に制御**する必要があります。

CNO と VCO を簡単に事前設定するには、Active Directory 管理者に次の PowerShell コマンドを実行します。

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

## <a name="security-baseline-exceptions"></a>セキュリティベースラインの例外

HGS を高度にロックされた環境に展開する場合、特定のグループポリシー設定を使用すると、HGS が正常に動作しなくなる可能性があります。
グループポリシーオブジェクトで次の設定を確認し、影響を受ける場合はガイダンスに従います。

### <a name="network-logon"></a>ネットワークログオン

**ポリシーのパス:** コンピューターのシステムの保護 \] 権利の権限の割り当て

**ポリシー名:** ネットワークからのこのコンピューターへのアクセスを拒否する

**必須の値:** 値がすべてのローカルアカウントのネットワークログオンをブロックしていないことを確認します。 ただし、ローカルの管理者アカウントは安全にブロックできます。

**理由:** フェールオーバークラスタリングでは、CLIUSR という管理者以外のローカルアカウントを利用してクラスターノードを管理します。 このユーザーのネットワークログオンをブロックすると、クラスターが正しく動作しなくなります。

### <a name="kerberos-encryption"></a>Kerberos 暗号化

**ポリシーのパス:** コンピューターの設定 \] 権利セキュリティオプション

**ポリシー名:** ネットワークセキュリティ: Kerberos で許可される暗号化の種類を構成する

**アクション**: このポリシーが構成されている場合、このポリシーでサポートされている暗号化の種類のみを使用するように、gMSA アカウントを[adserviceaccount](https://docs.microsoft.com/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps)に更新する必要があります。 たとえば、ポリシーで AES128 hmac sha1 と AES256 hmac sha1 のみが許可されている場合は、を \_ \_ 実行する \_ \_ 必要があり `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256` ます。



## <a name="next-steps"></a>次のステップ

- TPM ベースの構成証明を設定する次の手順については、「[既存の要塞フォレストで tpm モードを使用して HGS クラスターを初期化](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)する」を参照してください。
- ホストキーの構成証明を設定する次の手順については、「[既存の要塞フォレストでキーモードを使用して HGS クラスターを初期化](guarded-fabric-initialize-hgs-key-mode-bastion.md)する」を参照してください。
- 管理者ベースの2019構成証明を設定する次の手順については、「[既存の要塞フォレストの AD モードを使用して HGS クラスターを初期化](guarded-fabric-initialize-hgs-ad-mode-bastion.md)する」を参照してください。

