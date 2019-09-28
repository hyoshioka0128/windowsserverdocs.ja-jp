---
title: ユーザーアクセス制御とアクセス許可の構成
description: Active Directory または Azure AD (Project ホノルル) を使用してユーザーアクセス制御とアクセス許可を構成する方法について説明します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 20b311e9330880c2b26e2494aabe27bb04891868
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407035"
---
# <a name="configure-user-access-control-and-permissions"></a>ユーザー Access Control とアクセス許可の構成

> 適用対象:Windows Admin Center、Windows Admin Center Preview

まだお持ちでない場合は、 [Windows 管理センターのユーザーアクセス制御オプション](../plan/user-access-options.md)についてよく理解してください。

> [!NOTE]
> Windows 管理センターでのグループベースのアクセスは、ワークグループ環境または信頼されていないドメイン間ではサポートされていません。

## <a name="gateway-access-role-definitions"></a>ゲートウェイアクセスロールの定義

Windows 管理センターゲートウェイサービスへのアクセスには、次の2つの役割があります。

**ゲートウェイユーザー**は、Windows 管理センターゲートウェイサービスに接続して、そのゲートウェイを介してサーバーを管理できますが、アクセス許可や、ゲートウェイに対する認証に使用される認証メカニズムを変更することはできません。

**ゲートウェイ管理者**は、アクセスを許可するユーザーと、ゲートウェイに対するユーザーの認証方法を構成できます。 Windows 管理センターでは、ゲートウェイ管理者だけがアクセス設定を表示および構成できます。 ゲートウェイコンピューターのローカル管理者は、常に Windows 管理センターゲートウェイサービスの管理者です。

> [!NOTE]
> ゲートウェイへのアクセスは、ゲートウェイによって表示される管理対象サーバーへのアクセスを意味しません。 対象サーバーを管理するには、接続するユーザーが資格情報を使用する必要があります (渡された Windows 資格情報を使用するか、**管理**者権限を持つ Windows 管理センターセッションで提供される資格情報を使用します)。その対象サーバーへの接続。

## <a name="active-directory-or-local-machine-groups"></a>Active Directory またはローカルコンピューターグループ

既定では、Active Directory またはローカルコンピューターグループを使用して、ゲートウェイアクセスを制御します。 Active Directory ドメインがある場合は、Windows 管理センターのインターフェイス内からゲートウェイユーザーと管理者のアクセス権を管理できます。

**[ユーザー]** タブでは、ゲートウェイユーザーとして Windows 管理センターにアクセスできるユーザーを制御できます。 既定では、セキュリティグループを指定しない場合、ゲートウェイの URL にアクセスするすべてのユーザーにアクセス権が与えられます。 1つまたは複数のセキュリティグループをユーザー一覧に追加すると、それらのグループのメンバーにアクセスが制限されます。

環境内で Active Directory ドメインを使用しない場合、アクセスは Windows 管理センターゲートウェイコンピューター上の @no__t 0 および @no__t ローカルグループによって制御されます。

### <a name="smartcard-authentication"></a>スマートカード認証

スマートカードベースのセキュリティグループに_必要な_追加のグループを指定することによって、**スマートカード認証**を適用できます。 スマートカードベースのセキュリティグループを追加した後は、ユーザーが Windows 管理センターサービスにアクセスできるのは、ユーザー一覧に含まれる任意のセキュリティグループとスマートカードグループのメンバーである場合のみです。

**[管理者]** タブでは、ゲートウェイ管理者として Windows 管理センターにアクセスできるユーザーを制御できます。 コンピューターのローカルの administrators グループには、常に完全な管理者アクセス権が付与され、一覧から削除することはできません。 セキュリティグループを追加することによって、これらのグループのメンバーに Windows 管理センターのゲートウェイ設定を変更する権限を付与します。 管理者リストでは、ユーザー一覧と同じ方法でスマートカード認証をサポートしています。セキュリティグループとスマートカードグループの AND 条件を使用します。

## <a name="azure-active-directory"></a>Azure Active Directory

組織で Azure Active Directory (Azure AD) を使用している場合は、ゲートウェイへのアクセスに Azure AD 認証を要求することにより、Windows 管理センターに**セキュリティ層を追加する**ことができます。 Windows 管理センターにアクセスするには、ユーザーの**windows アカウント**もゲートウェイサーバーにアクセスできる必要があります (Azure AD 認証が使用されている場合でも)。 Azure AD を使用する場合、windows 管理センターの UI 内からではなく、Azure Portal から Windows 管理センターのユーザーと管理者のアクセス許可を管理します。

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 認証が有効になっている場合の Windows 管理センターへのアクセス

使用されているブラウザーによっては、Azure AD 認証が構成された Windows 管理センターにアクセスしている一部のユーザーが、**ブラウザーから**追加のプロンプトを受け取ります。このプロンプトで、windows アカウントの資格情報を入力する必要があります。Windows 管理センターがインストールされています。 この情報を入力すると、ユーザーは追加の Azure Active Directory 認証プロンプトを取得します。これには、Azure の Azure AD アプリケーションでアクセス権が付与されている Azure アカウントの資格情報が必要です。

> [!NOTE]
> Windows アカウントを持つユーザーは、ゲートウェイコンピューターに対する**管理者権限**を持っているため、Azure AD 認証を求められることはありません。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows 管理センタープレビューの Azure Active Directory 認証の構成

Windows 管理センターの**設定**  >  **アクセス** の順に移動し、トグルスイッチを使用して Azure Active Directory を使用してセキュリティ層をゲートウェイに追加する をオンにします。 Azure にゲートウェイを登録していない場合は、この時点で実行するように指示されます。

既定では、Azure AD テナントのすべてのメンバーには、Windows 管理センターゲートウェイサービスへのユーザーアクセス権があります。 Windows 管理センターゲートウェイへの管理者アクセス権を持つのは、ゲートウェイコンピューターのローカル管理者だけです。 ゲートウェイコンピューターのローカル管理者の権限は制限できないことに注意してください。認証に Azure AD が使用されているかどうかにかかわらず、ローカルの管理者は何でも実行できます。

特定の Azure AD ユーザーまたはグループに、ゲートウェイユーザーまたはゲートウェイ管理者が Windows 管理センターサービスにアクセスできるようにするには、次の操作を行う必要があります。

1.  [アクセス設定] に表示されているハイパーリンクを使用して、Azure portal で Windows 管理センター Azure AD アプリケーションにアクセスします。 注このハイパーリンクは、Azure Active Directory 認証が有効になっている場合にのみ使用できます。 
    -   また、Azure portal でアプリケーションを検索するには、[ **Azure Active Directory** > **エンタープライズ @no__t アプリケーション**] に移動し、 **[すべてのアプリケーション]** を見つけて、 **windowsadmincenter**を検索します (Azure AD アプリの名前はWindowsAdminCenter-<gateway name>)。 検索結果が得られない場合は、**表示**が **すべてのアプリケーション** に設定されていること、**アプリケーションの状態** が **任意** に設定されていることを確認し、適用 をクリックして、検索を アプリケーションが見つかったら、 **[ユーザーとグループ]** にアクセスします。
2.  プロパティ] タブで、 **[ユーザー割り当てが必要]** を [はい に設定します。
    この操作を完了すると、 **[ユーザーとグループ]** タブに表示されているメンバーのみが Windows 管理センターゲートウェイにアクセスできるようになります。
3.  ユーザーとグループ タブで、**ユーザーの追加** を選択します。 追加するユーザーまたはグループごとに、ゲートウェイユーザーまたはゲートウェイ管理者ロールを割り当てる必要があります。

Azure AD 認証を有効にすると、ゲートウェイサービスが再起動し、ブラウザーを最新の状態に更新する必要があります。 Azure portal では、SME Azure AD アプリケーションのユーザーアクセスをいつでも更新できます。

ユーザーが Windows 管理センターのゲートウェイの URL にアクセスしようとすると、Azure Active Directory id を使用してサインインするように求められます。 Windows 管理センターにアクセスするには、ユーザーもゲートウェイサーバーのローカルユーザーのメンバーである必要があることに注意してください。

ユーザーおよび管理者は、現在ログインしているアカウントを表示したり、Windows 管理センターの設定の **[アカウント]** タブからこの Azure AD アカウントからサインアウトしたりできます。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows 管理センターの Azure Active Directory 認証の構成

[Azure AD 認証を設定するには、最初に Azure にゲートウェイを登録する必要があり](azure-integration.md)ます (これは、Windows 管理センターゲートウェイに対して1回だけ行う必要があります)。 この手順では、ゲートウェイユーザーとゲートウェイの管理者アクセスを管理できる Azure AD アプリケーションを作成します。

特定の Azure AD ユーザーまたはグループに、ゲートウェイユーザーまたはゲートウェイ管理者が Windows 管理センターサービスにアクセスできるようにするには、次の操作を行う必要があります。

1.  Azure portal で、SME Azure AD アプリケーションにアクセスします。 
    -   **[アクセス制御の変更]** をクリックし、Windows 管理センターのアクセス設定 で  **[Azure Active Directory]** を選択した場合は、UI に表示されるハイパーリンクを使用して、Azure portal 内の Azure AD アプリケーションにアクセスできます。 このハイパーリンクは、[保存] をクリックし、アクセス制御 id プロバイダーとして Azure AD を選択した後に、アクセス設定でも使用できます。
    -   また、Azure portal でアプリケーションを検索することもできます。そのためには、[ **Azure Active Directory** > **エンタープライズアプリケーション**] @no__t **[すべてのアプリケーション]** の順に移動し、 **[sme]** を検索します (Azure AD アプリの名前は "sme-<gateway>" になります)。 検索結果が得られない場合は、**表示**が **すべてのアプリケーション** に設定されていること、**アプリケーションの状態** が **任意** に設定されていることを確認し、適用 をクリックして、検索を アプリケーションが見つかったら、 **[ユーザーとグループ]** にアクセスします。
2.  プロパティ] タブで、 **[ユーザー割り当てが必要]** を [はい に設定します。
    この操作を完了すると、 **[ユーザーとグループ]** タブに表示されているメンバーのみが Windows 管理センターゲートウェイにアクセスできるようになります。
3.  ユーザーとグループ タブで、**ユーザーの追加** を選択します。 追加するユーザーまたはグループごとに、ゲートウェイユーザーまたはゲートウェイ管理者ロールを割り当てる必要があります。

**[アクセス制御の変更]** ウィンドウで Azure AD アクセス制御を保存すると、ゲートウェイサービスが再起動し、ブラウザーを最新の状態に更新する必要があります。 Azure portal では、Windows 管理センター Azure AD アプリケーションのユーザーアクセスをいつでも更新できます。 

ユーザーが Windows 管理センターのゲートウェイの URL にアクセスしようとすると、Azure Active Directory id を使用してサインインするように求められます。 Windows 管理センターにアクセスするには、ユーザーもゲートウェイサーバーのローカルユーザーのメンバーである必要があることに注意してください。 

Windows 管理センターの全般設定の **[Azure]** タブを使用すると、ユーザーと管理者は、現在ログインしているアカウントを表示したり、この Azure AD アカウントからサインアウトしたりすることができます。

### <a name="conditional-access-and-multi-factor-authentication"></a>条件付きアクセスと多要素認証

Windows 管理センターゲートウェイへのアクセスを制御するために Azure AD を追加のセキュリティ層として使用する利点の1つは、条件付きアクセスや multi-factor authentication などの強力なセキュリティ機能を Azure AD 利用できることです。 

[Azure Active Directory を使用した条件付きアクセスの構成の詳細については、こちらをご覧ください。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>シングル サインオンを構成する

**Windows Server にサービスとして展開された場合のシングルサインオン**

Windows 10 に Windows 管理センターをインストールすると、シングルサインオンを使用できるようになります。 ただし、windows Server で Windows 管理センターを使用する場合は、シングルサインオンを使用する前に、環境内に何らかの形式の Kerberos 委任を設定する必要があります。 委任によって、ターゲットノードに委任するようにゲートウェイコンピューターが信頼済みとして構成されます。 

環境内で[リソースベースの制約付き委任](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)を構成するには、次の PowerShell コマンドレットを実行します。 (これには、Windows Server 2012 以降を実行しているドメインコントローラーが必要であることに注意してください)。

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

この例では、Windows 管理センターゲートウェイがサーバー **Windowsadmincenter gw**にインストールされ、ターゲットノード名が**managednode**になっています。

このリレーションシップを削除するには、次のコマンドレットを実行します。

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>役割ベースのアクセス制御

ロールベースのアクセス制御を使用すると、ローカルの完全な管理者ではなく、コンピューターへの制限付きアクセスをユーザーに提供できます。
[ロールベースのアクセス制御と使用可能なロールについては、こちらを参照してください。](../plan/user-access-options.md#role-based-access-control)

RBAC の設定は、ターゲットコンピュータでのサポートの有効化と、関連するロールへのユーザーの割り当てという2つの手順で構成されています。

> [!TIP]
> ロールベースのアクセス制御のサポートを構成するコンピューターに、ローカル管理者特権があることを確認します。

### <a name="apply-role-based-access-control-to-a-single-machine"></a>ロールベースのアクセス制御を1台のコンピューターに適用する

シングルマシンデプロイモデルは、管理するコンピューターが少数の単純な環境に最適です。
ロールベースのアクセス制御をサポートするコンピューターを構成すると、次のような変更が行われます。

-   Windows 管理センターで必要な機能を備えた PowerShell モジュールは、システムドライブの `C:\Program Files\WindowsPowerShell\Modules` の下にインストールされます。 すべてのモジュールが Microsoft の Sme から開始され**ます。**
-   Desired State Configuration では、1回限りの構成を実行して、コンピューター上の管理エンドポイントを構成します。これは、" **Microsoft.** ..." という名前です。 このエンドポイントは、Windows 管理センターによって使用される3つのロールを定義し、ユーザーが接続すると、一時的なローカル管理者として実行されます。
-   3新しいローカルグループが作成され、どのユーザーにどのロールへのアクセスが割り当てられているかを制御します。
    -   Windows 管理センター管理者
    -   Windows 管理センター Hyper-v 管理者
    -   Windows 管理センターリーダー

1台のコンピューターでロールベースのアクセス制御のサポートを有効にするには、次の手順を実行します。

1.  Windows 管理センターを開き、ターゲットコンピューターでローカル管理者特権を持つアカウントを使用して、ロールベースのアクセス制御で構成するコンピューターに接続します。
2.  **概要**ツールで、**設定** をクリックし  > **ロールベースのアクセス制御** をクリックします。
3.  ページの下部にある **[適用]** をクリックして、ターゲットコンピューターでのロールベースのアクセス制御のサポートを有効にします。 アプリケーションプロセスでは、PowerShell スクリプトをコピーし、ターゲットコンピューターで (PowerShell Desired State Configuration を使用して) 構成を呼び出します。 完了までに最大で10分かかる場合があり、WinRM は再起動されます。 これにより、Windows 管理センター、PowerShell、および WMI ユーザーが一時的に切断されます。
4.  ページを更新して、ロールベースのアクセス制御の状態を確認します。 使用準備が整うと、状態が [**適用**済み] に変わります。

構成が適用されると、ユーザーをロールに割り当てることができます。

1.  **[ローカルユーザーとグループ]** ツールを開き、 **[グループ]** タブに移動します。
2.  **Windows 管理センターの閲覧者**グループを選択します。
3.  下部の*詳細*ウィンドウで、[ユーザーの**追加**] をクリックし、Windows 管理センターを使用してサーバーへの読み取り専用アクセス権を持つユーザーまたはセキュリティグループの名前を入力します。 ユーザーとグループは、ローカルコンピューターまたは Active Directory ドメインから取得できます。
4.  **Windows 管理センターの Hyper-v 管理**者グループと Windows 管理センターの**管理者**グループに対して、手順2-3 を繰り返します。

また、制限された[グループポリシー設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)を使用してグループポリシーオブジェクトを構成することによって、これらのグループをドメイン全体で一貫したものにすることもできます。

### <a name="apply-role-based-access-control-to-multiple-machines"></a>複数のコンピューターへのロールベースのアクセス制御の適用

大規模なエンタープライズ展開では、Windows 管理センターゲートウェイから構成パッケージをダウンロードすることによって、既存の自動化ツールを使用して、ロールベースのアクセス制御機能をコンピューターにプッシュできます。
構成パッケージは、PowerShell Desired State Configuration と共に使用するように設計されていますが、優先する automation ソリューションで動作するように調整することができます。

#### <a name="download-the-role-based-access-control-configuration"></a>ロールベースのアクセス制御構成をダウンロードする

ロールベースのアクセス制御構成パッケージをダウンロードするには、Windows 管理センターと PowerShell プロンプトにアクセスできる必要があります。

Windows Server で Windows 管理センターゲートウェイをサービスモードで実行している場合は、次のコマンドを使用して構成パッケージをダウンロードします。
ゲートウェイアドレスは、実際の環境に合わせて適切なものに更新してください。

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 コンピューターで Windows 管理センターゲートウェイを実行している場合は、代わりに次のコマンドを実行します。

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip アーカイブを展開すると、次のフォルダー構造が表示されます。

- InstallJeaFeatures
- ジャストの管理 (ディレクトリ)
- モジュール (ディレクトリ)
    - @No__t-0 (ディレクトリ)
    - WindowsAdminCenter Jea (ディレクトリ)

ノードでロールベースのアクセス制御のサポートを構成するには、次の操作を実行する必要があります。

1.  対象のコンピューター上の PowerShell モジュールディレクトリに、ジャストイン \*、および WindowsAdminCenter の各モジュールをコピーします。 通常、これは @no__t 0 にあります。
2.  RBAC エンドポイントに必要な構成に合わせて**InstallJeaFeature**ファイルを更新します。
3.  InstallJeaFeature を実行して、DSC リソースをコンパイルします。
4.  すべてのコンピューターに DSC 構成をデプロイして、構成を適用します。

次のセクションでは、PowerShell リモート処理を使用してこれを行う方法について説明します。

#### <a name="deploy-on-multiple-machines"></a>複数のコンピューターへのデプロイ

ダウンロードした構成を複数のコンピューターに展開するには、 **InstallJeaFeatures**スクリプトを更新して、環境に適したセキュリティグループを追加し、各コンピューターにファイルをコピーして、構成スクリプト。
この記事では、適切なオートメーションツールを使用してこれを実現できます。ただし、この記事では、純粋な PowerShell ベースのアプローチに焦点を当てます。

既定では、構成スクリプトは、各ロールへのアクセスを制御するために、コンピューター上にローカルセキュリティグループを作成します。
これはワークグループとドメインに参加しているコンピューターに適していますが、ドメインのみの環境でを展開する場合は、ドメインセキュリティグループを各ロールに直接関連付けることをお勧めします。
ドメインセキュリティグループを使用するように構成を更新するには、 **InstallJeaFeatures**を開き、次のように変更します。

1.  ファイルから3つの**グループ**リソースを削除します。
    1.  "Group MS-Reader-Group"
    2.  "Group MS-Hyper-v-Administrators-Group"
    3.  "グループ MS-Administrators-グループ"
2.  JeaEndpoint **DependsOn**プロパティから3つのグループリソースを削除します。
    1.  "[Group] MS Reader-Group"
    2.  "[グループ] MS-Hyper-v-Administrators-Group"
    3.  "[グループ] MS-Administrators-グループ"
3.  JeaEndpoint **Roledefinitions**プロパティのグループ名を、目的のセキュリティグループに変更します。 たとえば、Windows 管理センターの管理者ロールへのアクセスを割り当てる必要があるセキュリティグループ*CONTOSO\MyTrustedAdmins*がある場合は、`'$env:COMPUTERNAME\Windows Admin Center Administrators'` を `'CONTOSO\MyTrustedAdmins'` に変更します。 更新する必要がある3つの文字列は次のとおりです。
    1.  ' $env: computer' 管理センター管理者 '
    2.  ' $env: computer' Admin Center Hyper-v Administrators '
    3.  ' $env: computer' 管理センターリーダー '

> [!NOTE]
> ロールごとに一意のセキュリティグループを使用してください。 同じセキュリティグループが複数のロールに割り当てられている場合、構成は失敗します。

次に、 **InstallJeaFeatures**ファイルの末尾に、PowerShell の次の行をスクリプトの最後に追加します。

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

最後に、モジュール、DSC リソース、および構成を含むフォルダーを各ターゲットノードにコピーし、 **InstallJeaFeature**スクリプトを実行できます。
管理ワークステーションからリモートでこれを行うには、次のコマンドを実行します。

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
