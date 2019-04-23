---
title: ユーザー アクセス制御とアクセス許可を構成します。
description: ユーザー アクセス制御と Active Directory または Azure AD (プロジェクト ホノルル) を使用してアクセス許可を構成する方法について説明します
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/19/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b19657f4ce1a1a2cfb94f7234f07805ba0abd42c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850573"
---
# <a name="configure-user-access-control-and-permissions"></a>ユーザー アクセス制御とアクセス許可を構成します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

まだインストールしていない場合について理解するおくと、 [Windows Admin Center でユーザー アクセス制御オプション](../plan/user-access-options.md)

>[!NOTE]
> ワークグループ環境で、または信頼されていないドメイン間では、Windows Admin Center でのグループ ベースのアクセスはサポートされていません。

## <a name="gateway-access-role-definitions"></a>ゲートウェイへのアクセス ロールの定義

これには、Windows Admin Center ゲートウェイ サービスにアクセスするための 2 つのロールがあります。

**ゲートウェイのユーザー** 、そのゲートウェイを介してサーバーを管理する Windows Admin Center ゲートウェイ サービスに接続できますが、アクセス許可も、ゲートウェイへの認証に使用する認証メカニズムは変更できません。

**ゲートウェイ管理者**へのアクセスを取得したゲートウェイにユーザーを認証する方法を構成することができます。 ゲートウェイの管理者だけでは、表示でき、Windows Admin Center でのアクセス設定を構成することができます。 ゲートウェイ コンピューター上のローカル管理者は、常に、Windows Admin Center ゲートウェイ サービスの管理者です。

> [!NOTE]
> ゲートウェイへのアクセスは、ゲートウェイが表示される管理対象のサーバーへのアクセスのことを意味しません。 ターゲット サーバーを管理する接続のユーザーが資格情報を使用する必要があります (そのを通じて渡される Windows 資格情報と、Windows Admin Center を使用してセッションで指定された資格情報、**として管理**アクション) があります。ターゲット サーバーへの管理アクセス。

## <a name="active-directory-or-local-machine-groups"></a>Active Directory またはローカル コンピューターのグループ

既定では、Active Directory またはローカル コンピューターのグループがゲートウェイへのアクセス制御に使用されます。 ゲートウェイのユーザーと管理者を管理することができる場合は、Active Directory ドメインがある場合は、Windows Admin Center インターフェイス内からアクセスします。

**ユーザー**ゲートウェイのユーザーとして Windows Admin Center にアクセスできるユーザーを制御できます タブ。 既定では、セキュリティ グループを指定しない場合、ゲートウェイの URL にアクセスするすべてのユーザーがアクセス権を持ちます。 1 つまたは複数のセキュリティ グループをユーザーの一覧に追加すると、アクセスは、それらのグループのメンバーに制限されます。

によってアクセスを制御環境内で Active Directory ドメインを使用しない場合、```Users```と```Administrators```Windows Admin Center ゲートウェイ コンピューター上のローカル グループです。

### <a name="smartcard-authentication"></a>スマート カード認証

適用できます**スマート カード認証**追加を指定して_必要_スマート カード ベースのセキュリティ グループのグループ。 スマート カード ベースのセキュリティ グループを追加した後は、任意のセキュリティ グループのメンバーになっていると、スマート カードのグループがユーザーの一覧に含まれている場合、ユーザーはのみ、Windows Admin Center サービスをアクセスできます。

**管理者**ゲートウェイ管理者として Windows Admin Center にアクセスできるユーザーを制御できます タブ。 コンピューターのローカルの administrators グループは完全な管理者アクセスは常にし、一覧から削除できません。 セキュリティ グループを追加すると、Windows Admin Center ゲートウェイ設定を変更する特権グループのメンバーを提供します。 管理者の一覧は、ユーザーの一覧と同じ方法でスマート カード認証をサポートしています。 スマート カードのグループとセキュリティ グループに対して AND 条件とします。

## <a name="azure-active-directory"></a>Azure Active Directory

組織は、Azure Active Directory (Azure AD) を使用している場合は、追加することもできます、**追加**ゲートウェイにアクセスする Azure AD 認証を要求することで、Windows Admin Center にセキュリティのレイヤー。 Windows Admin Center、ユーザーのアクセスするために**Windows アカウント**(Azure AD 認証を使用) 場合でも、ゲートウェイ サーバーへのアクセスを権も必要です。 内からではなく、Azure Portal から、Windows Admin Center のユーザーと管理者のアクセス許可を管理するが Azure AD を使用すると、Windows Admin Center UI。

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 認証を有効にする Windows Admin Center へのアクセス

一部のユーザーが構成されている Azure AD 認証を使用した Windows Admin Center へのアクセス、ブラウザーを使用すると、によって、追加のプロンプトが表示されます**ブラウザーから**のために Windows アカウント資格情報を提供する必要がありますWindows Admin Center がインストールされているコンピューター。 その情報を入力した後、ユーザーが Azure での Azure AD アプリケーションでのアクセスが付与されている Azure アカウントの資格情報が必要追加 Azure Active Directory 認証プロンプトが表示されます。

> [!NOTE]
> Windows のユーザー アカウントが**管理者権限**ゲートウェイ上でマシンは求められません Azure AD 認証。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows Admin Center プレビューの Azure Active Directory 認証を構成します。

Windows Admin Center に移動して**設定** > **アクセス**トグル スイッチを使用して有効にして"を使用して、ゲートウェイにセキュリティ レイヤーを追加する Azure Active Directory"。 Azure へのゲートウェイを登録していない場合、この時点でそのは説明します。

既定では、Azure AD テナントのすべてのメンバーは、Windows Admin Center ゲートウェイ サービスに対するユーザー アクセスを必要です。 ゲートウェイ コンピューターのローカル管理者のみでは、Windows Admin Center ゲートウェイへの管理者アクセスがあります。 ゲートウェイ コンピューター上のローカル管理者の権限を制限することはできません - ローカルの管理者には、認証に Azure AD を使用するかどうかに関係なく何も実行できますに注意してください。

特定の Azure AD ユーザーまたはグループのゲートウェイのユーザーまたは Windows Admin Center サービスへのゲートウェイの管理者アクセスする場合は、次の操作を行う必要があります。

1.  アクセス設定で提供されるハイパーリンクを使用して、Azure portal で、Windows Admin Center の Azure AD アプリケーションに移動します。 このハイパーリンクは、Azure Active Directory 認証が有効になっている場合にのみ使用可能なに注意してください。 
    -   移動して、Azure portal でアプリケーションを検索することもできます**Azure Active Directory** > **エンタープライズ アプリケーション** > **のすべてのアプリケーション**と検索**WindowsAdminCenter** (Azure AD アプリの名前は WindowsAdminCenter-<gateway name>)。 検索結果を得られない場合は、以下のことを確認**表示**に設定されている**すべてのアプリケーション**、**アプリケーション状態**に設定されている**任意**適用、 をクリック検索を再試行してください。 アプリケーションが見つかったらに移動して**ユーザーとグループ**
2.  [プロパティ] タブで、次のように設定します。**ユーザー割り当てが必要**[はい] にします。
    これが完了したら、したらにはメンバーだけが一覧表示、**ユーザーとグループ** タブは、Windows Admin Center ゲートウェイにアクセスできます。
3.  ユーザーとグループ タブでは、次のように選択します。**ユーザーの追加**します。 ゲートウェイのユーザーまたは各ユーザー/グループがその追加のゲートウェイの管理者ロールを割り当てる必要があります。

Azure AD 認証を有効にすると、ゲートウェイ サービスが再起動しては、ブラウザーを更新する必要があります。 いつでも、Azure portal で Azure AD の SME アプリケーションのユーザー アクセスを更新することができます。

ユーザーは、Windows Admin Center ゲートウェイの URL へのアクセスを試みるときに、Azure Active Directory id を使用してサインインを求められます。 ユーザー Windows Admin Center にアクセスするゲートウェイ サーバー上のローカル ユーザーのメンバーでもあることに注意してください。

ユーザーと管理者が、現在のログイン アカウントを表示およびからは、この Azure AD アカウントのも、サインアウト、**アカウント**Windows Admin Center の設定のタブ。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows Admin Center を Azure Active Directory 認証を構成します。

[Azure AD 認証を設定するにする必要があります最初に、ゲートウェイを Azure に登録](azure-integration.md)(だけこれを 1 回、Windows Admin Center ゲートウェイを実行する必要があります)。 この手順では、ゲートウェイのユーザーとゲートウェイの管理者アクセスを管理できる Azure AD アプリケーションを作成します。

特定の Azure AD ユーザーまたはグループのゲートウェイのユーザーまたは Windows Admin Center サービスへのゲートウェイの管理者アクセスする場合は、次の操作を行う必要があります。

1.  Azure portal で Azure AD の SME アプリケーションに移動します。 
    -   クリックすると**変更アクセス制御**選び**Azure Active Directory** Windows Admin Center へのアクセスの設定から、Azure AD へのアクセスに、UI で提供されるハイパーリンクを使用することができますAzure portal でのアプリケーションです。 このハイパーリンクは、保存 をクリックし、アクセス コントロールの id プロバイダーとして Azure AD を選択した後にも、アクセスの設定で使用できます。
    -   移動して、Azure portal でアプリケーションを検索することもできます**Azure Active Directory** > **エンタープライズ アプリケーション** > **のすべてのアプリケーション**と検索**SME** (Azure AD アプリの名前は SME-<gateway>)。 検索結果を得られない場合は、以下のことを確認**表示**に設定されている**すべてのアプリケーション**、**アプリケーション状態**に設定されている**任意**適用、 をクリック検索を再試行してください。 アプリケーションが見つかったらに移動して**ユーザーとグループ**
2.  [プロパティ] タブで、次のように設定します。**ユーザー割り当てが必要**[はい] にします。
    これが完了したら、したらにはメンバーだけが一覧表示、**ユーザーとグループ** タブは、Windows Admin Center ゲートウェイにアクセスできます。
3.  ユーザーとグループ タブでは、次のように選択します。**ユーザーの追加**します。 ゲートウェイのユーザーまたは各ユーザー/グループがその追加のゲートウェイの管理者ロールを割り当てる必要があります。

保存すると、Azure AD でのアクセス制御、**変更アクセス制御**ウィンドウで、ゲートウェイ サービスを再起動して、ブラウザーを更新する必要があります。 いつでも、Azure portal で、Windows Admin Center の Azure AD アプリケーションのユーザー アクセスを更新することができます。 

ユーザーは、Windows Admin Center ゲートウェイの URL へのアクセスを試みるときに、Azure Active Directory id を使用してサインインを求められます。 ユーザー Windows Admin Center にアクセスするゲートウェイ サーバー上のローカル ユーザーのメンバーでもあることに注意してください。 

使用して、 **Azure** Windows Admin Center の 全般設定、ユーザーおよび管理者のタブは、現在のログイン アカウントを表示できますとも、この Azure AD アカウントのようにサインアウトします。

### <a name="conditional-access-and-multi-factor-authentication"></a>条件付きアクセスと多要素認証

追加のセキュリティ層としての Azure AD を使用して、Windows Admin Center ゲートウェイへのアクセスを制御する利点の 1 つは、条件付きアクセスと多要素認証などの Azure AD の強力なセキュリティ機能を活用することができます。 

[Azure Active Directory で条件付きアクセスの構成に関する詳細について説明します。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>シングル サインオンを構成する

**シングル サインオンで Windows Server 上のサービスとしてデプロイした場合**

Windows 10 の Windows Admin Center をインストールするときに、シングル サインオンを使用する準備ができては。 Windows Server で Windows Admin Center を使用しようとしている場合は、シングル サインオンを使用する前に、何らかの形式の環境における Kerberos の委任を設定する必要があります。 委任は、ターゲット ノードに委任する信頼済みとしてゲートウェイ コンピューターを構成します。 

構成する[リソースに基づく制約付き委任](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)環境内には、次の PowerShell コマンドレットを実行します。 (Windows Server 2012 を実行するドメイン コント ローラーが必要であるに注意してくださいまたはそれ以降を使用します。)

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

サーバーで、この例では、Windows Admin Center ゲートウェイがインストールされている**WindowsAdminCenterGW**、対象のノード名と**ManagedNode**します。

このリレーションシップを削除するには、次のコマンドレットを実行します。

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>役割ベースのアクセス制御

ロール ベース access control では、それらの完全なローカル管理者ではなく、マシンへのアクセス制限をユーザーに提供することができます。
[ロールベースのアクセス制御と利用可能な役割の詳細。](../plan/user-access-options.md#role-based-access-control)

RBAC の設定の 2 つの手順で構成されています。 対象コンピューターでのサポートを有効にすると、ユーザーを関連するロールに割り当てます。

> [!TIP]
> コンピューターのローカル管理者権限があることを確認してロールベースのアクセス制御のサポートを構成しているを作成します。

### <a name="apply-role-based-access-control-to-a-single-machine"></a>単一のコンピューターにロールベースのアクセス制御を適用します。

1 台のマシンのデプロイ モデルでは、一部のコンピューターを管理するだけで単純な環境に最適です。
ロールベースのアクセス制御対応のマシンを構成すると、次の変更が発生します。
-   Windows Admin Center で必要な関数での PowerShell モジュールをシステム ドライブ上のインストールは`C:\Program Files\WindowsPowerShell\Modules`します。 開始されますすべてのモジュール**Microsoft.Sme。**
-   実行という名前のマシンで Just Enough Administration のエンドポイントを構成する 1 回限りの構成を Desired State Configuration **Microsoft.Sme.PowerShell**します。 このエンドポイントは、Windows Admin Center で使用される 3 つのロールを定義し、ユーザーがそれに接続するときに、一時的なローカル管理者として実行されます。
-   ユーザーは、どのロールにアクセスを割り当てられているコントロールに、3 つの新しいローカル グループが作成されます。
    -   Windows Admin Center 管理者
    -   Windows Admin Center HYPER-V 管理者
    -   Windows Admin Center リーダー

1 台のコンピューターでのロールベースのアクセス制御のサポートを有効にするには、次の手順に従います。

1.  Windows Admin Center を開き、ターゲット コンピューターのローカル管理者特権を持つアカウントを使用してロールベースのアクセス制御を構成するマシンに接続します。
2.  **概要**ツールで、をクリックして**設定** > **ロール ベース access control**します。
3.  クリックして**適用**ターゲット コンピューターでのロールベースのアクセス制御のサポートを有効にするページの下部にあります。 アプリケーション プロセスには、ターゲット コンピューターの PowerShell スクリプトをコピーし、(PowerShell Desired State Configuration を使用して) 構成を起動が含まれます。 を完了するまで 10 分かかる場合がありますと WinRM の再起動が発生します。 Windows Admin Center、PowerShell、および WMI のユーザーを一時的に切断します。
4.  ロールベースのアクセス制御の状態を確認 ページを更新します。 使用できる状態であるときに、状態が変わります**適用**します。

構成が適用されると、ロールにユーザーを割り当てることができます。

1.  開く、**ローカル ユーザーとグループ**ツールに移動して、**グループ**タブ。
2.  選択、 **Windows Admin Center リーダー**グループ。
3.  *詳細*ペインの下部で、クリックします**ユーザーの追加**Windows Admin Center を通じてサーバーへの読み取り専用アクセスを付与するユーザーまたはセキュリティ グループの名前を入力します。 ユーザーとグループは、ローカル コンピューターまたは Active Directory ドメインから取得できます。
4.  手順 2 ~ 3 を**Windows Admin Center HYPER-V Administrators**と**Windows Admin Center 管理者**グループ。

記入することもこれらのグループ一貫して、ドメイン全体で使用して、グループ ポリシー オブジェクトを構成することによって、[制限付きのグループ ポリシー設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)します。

### <a name="apply-role-based-access-control-to-multiple-machines"></a>複数のコンピューターにロールベースのアクセス制御を適用します。

大規模なエンタープライズ デプロイでは、Windows Admin Center ゲートウェイから構成パッケージをダウンロードすることによって、コンピューターに、ロールベースのアクセス制御機能をプッシュする、既存のオートメーション ツールを使用できます。
PowerShell Desired State Configuration で使用する構成パッケージは設計されていますが、推奨される automation ソリューションと連動するように調整できます。

#### <a name="download-the-role-based-access-control-configuration"></a>ロールベースのアクセス制御の構成をダウンロードします。

ロールベースのアクセス制御の構成パッケージをダウンロードするには、Windows Admin Center や PowerShell プロンプトにアクセスする必要があります。

Windows Server でサービス モードで、Windows Admin Center ゲートウェイを実行している、次のコマンドを使用して、構成パッケージをダウンロードします。
環境に適したでゲートウェイのアドレスを更新してください。

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 コンピューターで Windows Admin Center ゲートウェイを実行している場合は、次のコマンドを実行します。

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip アーカイブを展開すると、次のフォルダー構造が表示されます。
- InstallJeaFeatures.ps1
- JustEnoughAdministration (ディレクトリ)
- モジュール (ディレクトリ)
    - Microsoft.SME します。\* (ディレクトリ)
    - WindowsAdminCenter.Jea (ディレクトリ)

ノードでのロールベースのアクセス制御のサポートを構成するには、次の操作を実行する必要があります。
1.  JustEnoughAdministration、Microsoft.SME をコピーします。\*、およびターゲット コンピューターの PowerShell モジュールのディレクトリに WindowsAdminCenter.Jea モジュール。 通常、これはある`C:\Program Files\WindowsPowerShell\Modules`します。
2.  Update **InstallJeaFeature.ps1** RBAC エンドポイントの必要な構成と一致するファイル。
3.  DSC リソースをコンパイルする InstallJeaFeature.ps1 を実行します。
4.  すべてのマシン構成を適用する DSC 構成をデプロイします。

次のセクションでは、PowerShell リモート処理を使用してこれを行う方法について説明します。

#### <a name="deploy-on-multiple-machines"></a>複数のコンピューターでのデプロイします。

複数のコンピューターにダウンロードした構成を展開するには、更新する必要があります、 **InstallJeaFeatures.ps1**スクリプト環境内の適切なセキュリティ グループが含まれて、各コンピューター、ファイルをコピーするには構成スクリプトを呼び出します。
この記事では純粋な PowerShell ベースのアプローチに重点が、これを実現するのに優先のオートメーション ツールを使用できます。

既定では、構成スクリプトは各ロールへのアクセスを制御するコンピューターのローカル セキュリティ グループを作成します。
これはワークグループに適したであり、ドメイン参加しているコンピューターが直接する可能性がありますドメイン専用の環境でデプロイする場合は、各ロールに、ドメイン セキュリティ グループを関連付けます。
ドメイン セキュリティ グループを使用する構成を更新するには、開く**InstallJeaFeatures.ps1**次の変更を行います。

1.  削除、3**グループ**ファイルからリソース。
    1.  「グループ MS リーダー グループ」
    2.  「グループ MS-ハイパー-V の管理者のグループ」
    3.  「グループ MS Administrators グループ」
2.  3 つのグループのリソースを削除、JeaEndpoint から**DependsOn**プロパティ
    1.  "[Group] MS-閲覧者グループ"
    2.  「[グループ] MS-ハイパー-V の管理者のグループ」
    3.  "[Group] MS Administrators"
3.  JeaEndpoint 内のグループ名を変更する**RoleDefinitions**プロパティを必要なセキュリティ グループ。 たとえば、セキュリティ グループがある*CONTOSO\MyTrustedAdmins*変更であり、Windows Admin Center の管理者ロールにアクセス権を割り当てるをする必要があります`'$env:COMPUTERNAME\Windows Admin Center Administrators'`に`'CONTOSO\MyTrustedAdmins'`します。 更新する必要がある 3 つの文字列は次のとおりです。
    1.  ' $env:path: COMPUTERNAME\Windows 管理センターの管理者の
    2.  ' $env:path: COMPUTERNAME\Windows 管理センター、HYPER-V 管理者
    3.  ' $env:path: COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> ロールごとに一意なセキュリティ グループを使用してください。 構成は、同じセキュリティ グループが複数のロールに割り当てられている場合は失敗します。

最後に、[次へ]、 **InstallJeaFeatures.ps1**ファイルに、スクリプトの一番下に次の PowerShell の行を追加します。

```powershell
Copy-Item "$PSScriptRoot\JustEnoughAdministration" "$env:ProgramFiles\WindowsPowerShell\Modules" -Recurse -Force
$ConfigData = @{
    AllNodes = @()
    ModuleBasePath = @{
        Source = "$PSScriptRoot\Modules"
        Destination = "$env:ProgramFiles\WindowsPowerShell\Modules"
    }
}
InstallJeaFeature -ConfigurationData $ConfigData | Out-Null
Start-DscConfiguration -Path "$PSScriptRoot\InstallJeaFeature" -JobName "Installing JEA for Windows Admin Center" -Force
```

最後に、モジュール、DSC リソースと各ターゲット ノードに構成を含むフォルダーをコピーし、実行、 **InstallJeaFeature.ps1**スクリプト。
これを行うリモートで管理ワークステーションから、次のコマンドを実行できます。

```powershell
$ComputersToConfigure = 'MyServer01', 'MyServer02'

$ComputersToConfigure | ForEach-Object {
    $session = New-PSSession -ComputerName $_ -ErrorAction Stop
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC\JustEnoughAdministration\" -Destination "$env:ProgramFiles\WindowsPowerShell\Modules\" -ToSession $session -Recurse -Force
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC" -Destination "$env:TEMP\WindowsAdminCenter_RBAC" -ToSession $session -Recurse -Force
    Invoke-Command -Session $session -ScriptBlock { Import-Module JustEnoughAdministration; & "$env:TEMP\WindowsAdminCenter_RBAC\InstallJeaFeature.ps1" } -AsJob
    Disconnect-PSSession $session
}
```
