---
title: グループの管理されたサービス アカウントの概要
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6da212185eb47d3f30f81ca6f1eb322bc232e229
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881453"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>グループの管理されたサービス アカウントの概要

>適用先:Windows Server 2016 の Windows Server (半期チャネル)


このガイドは、有効にして、グループ管理サービス アカウントを使用して、Windows Server 2012 での手順および背景情報を提供します。

**このドキュメントで**

-   [前提条件](#BKMK_Prereqs)

-   [はじめに](#BKMK_Intro)

-   [新しいサーバー ファームを展開します。](#BKMK_DeployNewFarm)

-   [既存のサーバー ファームへのメンバー ホストを追加します。](#BKMK_AddMemberHosts)

-   [グループ管理サービス アカウント プロパティの更新](#BKMK_Update_gMSA)

-   [既存のサーバー ファームからのメンバー ホストを使用停止](#BKMK_DecommMemberHosts)


> [!NOTE]
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。

## <a name="BKMK_Prereqs"></a>前提条件
[グループの管理されたサービス アカウントの要件](#BKMK_gMSA_Req)については、このトピックのセクションを参照してください。

## <a name="BKMK_Intro"></a>概要
ネットワーク負荷分散 (NLB) (またはすべてのサーバーがクライアントに対して同じサービスを提供している) などの方式を使用しているサーバー ファームにホストされたサービスにクライアント コンピューターが接続するときに、サービスのすべてのインスタンスが同じプリンシパルを使用していない場合は、相互認証 (Kerberos など) をサポートする認証プロトコルを使用することはできません。 つまり、各サービスは同じパスワード/キーを使用して ID を証明する必要があります。

> [!NOTE]
> フェールオーバー クラスターでは、gMSA をサポートしていません。 ただし、クラスター サービスの上位で実行されるサービスは、それが Windows サービス、アプリケーション プール、またはスケジュールされたタスクである場合、あるいは gMSA/sMSA をネイティブにサポートしている場合、gMSA または sMSA を使用できます。

サービスは次のプリンシパルを選択肢として備えており、各プリンシパルには特定の制限があります。

|プリンシパル|Scope|サポートされるサービス|パスワード管理|
|-------|-----|-----------|------------|
|Windows システムのコンピューター アカウント|ドメイン|ドメインに参加している 1 つのサーバーに限定|コンピューターによる管理|
|Windows システムなしのコンピューター アカウント|ドメイン|ドメインに参加している任意のサーバー|なし|
|仮想アカウント|ローカル|1 つのサーバーに限定|コンピューターによる管理|
|Windows 7 スタンドアロンの管理されたサービス アカウント|ドメイン|ドメインに参加している 1 つのサーバーに限定|コンピューターによる管理|
|ユーザー アカウント|ドメイン|ドメインに参加している任意のサーバー|なし|
|グループ管理サービス アカウント|ドメイン|Windows Server 2012 ドメインに参加しているサーバー|ドメイン コントローラーによる管理、ホストによる取得|

Windows コンピューター アカウント、Windows 7 スタンドアロンの管理されたサービス アカウント (sMSA)、または仮想アカウントを複数のシステムで共有することはできません。 1 つのアカウントをサーバー ファームのサービスで共有するように構成する場合は、Windows システムとは別にユーザー アカウントまたはコンピューター アカウントを選択する必要があります。 いずれにしても、これらのアカウントには、シングルポイントコントロールでパスワードを管理する機能はありません。 このため問題が生じます。各組織は Active Directory のサービスのキーを更新してそのキーを該当するすべてのサービスのインスタンスに配布するために、コストの高いソリューションを作成する必要があります。

Windows Server 2012 では、サービスまたはサービス管理者必要はありませんグループ管理サービス アカウント (gMSA) を使用する場合、サービス インスタンス間のパスワード同期を管理します。 AD で gMSA をプロビジョニングし、管理されたサービス アカウントをサポートするサービスを構成します。 Active Directory モジュールに含まれる *-ADServiceAccount コマンドレットを使用して gMSA をプロビジョニングできます。 ホストでのサービス ID の構成は、次のものによってサポートされます。

-   sMSA と同じ API。したがって sMSA をサポートする製品は gMSA をサポートします。

-   サービス コントロール マネージャーを使用してログオン ID を構成するサービス。

-   アプリケーション プールに対応する IIS マネージャーを使用して ID を構成するサービス。

-   タスク スケジューラを使用するタスク。

### <a name="BKMK_gMSA_Req"></a>グループ管理サービス アカウントの要件
次の表に、Kerberos 認証が gMSA を使用してサービスを操作するための、オペレーティング システムの要件を一覧します。 表の後に Active Directory の要件を一覧します。

グループの管理されたサービス アカウントを管理するために使用する Windows PowerShell コマンドレットを実行するには 64 ビット アーキテクチャが必要です。

**オペレーティング システムの要件**

|要素|要件|オペレーティング システム|
|------|--------|----------|
|クライアント アプリケーション ホスト|RFC 準拠の Kerberos クライアント|Windows XP 以降|
|ユーザー アカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|共有されたサービス メンバー ホスト|| Windows Server 2012 |
|メンバー ホストのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|gMSA アカウントのドメイン Dc| Windows Server 2012 Dc のパスワードを取得するホストで使用できます。|一部のシステムを Windows Server 2012 より前に持つことができる Windows Server 2012 ドメイン |
|バックエンド サービス ホスト|RFC 準拠の Kerberos アプリケーション サーバー|Windows Server 2003 以降|
|バックエンド サービス アカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|Active Directory の Windows PowerShell|64 ビット アーキテクチャをサポートするコンピューターまたはリモート管理コンピューターにローカルにインストールされた Windows PowerShell for Active Directory (たとえば、リモート サーバー管理ツールキットを使用)| Windows Server 2012 |

**Active Directory ドメイン サービスの要件**

-   GMSA ドメインのフォレストの Active Directory スキーマは、gMSA を作成する Windows Server 2012 に更新する必要があります。

    Windows Server 2012 を実行するドメイン コント ローラーをインストールすることで、または Windows Server 2012 を実行しているコンピューターから adprep.exe のバージョンを実行してスキーマを更新することができます。 オブジェクト CN=Schema、CN=Configuration、DC=Contoso、DC=Com の object-version 属性値は 52 でなければなりません。

-   プロビジョニングされた新しい gMSA アカウント

-   グループ別に gMSA を使用するサービス ホストのアクセス許可を管理している場合は、新規または既存のセキュリティ グループ。

-   グループ別にサービス アクセス コントロールを管理する場合は、新規または既存のセキュリティ グループ。

-   Active Directory の最初のマスター ルート キーがドメインに展開されていない場合または作成されていない場合は、それを作成します。 作成した結果は、KdsSvc 操作ログ (Event ID 4004) で検証できます。

手順については、キーの参照を作成する方法[キー配布サービス KDS ルート キーの作成](create-the-key-distribution-services-kds-root-key.md)です。 Microsoft キー配布サービス (kdssvc.dll)、AD のルート キー。

**ライフ サイクル**

gMSA 機能を使用するサーバー ファームのライフサイクルは、通常、次のタスクを必要とします。

-   新しいサーバー ファームの展開

-   既存のサーバー ファームへのメンバー ホストの追加

-   既存のサーバー ファームからのメンバー ホストの使用停止

-   既存のサーバー ファームの使用停止

-   必要に応じて、セキュリティ侵害を受けているメンバー ホストをサーバー ファームから削除

## <a name="BKMK_DeployNewFarm"></a>新しいサーバー ファームを展開します。
新しいサーバー ファームを展開するとき、サービス管理者は次のことを決める必要があります。

-   サービスが gMSA の使用をサポートするかどうか

-   サービスが認証済みの受信接続または送信接続を必要とするかどうか

-   gMSA を使用するサービス用のメンバー ホストのコンピューター アカウント名

-   サービスの NetBIOS 名

-   サービスの DNS ホスト名

-   サービスのサービス プリンシパル名 (SPN)

-   パスワード変更間隔 (既定では 30 日)。

### <a name="BKMK_Step1"></a>手順 1:グループの管理されたサービス アカウントのプロビジョニング
Windows Server 2012 フォレストのスキーマが更新されました、Active Directory のマスター ルート キーが展開されて、および、gMSA を作成するドメイン内に少なくとも 1 つの Windows Server 2012 DC がある場合にのみ、gMSA を作成できます。

次の手順を完了するには、**[Domain Admins]** または **[Account Operators]** のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを作成する機能が最低限必要です。

#### <a name="BKMK_CreateGMSA"></a>New-adserviceaccount コマンドレットを使用して gMSA を作成するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell のコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します (Active Directory モジュールが自動的にロードされます)。

    **新しい ADServiceAccount [-名] <string> - DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < null 許容型は [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal>] - SamAccountName <string> ServicePrincipalNames < string[] >**

    |パラメーター|String|例|
    |-------|-----|------|
    |名前|アカウントの名前|ITFarm1|
    |DNSHostName|サービスの DNS ホスト名|ITFarm1.contoso.com|
    |KerberosEncryptionType|ホスト サーバーによってサポートされる暗号化の種類|RC4、AES128、AES256|
    |ManagedPasswordIntervalInDays|日単位のパスワード変更間隔 (指定がなければ既定では 30 日)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|ITFarmHosts|
    |SamAccountName|Name と同じでない場合はサービスの NetBIOS 名|ITFarm1|
    |ServicePrincipalNames|サービスのサービス プリンシパル名 (SPN)|http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso|

    > [!IMPORTANT]
    > パスワード変更間隔は作成時にしか設定できません。 パスワード変更間隔を変更する必要がある場合は、新しい gMSA を作成し、作成時にその間隔を設定してください。

    **例**

    コマンドレットを単一行に入力します。ただし、書式上の制約から複数行に改行されて表示される場合があります。

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

この手順を完了するには、**[Domain Admins]** または **[Account Operators]** のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを作成する機能が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「 [ローカルおよびドメインの既定のグループ](https://technet.microsoft.com/library/dd728026(WS.10).aspx)」を参照してください。

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>New-ADServiceAccount コマンドレットを使用して、送信の認証のみに gMSA を作成するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **New-ADServiceAccount [-Name] <string> -RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays <Nullable[Int32]>] [-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>]**

    |パラメーター|String|例|
    |-------|-----|------|
    |名前|アカウントの名前|ITFarm1|
    |ManagedPasswordIntervalInDays|日単位のパスワード変更間隔 (指定がなければ既定では 30 日)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|ITFarmHosts|

    > [!IMPORTANT]
    > パスワード変更間隔は作成時にしか設定できません。 パスワード変更間隔を変更する必要がある場合は、新しい gMSA を作成し、作成時にその間隔を設定してください。

**例**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>手順 2:サービス ID アプリケーション サービスの構成
Windows Server 2012 では、サービスを構成するには、次の機能ドキュメントを参照してください。

-   IIS アプリケーション プール

    詳細については、「 [アプリケーション プールの ID を指定する (IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx)」を参照してください。

-   Windows サービス

    詳細については、「 [サービス](https://technet.microsoft.com/library/cc772408.aspx)」を参照してください。

-   処理手順

    詳細については、「 [タスク スケジューラの概要](https://technet.microsoft.com/library/cc721871.aspx)」を参照してください。

gMSA をサポートするサービスが他に存在する場合があります。 それらのサービスを構成する方法の詳細については、適切な製品ドキュメントを参照してください。

## <a name="BKMK_AddMemberHosts"></a>既存のサーバー ファームへのメンバー ホストを追加します。
メンバー ホストを管理するためのセキュリティ グループを使用する場合は、セキュリティ グループ (gMSA のメンバー ホストのメンバーである) を新しいメンバー ホストのコンピューター アカウントを追加、次のメソッドのいずれかを使用します。

これらの手順を完了するには、**[Domain Admins]** のメンバーシップか、またはセキュリティ グループ オブジェクトにメンバーを追加する機能が最低限必要です。

-   方法 1:Active Directory ユーザーとコンピューター

    この方法を使用する手順については、Windows インターフェイスを使用した「 [コンピューター アカウントをグループに追加する](https://technet.microsoft.com/library/cc733097.aspx) 」および「 [Active Directory 管理センターでさまざまなドメインを管理する](manage-different-domains-in-active-directory-administrative-center.md)」を参照してください。

-   方法 2: dsmod

    この方法を使用する手順については、コマンド ラインを使用した「 [コンピューター アカウントをグループに追加する](https://technet.microsoft.com/library/cc733097.aspx) 」を参照してください。

-   方法 3:Windows PowerShell Active Directory コマンドレット Add-ADPrincipalGroupMembership

    この方法を使用する手順については、「 [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx)」を参照してください。

コンピューター アカウントを使用する場合は、既存のアカウントを検索し、新しいコンピューター アカウントを追加します。

この手順を完了するには、**[Domain Admins]** または **[Account Operators]** のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを管理する権利が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「ローカルおよびドメインの既定のグループ」を参照してください。

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount コマンドレットを使用してメンバー ホストを追加するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Get-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Set-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>**

|パラメーター|String|例|
|-------|-----|------|
|名前|アカウントの名前|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|Host1、Host2、Host3|

**例**

たとえば、メンバー ホストを追加するには、次のコマンドを入力し、ENTER キーを押します。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1,Host2,Host3

```

## <a name="BKMK_Update_gMSA"></a>グループ管理されたサービス アカウントのプロパティを更新しています
これらの手順を完了するには、**[Domain Admins]** または **[Account Operators]** のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを書き込む権利が最低限必要です。

Windows PowerShell 用の Active Directory モジュールを開き、Set-ADServiceAccount コマンドレットを使用してプロパティを設定します。

これらのプロパティの設定方法の詳細については、TechNet ライブラリの「 [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) 」を参照してください。または、Windows PowerShell の Active Directory モジュールのコマンド プロンプトに「 **Get-Help Set-ADServiceAccount** 」と入力し、ENTER キーを押してください。

## <a name="BKMK_DecommMemberHosts"></a>既存のサーバー ファームからのメンバー ホストを使用停止
これらの手順を完了するには、**[Domain Admins]** のメンバーシップか、またはセキュリティ グループ オブジェクトからメンバーを削除する権利が最低限必要です。

### <a name="step-1-remove-member-host-from-gmsa"></a>手順 1:gMSA からメンバー ホストを削除する
メンバー ホストを管理するためのセキュリティ グループを使用する場合は、gMSA のメンバー ホストを使用して、次のいずれかのメンバーであること、セキュリティ グループから、使用停止されたメンバー ホストのコンピューター アカウントを削除します。

-   方法 1:Active Directory ユーザーとコンピューター

    この方法を使用する手順については、「 [Windows インターフェイスを使用してコンピューター アカウントを削除する](https://technet.microsoft.com/library/cc754624.aspx) 」および「 [Active Directory 管理センターでさまざまなドメインを管理する](manage-different-domains-in-active-directory-administrative-center.md)」を参照してください。

-   方法 2: drsm

    この方法を使用する手順については、「 [コマンド ラインを使用してコンピューター アカウントを削除する](https://technet.microsoft.com/library/cc754624.aspx) 」を参照してください。

-   方法 3:Windows PowerShell Active Directory コマンドレット Remove-ADPrincipalGroupMembership

    この方法の実行手順の詳細については、TechNet ライブラリの「  [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) 」を参照してください。あるいは、Windows PowerShell の Active Directory モジュールのコマンド プロンプトに「 **Get-Help Remove-ADPrincipalGroupMembership** 」と入力し、ENTER キーを押してください。

コンピューター アカウントを一覧する場合は、既存のコンピューター アカウントを検索し、削除されたものを除くすべてのコンピューター アカウントを追加します。

この手順を完了するには、**[Domain Admins]** または **[Account Operators]** のメンバーシップ、あるいは msDS-GroupManagedServiceAccount オブジェクトを管理する権利が最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「ローカルおよびドメインの既定のグループ」を参照してください。

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount コマンドレットを使用してメンバー ホストを削除するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Get-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Set-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>**

|パラメーター|String|例|
|-------|-----|------|
|名前|アカウントの名前|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのコンピューター アカウントまたはメンバー ホストが属するセキュリティ グループ|Host1、Host3|

**例**

たとえば、メンバー ホストを削除するには、次のコマンドを入力し、ENTER キーを押します。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1,Host3

```

### <a name="BKMK_RemoveGMSA"></a>手順 2:グループの管理されたサービス アカウントをシステムから削除する
ホスト システム上で Uninstall-ADServiceAccount または NetRemoveServiceAccount API を使用して、キャッシュされた gMSA 資格情報をメンバー ホストから削除します。

これらの手順を完了するには、**[Administrators]** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>Uninstall-ADServiceAccount コマンドレットを使用して gMSA を削除するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Uninstall-adserviceaccount < ADServiceAccount >**

    **例**

    たとえば、ITFarm1 という名前の gMSA のキャッシュされた資格情報を削除するには、次のコマンドを入力し、ENTER キーを押します。

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Uninstall-ADServiceAccount コマンドレットの詳細については、Windows PowerShell の Active Directory モジュールのコマンド プロンプトで、「 **Get-Help Uninstall-ADServiceAccount**」と入力し、ENTER キーを押すか、または TechNet Web の「 [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx)」に掲載された情報を参照してください。



## <a name="BKMK_Links"></a>参照してください。

-   [グループ管理サービス アカウントの概要](group-managed-service-accounts-overview.md)



