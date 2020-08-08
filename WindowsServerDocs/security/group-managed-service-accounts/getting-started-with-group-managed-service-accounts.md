---
title: Getting Started with Group Managed Service Accounts
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 979a6cf1e0b5e2d68c05f6285a9d745eabe41fa4
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991515"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>Getting Started with Group Managed Service Accounts

>適用先:Windows Server (半期チャネル)、Windows Server 2016


このガイドでは、Windows Server 2012 でグループの管理されたサービスアカウントを有効にして使用するための詳細な手順と背景情報について説明します。

**このドキュメントの内容**

-   [前提条件](#BKMK_Prereqs)

-   [はじめに](#BKMK_Intro)

-   [新しいサーバー ファームの展開](#BKMK_DeployNewFarm)

-   [既存のサーバー ファームへのメンバー ホストの追加](#BKMK_AddMemberHosts)

-   [グループの管理されたサービス アカウント プロパティの更新](#BKMK_Update_gMSA)

-   [既存のサーバー ファームからのメンバー ホストの使用停止](#BKMK_DecommMemberHosts)


> [!NOTE]
> このトピックでは、説明した手順の一部を自動化するのに使用できる Windows PowerShell コマンドレットのサンプルを示します。 詳細については、「[コマンドレットの使用](https://go.microsoft.com/fwlink/p/?linkid=230693)」を参照してください。

## <a name="prerequisites"></a><a name="BKMK_Prereqs"></a>前提条件
[グループの管理されたサービス アカウントの要件](#BKMK_gMSA_Req)については、このトピックのセクションを参照してください。

## <a name="introduction"></a><a name="BKMK_Intro"></a>はじめに
ネットワーク負荷分散 (NLB) (またはすべてのサーバーがクライアントに対して同じサービスを提供している) などの方式を使用しているサーバー ファームにホストされたサービスにクライアント コンピューターが接続するときに、サービスのすべてのインスタンスが同じプリンシパルを使用していない場合は、相互認証 (Kerberos など) をサポートする認証プロトコルを使用することはできません。 つまり、各サービスは同じパスワード/キーを使用して ID を証明する必要があります。

> [!NOTE]
> フェールオーバー クラスターでは、gMSA をサポートしていません。 ただし、クラスター サービスの上位で実行されるサービスは、それが Windows サービス、アプリケーション プール、またはスケジュールされたタスクである場合、あるいは gMSA/sMSA をネイティブにサポートしている場合、gMSA または sMSA を使用できます。

サービスは次のプリンシパルを選択肢として備えており、各プリンシパルには特定の制限があります。

|プリンシパル|Scope|サポートされるサービス|パスワード管理|
|-------|-----|-----------|------------|
|Windows システムのコンピューター アカウント|Domain|ドメインに参加している 1 つのサーバーに限定|コンピューターによる管理|
|Windows システムなしのコンピューター アカウント|Domain|ドメインに参加している任意のサーバー|None|
|仮想アカウント|ローカル|1 つのサーバーに限定|コンピューターによる管理|
|Windows 7 スタンドアロンの管理されたサービス アカウント|Domain|ドメインに参加している 1 つのサーバーに限定|コンピューターによる管理|
|ユーザー アカウント|Domain|ドメインに参加している任意のサーバー|None|
|グループの管理されたサービス アカウント|Domain|任意の Windows Server 2012 ドメインに参加しているサーバー|ドメイン コントローラーによる管理、ホストによる取得|

Windows コンピューター アカウント、Windows 7 スタンドアロンの管理されたサービス アカウント (sMSA)、または仮想アカウントを複数のシステムで共有することはできません。 1 つのアカウントをサーバー ファームのサービスで共有するように構成する場合は、Windows システムとは別にユーザー アカウントまたはコンピューター アカウントを選択する必要があります。 いずれにしても、これらのアカウントには、シングルポイントコントロールでパスワードを管理する機能はありません。 このため問題が生じます。各組織は Active Directory のサービスのキーを更新してそのキーを該当するすべてのサービスのインスタンスに配布するために、コストの高いソリューションを作成する必要があります。

Windows Server 2012 では、サービスまたはサービス管理者は、グループの管理されたサービスアカウント (gMSA) を使用するときに、サービスインスタンス間のパスワード同期を管理する必要はありません。 AD で gMSA をプロビジョニングし、管理されたサービス アカウントをサポートするサービスを構成します。 Active Directory モジュールに含まれる *-ADServiceAccount コマンドレットを使用して gMSA をプロビジョニングできます。 ホストでのサービス ID の構成は、次のものによってサポートされます。

-   sMSA と同じ API。したがって sMSA をサポートする製品は gMSA をサポートします。

-   サービス コントロール マネージャーを使用してログオン ID を構成するサービス。

-   アプリケーション プールに対応する IIS マネージャーを使用して ID を構成するサービス。

-   タスク スケジューラを使用するタスク。

### <a name="requirements-for-group-managed-service-accounts"></a><a name="BKMK_gMSA_Req"></a>グループの管理されたサービス アカウントの要件
次の表に、Kerberos 認証が gMSA を使用してサービスを操作するための、オペレーティング システムの要件を一覧します。 表の後に Active Directory の要件を一覧します。

グループの管理されたサービス アカウントを管理するために使用する Windows PowerShell コマンドレットを実行するには 64 ビット アーキテクチャが必要です。

**オペレーティングシステムの要件**

|要素|要件|オペレーティング システム|
|------|--------|----------|
|クライアント アプリケーション ホスト|RFC 準拠の Kerberos クライアント|Windows XP 以降|
|ユーザーアカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|共有されたサービス メンバー ホスト|| Windows Server 2012 |
|メンバーホストのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|gMSA アカウントのドメイン Dc| パスワードを取得するためにホストで使用できる Windows Server 2012 Dc|Windows server 2012 より前の一部のシステムを持つことができる Windows Server 2012 を使用するドメイン |
|バックエンド サービス ホスト|RFC 準拠の Kerberos アプリケーション サーバー|Windows Server 2003 以降|
|バックエンドサービスアカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|Active Directory の Windows PowerShell|64 ビット アーキテクチャをサポートするコンピューターまたはリモート管理コンピューターにローカルにインストールされた Windows PowerShell for Active Directory (たとえば、リモート サーバー管理ツールキットを使用)| Windows Server 2012 |

**Active Directory ドメイン サービスの要件**

-   GMSA を作成するには、gMSA ドメインのフォレスト内の Active Directory スキーマを Windows Server 2012 に更新する必要があります。

    スキーマを更新するには、Windows Server 2012 を実行するドメインコントローラーをインストールするか、Windows Server 2012 を実行しているコンピューターから adprep.exe のバージョンを実行します。 オブジェクト CN=Schema、CN=Configuration、DC=Contoso、DC=Com の object-version 属性値は 52 でなければなりません。

-   プロビジョニングされた新しい gMSA アカウント

-   グループ別に gMSA を使用するサービス ホストのアクセス許可を管理している場合は、新規または既存のセキュリティ グループ。

-   グループ別にサービス アクセス コントロールを管理する場合は、新規または既存のセキュリティ グループ。

-   Active Directory の最初のマスター ルート キーがドメインに展開されていない場合または作成されていない場合は、それを作成します。 作成した結果は、KdsSvc 操作ログ (Event ID 4004) で検証できます。

キーを作成する方法については、「 [create The Key Distribution SERVICES KDS Root key](create-the-key-distribution-services-kds-root-key.md)」を参照してください。 Microsoft キー配布サービス (kdssvc.dll)、AD のルート キー。

**ライフサイクル**

gMSA 機能を使用するサーバー ファームのライフサイクルは、通常、次のタスクを必要とします。

-   新しいサーバー ファームの展開

-   既存のサーバー ファームへのメンバー ホストの追加

-   既存のサーバー ファームからのメンバー ホストの使用停止

-   既存のサーバー ファームの使用停止

-   必要に応じて、セキュリティ侵害を受けているメンバー ホストをサーバー ファームから削除

## <a name="deploying-a-new-server-farm"></a><a name="BKMK_DeployNewFarm"></a>新しいサーバー ファームの展開
新しいサーバー ファームを展開するとき、サービス管理者は次のことを決める必要があります。

-   サービスが gMSA の使用をサポートするかどうか

-   サービスが認証済みの受信接続または送信接続を必要とするかどうか

-   gMSA を使用するサービス用のメンバー ホストのコンピューター アカウント名

-   サービスの NetBIOS 名

-   サービスの DNS ホスト名

-   サービスのサービス プリンシパル名 (SPN)

-   パスワード変更間隔 (既定では 30 日)。

### <a name="step-1-provisioning-group-managed-service-accounts"></a><a name="BKMK_Step1"></a>手順 1:グループの管理されたサービス アカウントのプロビジョニング
GMSA を作成できるのは、フォレストのスキーマが Windows Server 2012 に更新されていて、Active Directory のマスタールートキーが展開されており、gMSA が作成されるドメインに少なくとも1つの Windows Server 2012 DC がある場合のみです。

次の手順を完了するには、[**Domain Admins**] または [**Account Operators**] のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを作成する機能が最低限必要です。

> [!NOTE]
> -Name パラメーターの値は常に必須です (-Name を指定するかどうかにかかわらず)。-DNSHostName、-RestrictToSingleComputer、および-RestrictToOutboundAuthentication は、3つの展開シナリオでセカンダリ要件となります。


#### <a name="to-create-a-gmsa-using-the-new-adserviceaccount-cmdlet"></a><a name="BKMK_CreateGMSA"></a>New-ADServiceAccount コマンドレットを使用して gMSA を作成するには

1.  Windows Server 2012 ドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell のコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します (Active Directory モジュールが自動的にロードされます)。

    **New-ADServiceAccount [-Name] &lt; string &gt; -DNSHostName &lt; string &gt; [-KerberosEncryptionType &lt; ADKerberosEncryptionType &gt; ] [-Managedpasswordintervalindays <Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword <adprincipal [] >] [-SamAccountName &lt; string &gt; ] [-serviceprincipalnames <string [] >]**

    |パラメーター|String|例|
    |-------|-----|------|
    |名前|アカウントの名前|ITFarm1|
    |DNSHostName|サービスの DNS ホスト名|ITFarm1.contoso.com|
    |KerberosEncryptionType|ホスト サーバーによってサポートされる暗号化の種類|None、RC4、AES128、AES256|
    |ManagedPasswordIntervalInDays|日単位のパスワード変更間隔 (指定がなければ既定では 30 日)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|ITFarmHosts|
    |SamAccountName|Name と同じでない場合はサービスの NetBIOS 名|ITFarm1|
    |ServicePrincipalNames|サービスのサービス プリンシパル名 (SPN)|http/ITFarm1/contoso .com、http/ITFarm1/contoso、http/ITFarm1/、http/ITFarm1/contoso、MSSQLSvc/ITFarm1、MSSQLSvc、ITFarm1、INST01、の順に実行して、のようにしてください。|

    > [!IMPORTANT]
    > パスワード変更間隔は作成時にしか設定できません。 パスワード変更間隔を変更する必要がある場合は、新しい gMSA を作成し、作成時にその間隔を設定してください。

    **例**

    コマンドレットを単一行に入力します。ただし、書式上の制約から複数行に改行されて表示される場合があります。

    ```Powershell
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$ -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso
    ```

この手順を完了するには、[**Domain Admins**] または [**Account Operators**] のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを作成する機能が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](/previous-versions/orphan-topics/ws.10/dd728026(v=ws.10))」を参照してください。

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>New-ADServiceAccount コマンドレットを使用して、送信の認証のみに gMSA を作成するには

1.  Windows Server 2012 ドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **New-ADServiceAccount [-Name] &lt; &gt; RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays <Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword <adprincipal [] >]**

    |パラメーター|String|例|
    |-------|-----|------|
    |名前|アカウントの名前|ITFarm1|
    |ManagedPasswordIntervalInDays|日単位のパスワード変更間隔 (指定がなければ既定では 30 日)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|ITFarmHosts|

    > [!IMPORTANT]
    > パスワード変更間隔は作成時にしか設定できません。 パスワード変更間隔を変更する必要がある場合は、新しい gMSA を作成し、作成時にその間隔を設定してください。

  **例**

```PowerShell
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$
```

### <a name="step-2-configuring-service-identity-application-service"></a><a name="BKMK_ConfigureServiceIdentity"></a>手順 2:サービス ID アプリケーション サービスの構成
Windows Server 2012 でサービスを構成するには、次の機能に関するドキュメントを参照してください。

-   IIS アプリケーション プール

    詳細については、「 [アプリケーション プールの ID を指定する (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771170(v=ws.10))」を参照してください。

-   Windows サービス

    詳細については、「 [サービス](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772408(v=ws.11))」を参照してください。

-   [タスク]

    詳細については、「 [タスク スケジューラの概要](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc721871(v=ws.11))」を参照してください。

gMSA をサポートするサービスが他に存在する場合があります。 それらのサービスを構成する方法の詳細については、適切な製品ドキュメントを参照してください。

## <a name="adding-member-hosts-to-an-existing-server-farm"></a><a name="BKMK_AddMemberHosts"></a>既存のサーバー ファームへのメンバー ホストの追加
メンバーホストの管理にセキュリティグループを使用する場合は、次のいずれかの方法を使用して、新しいメンバーホストのコンピューターアカウントをセキュリティグループ (gMSA のメンバーホストがメンバーである) に追加します。

これらの手順を完了するには、[**Domain Admins**] のメンバーシップか、またはセキュリティ グループ オブジェクトにメンバーを追加する機能が最低限必要です。

-   方法 1:Active Directory ユーザーとコンピューター

    この方法を使用する手順については、Windows インターフェイスを使用した「 [コンピューター アカウントをグループに追加する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc733097(v=ws.11)) 」および「 [Active Directory 管理センターでさまざまなドメインを管理する](manage-different-domains-in-active-directory-administrative-center.md)」を参照してください。

-   方法 2: dsmod

    この方法を使用する手順については、コマンド ラインを使用した「 [コンピューター アカウントをグループに追加する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc733097(v=ws.11)) 」を参照してください。

-   方法 3:Windows PowerShell Active Directory コマンドレット Add-ADPrincipalGroupMembership

    この方法を使用する手順については、「 [Add-ADPrincipalGroupMembership](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617203(v=technet.10))」を参照してください。

コンピューター アカウントを使用する場合は、既存のアカウントを検索し、新しいコンピューター アカウントを追加します。

この手順を完了するには、[**Domain Admins**] または [**Account Operators**] のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを管理する権利が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「ローカルおよびドメインの既定のグループ」を参照してください。

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount コマンドレットを使用してメンバー ホストを追加するには

1.  Windows Server 2012 ドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **PrincipalsAllowedToRetrieveManagedPassword の取得-ADServiceAccount [-Identity] &lt; 文字列 &gt; のプロパティ**

3.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Set-ADServiceAccount [-Identity] &lt; string &gt; -PrincipalsAllowedToRetrieveManagedPassword <adprincipal [] >**

|パラメーター|String|例|
|-------|-----|------|
|名前|アカウントの名前|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|Host1、Host2、Host3|

**例**

たとえば、メンバー ホストを追加するには、次のコマンドを入力し、ENTER キーを押します。

```PowerShell
Get-ADServiceAccount [-Identity] ITFarm1 -Properties PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Identity] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host2$,Host3$
```

## <a name="updating-the-group-managed-service-account-properties"></a><a name="BKMK_Update_gMSA"></a>グループの管理されたサービスアカウントのプロパティを更新しています
これらの手順を完了するには、[**Domain Admins**] または [**Account Operators**] のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを書き込む権利が最低限必要です。

Windows PowerShell 用の Active Directory モジュールを開き、Set-ADServiceAccount コマンドレットを使用してプロパティを設定します。

これらのプロパティの設定方法の詳細については、TechNet ライブラリの「 [Set-ADServiceAccount](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617252(v=technet.10)) 」を参照してください。または、Windows PowerShell の Active Directory モジュールのコマンド プロンプトに「 **Get-Help Set-ADServiceAccount** 」と入力し、ENTER キーを押してください。

## <a name="decommissioning-member-hosts-from-an-existing-server-farm"></a><a name="BKMK_DecommMemberHosts"></a>既存のサーバー ファームからのメンバー ホストの使用停止
これらの手順を完了するには、[**Domain Admins**] のメンバーシップか、またはセキュリティ グループ オブジェクトからメンバーを削除する権利が最低限必要です。

### <a name="step-1-remove-member-host-from-gmsa"></a>手順 1:gMSA からメンバー ホストを削除する
メンバーホストの管理にセキュリティグループを使用する場合は、次のいずれかの方法を使用して、gMSA のメンバーホストがメンバーとなっているセキュリティグループから使用停止されたメンバーホストのコンピューターアカウントを削除します。

-   方法 1:Active Directory ユーザーとコンピューター

    この方法を使用する手順については、「 [Windows インターフェイスを使用してコンピューター アカウントを削除する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754624(v=ws.11)) 」および「 [Active Directory 管理センターでさまざまなドメインを管理する](manage-different-domains-in-active-directory-administrative-center.md)」を参照してください。

-   方法 2: drsm

    この方法を使用する手順については、「 [コマンド ラインを使用してコンピューター アカウントを削除する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754624(v=ws.11)) 」を参照してください。

-   方法 3:Windows PowerShell Active Directory コマンドレット Remove-ADPrincipalGroupMembership

    この方法の実行手順の詳細については、TechNet ライブラリの「  [Remove-ADPrincipalGroupMembership](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617243(v=technet.10)) 」を参照してください。あるいは、Windows PowerShell の Active Directory モジュールのコマンド プロンプトに「 **Get-Help Remove-ADPrincipalGroupMembership** 」と入力し、ENTER キーを押してください。

コンピューター アカウントを一覧する場合は、既存のコンピューター アカウントを検索し、削除されたものを除くすべてのコンピューター アカウントを追加します。

この手順を完了するには、[**Domain Admins**] または [**Account Operators**] のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを管理する権利が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「ローカルおよびドメインの既定のグループ」を参照してください。

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount コマンドレットを使用してメンバー ホストを削除するには

1.  Windows Server 2012 ドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **PrincipalsAllowedToRetrieveManagedPassword の取得-ADServiceAccount [-Identity] &lt; 文字列 &gt; のプロパティ**

3.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Set-ADServiceAccount [-Identity] &lt; string &gt; -PrincipalsAllowedToRetrieveManagedPassword <adprincipal [] >**

|パラメーター|String|例|
|-------|-----|------|
|名前|アカウントの名前|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|Host1、Host3|

**例**

たとえば、メンバー ホストを削除するには、次のコマンドを入力し、ENTER キーを押します。

```PowerShell
Get-ADServiceAccount [-Identity] ITFarm1 -Properties PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Identity] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host3$
```

### <a name="step-2-removing-a-group-managed-service-account-from-the-system"></a><a name="BKMK_RemoveGMSA"></a>手順 2:グループの管理されたサービス アカウントをシステムから削除する
ホスト システム上で Uninstall-ADServiceAccount または NetRemoveServiceAccount API を使用して、キャッシュされた gMSA 資格情報をメンバー ホストから削除します。

これらの手順を完了するには、[**Administrators**] のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>Uninstall-ADServiceAccount コマンドレットを使用して gMSA を削除するには

1.  Windows Server 2012 ドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **アンインストール-ADServiceAccount &lt; adserviceaccount&gt;**

    **例**

    たとえば、ITFarm1 という名前の gMSA のキャッシュされた資格情報を削除するには、次のコマンドを入力し、ENTER キーを押します。

    ```PowerShell
    Uninstall-ADServiceAccount ITFarm1
    ```

Uninstall-ADServiceAccount コマンドレットの詳細については、Windows PowerShell の Active Directory モジュールのコマンド プロンプトで、「 **Get-Help Uninstall-ADServiceAccount**」と入力し、ENTER キーを押すか、または TechNet Web の「 [Uninstall-ADServiceAccount](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617202(v=technet.10))」に掲載された情報を参照してください。



## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目

-   [グループの管理されたサービスアカウントの概要](group-managed-service-accounts-overview.md)