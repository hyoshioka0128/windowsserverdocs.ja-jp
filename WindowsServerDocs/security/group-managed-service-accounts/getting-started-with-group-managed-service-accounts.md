---
title: "管理されたサービス アカウントをグループの概要"
description: "Windows Server のセキュリティ"
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
ms.openlocfilehash: cd1e92f93701e5b430d1425fcf9a2f3590d1fe5d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="getting-started-with-group-managed-service-accounts"></a>管理されたサービス アカウントをグループの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016


このガイドは、有効にすると、グループ管理サービス アカウントを使用して、Windows Server 2012 で詳細な手順および背景情報を提供します。

**このドキュメントで**

-   [前提条件](#BKMK_Prereqs)

-   [概要](#BKMK_Intro)

-   [新しいサーバー ファームを展開します。](#BKMK_DeployNewFarm)

-   [既存のサーバー ファームへのメンバー ホストを追加します。](#BKMK_AddMemberHosts)

-   [グループの管理されたサービス アカウントのプロパティを更新](#BKMK_Update_gMSA)

-   [既存のサーバー ファームからメンバー ホストの使用停止](#BKMK_DecommMemberHosts)


> [!NOTE]
> このトピックには、説明する手順の一部を自動化するのに使用できるサンプル Windows PowerShell コマンドレットが含まれています。 詳細については、次を参照してください。[コマンドレットを使用した](https://go.microsoft.com/fwlink/p/?linkid=230693)します。

## <a name="BKMK_Prereqs"></a>前提条件
このトピックのセクションを参照して[グループ管理サービス アカウントに関する要件](#BKMK_gMSA_Req)します。

## <a name="BKMK_Intro"></a>概要
クライアント コンピューターは、サーバー ファームのネットワーク負荷分散 (NLB) またはその他の方法を使用してすべてのサーバーがクライアントに同じサービスのように表示される場所でホストされるサービスに接続するときに、Kerberos などの相互認証をサポートする認証プロトコルは使用できません、サービスのすべてのインスタンスが同じプリンシパルを使用していない場合。 これは、自分の身元を証明するために同じパスワード/キーを使用する各サービスがあることを意味します。

> [!NOTE]
> フェールオーバー クラスターは、Gmsa をサポートしていません。 ただし、クラスタ サービス上で実行されるサービスが Windows サービス、アプリケーション プール、スケジュールされたタスクや gMSA または sMSA をネイティブでサポート、gMSA または sMSA を使用できます。

次のプリンシパルを選択すると、サービス、各は制限事項があります。

|プリンシパル|スコープ|サポートされているサービス|パスワード管理|
|-------|-----|-----------|------------|
|コンピューター アカウントの Windows のシステム|ドメイン|1 つのドメインに制限されます。 には、サーバーが参加しています。|コンピューターを管理します。|
|Windows システムなしのコンピューター アカウント|ドメイン|任意のドメインに参加しているサーバー|[なし]|
|仮想アカウント|地元の|1 台のサーバーに制限されます。|コンピューターを管理します。|
|Windows 7 スタンドアロンの管理されたサービス アカウント|ドメイン|1 つのドメインに制限されます。 には、サーバーが参加しています。|コンピューターを管理します。|
|ユーザー アカウント|ドメイン|任意のドメインに参加しているサーバー|[なし]|
|グループの管理されたサービス アカウント|ドメイン|Windows Server 2012 ドメインに参加しているサーバー|ドメイン コント ローラーを管理していると、ホストによる取得|

Windows コンピューター アカウント、または Windows 7 スタンドアロンの管理されたサービス アカウント (sMSA)、または仮想アカウントは、複数のシステムで共有することはできません。 共有するサーバー ファームのサービスの 1 つのアカウントを構成する場合は、ユーザー アカウントまたは Windows システムとは別のコンピューター アカウントを選択する必要があります。 いずれにしても、これらのアカウントでは、シングル ポイント コントロールのパスワード管理の機能を必要はありません。 これは、各組織が Active Directory で、サービスのキーを更新し、それらのサービスのすべてのインスタンスへのキーを配布するコストが高いソリューションを作成する必要がある問題を作成します。

Windows Server 2012 では、サービス自体もサービス管理者する必要はありませんグループ管理サービス アカウント (gMSA) を使用する場合、サービス インスタンス間のパスワード同期を管理します。 AD で gMSA をプロビジョニングし、[管理されたサービス アカウントをサポートしているサービスを構成します。 使用して gMSA をプロビジョニングすることができます、*-Active Directory モジュールの一部である-adserviceaccount コマンドレット。 によって、ホスト上のサービス id の構成がサポートされます。

-   SMSA と同じ Api sMSA をサポートするための製品は gMSA をサポートします。

-   サービス コントロール マネージャを使用してログオン id を構成するサービス

-   サービス id を構成するアプリケーション プールの IIS マネージャーを使用しています。

-   タスクはタスク スケジューラを使用します。

### <a name="BKMK_gMSA_Req"></a>グループ管理サービス アカウントに関する要件
次の表は、gMSA を使用してサービスを使用する Kerberos 認証用のオペレーティング システムの要件を示します。 Active Directory の要件は、表の後に一覧表示されます。

グループ管理サービス アカウントを管理するために使用する Windows PowerShell コマンドを実行するには、64 ビット アーキテクチャが必要です。

**オペレーティング システムの要件**

|要素|要件|オペレーティング システム|
|------|--------|----------|
|クライアント アプリケーション ホスト|RFC 準拠の Kerberos クライアント|Windows XP 以降|
|ユーザー アカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|共有サービス メンバー ホスト|| Windows Server 2012 |
|メンバー ホストのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|gMSA アカウントのドメイン Dc| Windows Server 2012 Dc のパスワードを取得するホストで使用できます。|Windows Server 2012 が与える可能性がいくつかのシステムを Windows Server 2012 より前のドメイン |
|バックエンド サービス ホスト|RFC 準拠の Kerberos アプリケーション サーバー|Windows Server 2003 以降|
|バックエンド サービス アカウントのドメイン Dc|RFC 準拠の KDC|Windows Server 2003 以降|
|Active Directory 用 Windows PowerShell|64 ビット アーキテクチャをサポートするコンピューターまたはリモート管理コンピューター (この例では、リモート サーバー管理ツールキットを使用して) ローカルにインストールされている Active Directory 用 Windows PowerShell| Windows Server 2012 |

**Active Directory ドメイン サービスの要件**

-   GMSA ドメインのフォレストで Active Directory スキーマは、gMSA を作成する Windows Server 2012 に更新する必要があります。

    Windows Server 2012 を実行するドメイン コント ローラーをインストールすることによって、または Windows Server 2012 を実行しているコンピューターから adprep.exe のバージョンを実行して、スキーマを更新することができます。 オブジェクト バージョン オブジェクトの属性値、CN = Schema, CN = Configuration, DC = Contoso, DC = Com は 52 でなければなりません。

-   プロビジョニングされた新しい gMSA アカウント

-   グループで、新規または既存のセキュリティ グループ別に gMSA を使用するサービス ホストのアクセス許可を管理している場合

-   サービス アクセス コントロールをグループ、し、新規または既存のセキュリティ グループを管理している場合

-   Active Directory の最初のマスター ルート キーが、ドメインが展開されていないか、または作成されていない場合は、それを作成します。 その作成した結果は、KdsSvc 操作ログには、イベント ID 4004 検証できます。

手順については、キーの参照を作成する方法[キー配布サービス KDS ルート キーの作成](create-the-key-distribution-services-kds-root-key.md)します。 Microsoft キー配布サービス (kdssvc.dll) されたルート キーの広告のします。

**ライフ サイクル**

通常、gMSA 機能を使用するサーバー ファームのライフ サイクルには、次のタスクが含まれます。

-   新しいサーバー ファームを展開します。

-   既存のサーバー ファームへのメンバー ホストを追加します。

-   既存のサーバー ファームからメンバー ホストの使用停止

-   既存のサーバー ファームを使用停止

-   必要な場合は、侵害されたメンバー ホスト サーバー ファームから削除しています。

## <a name="BKMK_DeployNewFarm"></a>新しいサーバー ファームを展開します。
で新しいサーバー ファームを展開する場合、サービス管理者を決定する必要があります。

-   Gmsa を使用して、サービスがサポートされている場合

-   サービスが受信または送信の認証接続が必要な場合

-   GMSA を使用して、サービス用のメンバー ホストのコンピューター アカウント名

-   サービスの NetBIOS 名

-   サービスの DNS ホスト名

-   サービスのサービス プリンシパル名 (Spn)

-   パスワード変更間隔 (既定では 30 日間)。

### <a name="BKMK_Step1"></a>手順 1: グループの管理されたサービス アカウントをプロビジョニングします。
Windows Server 2012 フォレストのスキーマが更新され、Active Directory のマスター ルート キーが展開されていて、および gMSA を作成するドメイン内に少なくとも 1 つの Windows Server 2012 DC がある場合にのみ、gMSA を作成することができます。

メンバーシップ**Domain Admins**、 **Account Operators** Msds-groupmanagedserviceaccount オブジェクトを作成する機能が次の手順を完了するために必要な最低限またはします。

#### <a name="BKMK_CreateGMSA"></a>New-adserviceaccount コマンドレットを使用して gMSA を作成するには

1.  Windows Server 2012 ドメイン コント ローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、し、ENTER キーを押します。 (Active Directory モジュールが自動的にロードします。)

    **新しい ADServiceAccount [-名] <string> - DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < [Int32] null 値 >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal >] - SamAccountName <string> ServicePrincipalNames < string[] >**

    |パラメーター|文字列|使用例|
    |-------|-----|------|
    |名|アカウントの名前|ITFarm1|
    |DNSHostName|サービスの DNS ホスト名|ITFarm1.contoso.com|
    |KerberosEncryptionType|ホスト サーバーでサポートされている暗号化の種類|RC4、AES128、AES256|
    |ManagedPasswordIntervalInDays|(既定値は 30 日間いない場合提供されている) 日以内にパスワード変更間隔|90|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのセキュリティ グループのメンバーであるメンバー ホストをコンピューター アカウント|ITFarmHosts|
    |Sam アカウント名|されていない場合に、サービスの NetBIOS 名の名前と同じ|ITFarm1|
    |ServicePrincipalNames|サービスのサービス プリンシパル名 (Spn)|http/ITFarm1.contoso.com/contoso.com、http/ITFarm1.contoso.com/contoso、http/ITFarm1/contoso.com、http/ITFarm1/contoso|

    > [!IMPORTANT]
    > パスワード変更間隔は、作成時にのみ設定できます。 間隔を変更する場合は、新しい gMSA を作成および作成時に設定する必要があります。

    **使用例**

    表示される場合でも可能性があります複数行に改行書式上の制約のために、1 つの行に、コマンドを入力します。

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

メンバーシップ**Domain Admins**、 **Account Operators**、Msds-groupmanagedserviceaccount オブジェクトを作成する機能がこの手順を完了するために必要な最低限またはします。 For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>New-adserviceaccount コマンドレットを使用してのみ、送信の認証の gMSA を作成するには

1.  Windows Server 2012 ドメイン コント ローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **新しい ADServiceAccount [-名] <string> - RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < [Int32] 許容 >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal >]**

    |パラメーター|文字列|使用例|
    |-------|-----|------|
    |名|アカウントを名前します。|ITFarm1|
    |ManagedPasswordIntervalInDays|(既定値は 30 日間いない場合提供されている) 日以内にパスワード変更間隔|75|
    |PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのセキュリティ グループのメンバーであるメンバー ホストをコンピューター アカウント|ITFarmHosts|

    > [!IMPORTANT]
    > パスワード変更間隔は、作成時にのみ設定できます。 間隔を変更する場合は、新しい gMSA を作成および作成時に設定する必要があります。

**使用例**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>手順 2: サービス id アプリケーション サービスを構成します。
Windows Server 2012 でサービスを構成するには、次の機能に関するドキュメントを参照してください。

-   IIS アプリケーション プール

    詳細については、次を参照してください。 [(IIS 7) アプリケーション プールの Id を指定](https://technet.microsoft.com/library/cc771170(WS.10).aspx)します。

-   Windows サービス

    詳細については、次を参照してください。[サービス](https://technet.microsoft.com/library/cc772408.aspx)します。

-   タスク

    詳細については、次を参照してください。、[タスク スケジューラの概要](https://technet.microsoft.com/library/cc721871.aspx)します。

その他のサービスは、gMSA をサポート可能性があります。 これらのサービスを構成する方法の詳細については、適切な製品ドキュメントを参照してください。

## <a name="BKMK_AddMemberHosts"></a>既存のサーバー ファームへのメンバー ホストを追加します。
メンバー ホストを管理するためのセキュリティ グループを使用する場合は、セキュリティ グループ (gMSA のメンバー ホストのメンバーである) を新しいメンバー ホストのコンピューター アカウントを追加、次の方法のいずれかを使用します。

メンバーシップ**Domain Admins**、またはセキュリティ グループ オブジェクトにメンバーを追加する機能がこれらの手順を完了するために必要な最小値。

-   方法 1: Active Directory ユーザーとコンピューター

    手順についてを参照してください、このメソッドを使用する方法[をグループにコンピューター アカウントを追加](https://technet.microsoft.com/library/cc733097.aspx)、Windows インターフェイスを使用してと[Active Directory 管理センターでさまざまなドメインを管理](manage-different-domains-in-active-directory-administrative-center.md)します。

-   方法 2: dsmod

    手順についてを参照してください、このメソッドを使用する方法[をグループにコンピューター アカウントを追加](https://technet.microsoft.com/library/cc733097.aspx)コマンドラインを使用します。

-   方法 3: Windows PowerShell の Active Directory コマンドレット Add-adprincipalgroupmembership

    手順についてを参照してください、このメソッドを使用する方法[Add-adprincipalgroupmembership](https://technet.microsoft.com/library/ee617203.aspx)します。

コンピューター アカウントを使用している場合は、既存のアカウントを見つけて、新しいコンピューター アカウントを追加します。

メンバーシップ**Domain Admins**、 **Account Operators**、または、Msds-groupmanagedserviceaccount オブジェクトを管理する機能が最低限のこの手順を実行する必要です。 適切なアカウントおよびグループ メンバーシップの使用に関する詳細については、ローカルおよびドメインの既定のグループを参照してください。

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-adserviceaccount コマンドレットを使用してメンバー ホストを追加するには

1.  Windows Server 2012 ドメイン コント ローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Get-adserviceaccount [-名] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Set-adserviceaccount [-名] <string> PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [>**

|パラメーター|文字列|使用例|
|-------|-----|------|
|名|アカウントを名前します。|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのセキュリティ グループのメンバーであるメンバー ホストをコンピューター アカウント|Host1、Host2、Host3|

**使用例**

たとえば、メンバーを追加するホストが、次のコマンドを入力およびし、ENTER キーを押します。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1 Host2 Host3

```

## <a name="BKMK_Update_gMSA"></a>グループの管理されたサービス アカウントのプロパティを更新します。
メンバーシップ**Domain Admins**、 **Account Operators**、する機能、Msds-groupmanagedserviceaccount オブジェクトへの書き込みは、これらの手順を完了するために必要な最低限またはします。

Active Directory モジュールの Windows PowerShell を開き、Set-adserviceaccount コマンドレットを使用して任意のプロパティを設定します。

参照してください、これらのプロパティを設定する方法の詳細について[Set-adserviceaccount](https://technet.microsoft.com/library/ee617252.aspx)または」と入力して、TechNet ライブラリで**Get-help Set-adserviceaccount** Windows PowerShell の Active Directory モジュールのコマンド プロンプトとキーを押して入力します。

## <a name="BKMK_DecommMemberHosts"></a>既存のサーバー ファームからメンバー ホストの使用停止
メンバーシップ**Domain Admins**、または、セキュリティ グループ オブジェクトからメンバーを削除する権利が最低限のこれらの手順を完了するために必要です。

### <a name="step-1-remove-member-host-from-gmsa"></a>手順 1: gMSA からメンバー ホストを削除します。
メンバー ホストを管理するためのセキュリティ グループを使用する場合は、gMSA のメンバー ホストを使用して、次のいずれかのメンバーであること、セキュリティ グループから、使用停止されたメンバー ホストのコンピューター アカウントを削除します。

-   方法 1: Active Directory ユーザーとコンピューター

    手順についてを参照してください、このメソッドを使用する方法[コンピューター アカウントを削除](https://technet.microsoft.com/library/cc754624.aspx)、Windows インターフェイスを使用してと[Active Directory 管理センターでさまざまなドメインを管理](manage-different-domains-in-active-directory-administrative-center.md)します。

-   方法 2: drsm

    手順についてを参照してください、このメソッドを使用する方法[コンピューター アカウントを削除](https://technet.microsoft.com/library/cc754624.aspx)コマンドラインを使用します。

-   方法 3: Windows PowerShell の Active Directory コマンドレット Remove-adprincipalgroupmembership

    方法の詳細についてを参照してください[Remove-adprincipalgroupmembership](https://technet.microsoft.com/library/ee617243.aspx)または」と入力して、TechNet ライブラリで**Get-help Remove-adprincipalgroupmembership** Windows PowerShell の Active Directory モジュールのコマンド プロンプトとキーを押して入力します。

コンピューター アカウントを一覧表示する、既存のアカウントを取得しを除くすべてのコンピューターの削除アカウントを追加します。

メンバーシップ**Domain Admins**、 **Account Operators**、または、Msds-groupmanagedserviceaccount オブジェクトを管理する機能が最低限のこの手順を実行する必要です。 適切なアカウントおよびグループ メンバーシップの使用に関する詳細については、ローカルおよびドメインの既定のグループを参照してください。

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-adserviceaccount コマンドレットを使用してメンバー ホストを削除するには

1.  Windows Server 2012 ドメイン コント ローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Get-adserviceaccount [-名] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Set-adserviceaccount [-名] <string> PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [>**

|パラメーター|文字列|使用例|
|-------|-----|------|
|名|アカウントを名前します。|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|メンバー ホストのセキュリティ グループのメンバーであるメンバー ホストをコンピューター アカウント|Host1、Host3|

**使用例**

たとえば、メンバーを削除するホストが、次のコマンドを入力およびし、ENTER キーを押します。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1 Host3

```

### <a name="BKMK_RemoveGMSA"></a>手順 2: システムからグループの管理されたサービス アカウントを削除します。
ホスト システム上で Uninstall-adserviceaccount または NetRemoveServiceAccount API を使用してメンバー ホストからキャッシュされた gMSA 資格情報を削除します。

メンバーシップ**管理者**、またはそれと同等がこれらの手順を完了するために必要な最小値。

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>Uninstall-adserviceaccount コマンドレットを使用して gMSA を削除するには

1.  Windows Server 2012 ドメイン コント ローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Uninstall-adserviceaccount < ADServiceAccount >**

    **使用例**

    やなどの gMSA のキャッシュされた資格情報を削除する ITFarm1 という名前、次のコマンドを入力し、ENTER キーを押します。

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Windows PowerShell コマンド プロンプトでの Active Directory モジュール、Uninstall-adserviceaccount コマンドレットの詳細については次のように入力します。 **Get-help Uninstall-adserviceaccount**、し、ENTER キーを押しますまたは TechNet web サイトに情報を参照してください[Uninstall-adserviceaccount](https://technet.microsoft.com/library/ee617202.aspx)します。



## <a name="BKMK_Links"></a>参照してください。

-   [グループの管理されたサービス アカウントの概要](group-managed-service-accounts-overview.md)



