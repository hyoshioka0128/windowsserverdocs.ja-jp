---
title: ユーザー アクセス制御とアクセス許可の構成
description: Active Directory または Azure AD (Project Honolulu) を使用してユーザー アクセス制御とアクセス許可を構成する方法について説明します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0de38560301d4d793214846036850a05a5d5a326
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182208"
---
# <a name="configure-user-access-control-and-permissions"></a>ユーザー アクセス制御とアクセス許可を構成する

> 適用先:Windows Admin Center、Windows Admin Center Preview

Windows Admin Center のユーザー アクセス制御オプションについてよく理解していない場合は、[こちら](../plan/user-access-options.md)で確認してください。

> [!NOTE]
> Windows Admin Center でのグループ ベースのアクセスは、ワークグループ環境または信頼されていないドメイン間ではサポートされていません。

## <a name="gateway-access-role-definitions"></a>ゲートウェイ アクセス ロールの定義

Windows Admin Center ゲートウェイ サービスへのアクセスには、次の 2 つのロールがあります。

**ゲートウェイ ユーザー**は、Windows Admin Center ゲートウェイ サービスに接続し、そのゲートウェイを介してサーバーを管理できますが、アクセス許可や、ゲートウェイに対する認証に使用される認証メカニズムを変更することはできません。

**ゲートウェイ管理者**は、ゲートウェイにアクセスできるユーザーとユーザーの認証方法を構成できます。 Windows Admin Center では、ゲートウェイ管理者のみがアクセス設定を表示および構成できます。 ゲートウェイ マシンのローカル管理者は、常に Windows Admin Center ゲートウェイ サービスの管理者です。

> [!NOTE]
> ゲートウェイにアクセスできることは、ゲートウェイから表示できるマネージド サーバーにアクセスできることを意味しません。 ターゲット サーバーを管理するには、接続するユーザーが、そのターゲット サーバーへの管理者アクセス権を持つ資格情報 (パススルー Windows 資格情報、または **[管理に使用する資格情報]** アクションを使用して Windows Admin Center セッションで指定した資格情報) を使用する必要があります。

## <a name="active-directory-or-local-machine-groups"></a>Active Directory またはローカル コンピューター グループ

既定では、Active Directory またはローカル コンピューター グループを使用して、ゲートウェイ アクセスを制御します。 Active Directory ドメインがある場合は、Windows Admin Center のインターフェイス内からゲートウェイ ユーザーと管理者アクセス権を管理できます。

**[ユーザー]** タブでは、ゲートウェイ ユーザーとして Windows Admin Center にアクセスできるユーザーを制御できます。 既定では、セキュリティ グループを指定しない場合、ゲートウェイの URL にアクセスするすべてのユーザーにアクセス権が与えられます。 1 つ以上のセキュリティ グループをユーザー一覧に追加すると、それらのグループのメンバーのみにアクセスが制限されます。

環境内で Active Directory ドメインを使用しない場合、アクセスは Windows Admin Center ゲートウェイ マシン上の `Users` および `Administrators` ローカル グループによって制御されます。

### <a name="smartcard-authentication"></a>スマートカード認証

**スマートカード認証**を適用するには、スマートカードベースのセキュリティ グループに追加の "_必要な_" グループを指定します。 スマートカードベースのセキュリティ グループを追加すると、ユーザーは、ユーザー一覧に含まれるセキュリティ グループとスマートカード グループの両方のメンバーである場合にのみ、Windows Admin Center サービスにアクセスできます。

**[管理者]** タブでは、ゲートウェイ管理者として Windows Admin Center にアクセスできるユーザーを制御できます。 コンピューターのローカルの管理者グループには、常に完全な管理者アクセス権が付与され、一覧から削除することはできません。 セキュリティ グループを追加すると、それらのグループのメンバーには Windows Admin Center ゲートウェイ設定を変更する特権が付与されます。 管理者一覧では、セキュリティ グループとスマートカード グループの AND 条件を使用して、ユーザー一覧と同じ方法でスマートカード認証がサポートされます。

## <a name="azure-active-directory"></a>Azure Active Directory

組織で Azure Active Directory (Azure AD) を使用している場合、ゲートウェイへのアクセスに Azure AD 認証を必須にすることで、Windows Admin Center に**もう 1 層の**セキュリティを追加することもできます。 Windows Admin Center にアクセスするには、(Azure AD 認証が使用されている場合でも) ユーザーの **Windows アカウント**にもゲートウェイ サーバーへのアクセス権が必要です。 Azure AD を使用する場合、Windows Admin Center UI 内からではなく、Azure portal から Windows Admin Center のユーザーおよび管理者のアクセス許可を管理します。

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Azure AD 認証が有効な場合の Windows Admin Center へのアクセス

使用しているブラウザーによっては、Azure AD 認証が構成された Windows Admin Center にアクセスする一部のユーザーには、**ブラウザーから**追加のプロンプトが表示されます。ここで Windows Admin Center がインストールされているマシンの Windows アカウントの資格情報を指定する必要があります。 その情報を入力すると、ユーザーには追加の Azure Active Directory 認証プロンプトが表示されます。ここでは、Azure の Azure AD アプリケーションでアクセスが許可された Azure アカウントの資格情報が必要です。

> [!NOTE]
> Windows アカウントにゲートウェイ マシン上で**管理者アクセス権**があるユーザーには、Azure AD 認証のプロンプトは表示されません。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Windows Admin Center プレビューの Azure Active Directory 認証の構成

Windows Admin Center の **[設定]**  >  **[アクセス]** に移動し、トグル スイッチを使用して [Use Azure Active Directory to add a layer of security to the gateway]\(Azure Active Directory を使用してセキュリティの層をゲートウェイに追加する\) をオンにします。 Azure にゲートウェイを登録していない場合は、この時点で行うように指示されます。

既定では、Azure AD テナントのすべてのメンバーには、Windows Admin Center ゲートウェイ サービスへのユーザー アクセス権があります。 Windows Admin Center ゲートウェイへの管理者アクセス権を持つのは、ゲートウェイ マシンのローカル管理者のみです。 ゲートウェイ マシンのローカル管理者の権限は制限できないことに注意してください。認証に Azure AD が使用されているかどうかにかかわらず、ローカルの管理者は何でも実行できます。

特定の Azure AD ユーザーまたはグループ ゲートウェイ ユーザーまたはゲートウェイ管理者に Windows Admin Center サービスへのアクセスを許可する場合は、次の操作を行う必要があります。

1.  Azure portal で [アクセス設定] に表示されるハイパーリンクを使用して、Windows Admin Center Azure AD アプリケーションにアクセスします。 このハイパーリンクは、Azure Active Directory 認証が有効な場合にのみ使用できることに注意してください。
    -   また、Azure portal で **[Azure Active Directory]**  >  **[エンタープライズ アプリケーション]**  >  **[すべてのアプリケーション]** にアクセスして **WindowsAdminCenter** を検索してアプリケーションを見つけることもできます (Azure AD アプリの名前は WindowsAdminCenter-<gateway name> になります)。 検索結果が表示されない場合は、 **[表示]** が **[すべてのアプリケーション]** に設定されていること、 **[アプリケーションの状態]** が **[すべて]** に設定されていることを確認し、[適用] をクリックしてから、検索を試してください。 アプリケーションが見つかったら、 **[ユーザーとグループ]** にアクセスします。
2.  [プロパティ] タブで、 **[ユーザーの割り当てが必要]** を [はい] に設定します。
    この操作を完了すると、 **[ユーザーとグループ]** タブに表示されているメンバーのみが Windows Admin Center ゲートウェイにアクセスできるようになります。
3.  [ユーザーとグループ] タブで、 **[ユーザーの追加]** を選択します。 追加したユーザーまたはグループごとに、ゲートウェイ ユーザーまたはゲートウェイ管理者のロールを割り当てる必要があります。

Azure AD 認証を有効にした後は、ゲートウェイ サービスが再起動します。また、ブラウザーを更新する必要があります。 Azure portal では、SME Azure AD アプリケーションのユーザー アクセスをいつでも更新できます。

ユーザーが Windows Admin Center ゲートウェイ URL にアクセスしようとすると、Azure Active Directory ID を使用してサインインするように求められます。 ユーザーが Windows Admin Center にアクセスするには、ゲートウェイ サーバーのローカル ユーザーのメンバーでもある必要があることに注意してください。

ユーザーと管理者は、Windows Admin Center の [設定] の **[アカウント]** タブから、現在ログインしているアカウントを表示できるだけでなく、Azure AD アカウントからサインアウトすることもできます。

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Windows Admin Center の Azure Active Directory 認証の構成

[Azure AD 認証を設定するには、まず Azure にゲートウェイを登録する必要があります](azure-integration.md) (この操作は、Windows Admin Center ゲートウェイに対して 1 回だけ行う必要があります)。 この手順では、ゲートウェイ ユーザーとゲートウェイ管理者のアクセスを管理できる Azure AD アプリケーションを作成します。

特定の Azure AD ユーザーまたはグループ ゲートウェイ ユーザーまたはゲートウェイ管理者に Windows Admin Center サービスへのアクセスを許可する場合は、次の操作を行う必要があります。

1.  Azure portal で SME Azure AD アプリケーションにアクセスします。
    -   **[Change access control]\(アクセス制御の変更\)** をクリックし、Windows Admin Center の [アクセスの設定] から **[Azure Active Directory]** を選択すると、UI に表示されるハイパーリンクを使用して Azure portal の Azure AD アプリケーションにアクセスできます。 このハイパーリンクは、[アクセスの設定] で [保存] をクリックし、アクセス制御 ID プロバイダーとして Azure AD を選択した後も使用できます。
    -   また、Azure portal で **[Azure Active Directory]**  >  **[エンタープライズ アプリケーション]**  >  **[すべてのアプリケーション]** にアクセスし、**SME** を検索してアプリケーションを見つけることもできます (Azure AD アプリの名前は SME-<gateway> になります)。 検索結果が表示されない場合は、 **[表示]** が **[すべてのアプリケーション]** に設定されていること、 **[アプリケーションの状態]** が **[すべて]** に設定されていることを確認し、[適用] をクリックしてから、検索を試してください。 アプリケーションが見つかったら、 **[ユーザーとグループ]** にアクセスします。
2.  [プロパティ] タブで、 **[ユーザーの割り当てが必要]** を [はい] に設定します。
    この操作を完了すると、 **[ユーザーとグループ]** タブに表示されているメンバーのみが Windows Admin Center ゲートウェイにアクセスできるようになります。
3.  [ユーザーとグループ] タブで、 **[ユーザーの追加]** を選択します。 追加したユーザーまたはグループごとに、ゲートウェイ ユーザーまたはゲートウェイ管理者のロールを割り当てる必要があります。

**[Change access control]\(アクセス制御の変更\)** ペインで Azure AD のアクセス制御を保存した後は、ゲートウェイ サービスが再起動します。また、ブラウザーを更新する必要があります。 Azure portal では、Windows Admin Center Azure AD アプリケーションのユーザー アクセスをいつでも更新できます。

ユーザーが Windows Admin Center ゲートウェイ URL にアクセスしようとすると、Azure Active Directory ID を使用してサインインするように求められます。 ユーザーが Windows Admin Center にアクセスするには、ゲートウェイ サーバーのローカル ユーザーのメンバーでもある必要があることに注意してください。

ユーザーと管理者は、Windows Admin Center の全般設定の **[Azure]** タブを使用して、現在ログインしているアカウントを表示できるだけでなく、Azure AD アカウントからサインアウトすることもできます。

### <a name="conditional-access-and-multi-factor-authentication"></a>条件付きアクセスと多要素認証

Windows Admin Center ゲートウェイへのアクセスを制御するために Azure AD を追加のセキュリティ層として使用する利点の 1 つは、条件付きアクセスや多要素認証などの Azure AD の強力なセキュリティ機能を利用できることです。

[Azure Active Directory を使用した条件付きアクセスの構成の詳細については、こちらを参照してください。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>シングル サインオンを構成する

**Windows Server にサービスとしてデプロイされた場合のシングル サインオン**

Windows 10 に Windows Admin Center をインストールすると、シングル サインオンを使用できるようになります。 ただし、Windows Server 上で Windows Admin Center を使用する場合は、シングル サインオンを使用する前に、環境内に何らかの形式の Kerberos 委任を設定する必要があります。 委任によってゲートウェイ マシンが信頼済みとして構成され、ターゲット ノードに委任されます。

環境内で[リソースベースの制約付き委任](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)を構成するには、次の PowerShell の例を使用します。 この例は、contoso.com ドメインの Windows Admin Center ゲートウェイ [wac.contoso.com] からの委任を受け入れるように Windows サーバー [node01.contoso.com] を構成する方法を示しています。

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount (Get-ADComputer wac)
```

このリレーションシップを削除するには、次のコマンドレットを実行します。

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>ロール基準のアクセス制御

ロールベースのアクセス制御を使用すると、ローカルの完全な管理者にするのではなく、マシンへの制限付きアクセス権をユーザーに付与できるようになります。
[ロールベースのアクセス制御と使用できるロールについては、こちらを参照してください。](../plan/user-access-options.md#role-based-access-control)

RBAC の設定は、ターゲット コンピューターでサポートを有効にし、ユーザーを関連するロールに割り当てるという 2 つの手順で構成されます。

> [!TIP]
> ロールベースのアクセス制御のサポートを構成するマシンに、ローカル管理者特権があることを確認します。

### <a name="apply-role-based-access-control-to-a-single-machine"></a>ロールベースのアクセス制御を 1 台のマシンに適用する

1 台のマシンのデプロイ モデルは、管理するマシンが少数の単純な環境に最適です。
ロールベースのアクセス制御をサポートするマシンを構成すると、次のような変更が行われます。

-   Windows Admin Center で必要な機能を備えた PowerShell モジュールは、システム ドライブの `C:\Program Files\WindowsPowerShell\Modules` にインストールされます。 すべてのモジュールは **Microsoft.Sme** から始まります。
-   Desired State Configuration によって 1 回限りの構成が実行され、**Microsoft.Sme.PowerShell** という Just Enough Administration エンドポイントがマシン上に構成されます。 このエンドポイントによって、Windows Admin Center に使用される 3 つのロールが定義され、ユーザーが接続するときに一時的なローカル管理者として実行されます。
-   どのユーザーにどのロールへのアクセスを割り当てるかを制御する 3 つの新しいローカル グループが作成されます。
    -   Windows Admin Center 管理者
    -   Windows Admin Center Hyper-V 管理者
    -   Windows Admin Center 閲覧者

1 台のマシンでロールベースのアクセス制御のサポートを有効にするには、次の手順を実行します。

1.  Windows Admin Center を開き、ターゲット マシンでローカル管理者特権を持つアカウントを使用して、ロールベースのアクセス制御で構成するマシンに接続します。
2.  **[概要]** ツールで、 **[設定]**  >  **[ロールベースのアクセス制御]** をクリックします。
3.  ページの下部にある **[適用]** をクリックし、ターゲット コンピューターでロールベースのアクセス制御をサポートできるようにします。 アプリケーション プロセスでは、PowerShell スクリプトがコピーされ、ターゲット マシンで (PowerShell Desired State Configuration を使用して) 構成が呼び出されます。 完了までに最大で 10 分かかる場合があります。また、WinRM が再起動します。 これにより、Windows Admin Center、PowerShell、および WMI ユーザーが一時的に切断されます。
4.  ページを更新して、ロールベースのアクセス制御の状態を確認します。 使用する準備が整うと、状態は **[適用済み]** に変わります。

構成が適用されると、ユーザーをロールに割り当てることができます。

1.  **[ローカル ユーザーとグループ]** ツールを開き、 **[グループ]** タブに移動します。
2.  **Windows Admin Center 閲覧者**グループを選択します。
3.  下部にある *[詳細]* ペインで、 **[ユーザーの追加]** をクリックし、Windows Admin Center を使用してサーバーへの読み取り専用アクセス権を持つユーザーまたはセキュリティ グループの名前を入力します。 ローカル コンピューターまたは Active Directory ドメインのユーザーとグループを使用できます。
4.  **Windows Admin Center Hyper-V 管理者**と **Windows Admin Center 管理者**グループについて、手順 2 から 3 を繰り返します。

[[Restricted Groups Policy Setting]\(制限されたグループ ポリシー設定\)](/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29) でグループ ポリシー オブジェクトを構成することで、ドメイン全体でこれらのグループを一貫した方法で入力することもできます。

### <a name="apply-role-based-access-control-to-multiple-machines"></a>複数のマシンにロールベースのアクセス制御を適用する

大規模なエンタープライズ展開では、既存の自動化ツールを使用して Windows Admin Center ゲートウェイから構成パッケージをダウンロードすることにより、ロールベースのアクセス制御機能をコンピューターにプッシュできます。
構成パッケージは、PowerShell Desired State Configuration と共に使用するように設計されていますが、好みの自動化ソリューションで動作するように調整することができます。

#### <a name="download-the-role-based-access-control-configuration"></a>ロールベースのアクセス制御構成をダウンロードする

ロールベースのアクセス制御構成パッケージをダウンロードするには、Windows Admin Center と PowerShell プロンプトにアクセスできる必要があります。

Windows Server 上で Windows Admin Center ゲートウェイをサービス モードで実行している場合は、次のコマンドを使用して構成パッケージをダウンロードします。
ゲートウェイのアドレスは、実際の環境に合わせて適切なものに更新してください。

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Windows 10 マシン上で Windows Admin Center ゲートウェイを実行している場合は、代わりに次のコマンドを実行します。

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

zip アーカイブを展開すると、次のフォルダー構造が表示されます。

- InstallJeaFeatures.ps1
- JustEnoughAdministration (ディレクトリ)
- Modules (ディレクトリ)
    - Microsoft.SME.\* (ディレクトリ)
    - WindowsAdminCenter.Jea (ディレクトリ)

ノード上でロールベースのアクセス制御のサポートを構成するには、次のアクションを実行する必要があります。

1.  JustEnoughAdministration、Microsoft.SME.\*、および WindowsAdminCenter.Jea モジュールをターゲット マシン上の PowerShell モジュール ディレクトリにコピーします。 通常、これは `C:\Program Files\WindowsPowerShell\Modules` にあります。
2.  RBAC エンドポイントの目的の構成に合わせて **InstallJeaFeature.ps1** ファイルを更新します。
3.  InstallJeaFeature.ps1 を実行して、DSC リソースをコンパイルします。
4.  すべてのマシンに DSC 構成を展開し、構成を適用します。

次のセクションでは、PowerShell リモート処理を使用してこれを行う方法について説明します。

#### <a name="deploy-on-multiple-machines"></a>複数のマシンに展開する

ダウンロードした構成を複数のマシンに展開するには、**InstallJeaFeatures.ps1** スクリプトを更新して、環境に適したセキュリティ グループを含め、ファイルを各コンピューターにコピーして、構成スクリプトを呼び出す必要があります。
好みの自動化ツールを使用してもこれを実現できますが、この記事では純粋な PowerShell ベースのアプローチに焦点を当てます。

この構成スクリプトを実行すると、既定では、マシン上にローカル セキュリティ グループが作成され、各ロールへのアクセスが制御されます。
これはワークグループとドメインに参加しているマシンに適していますが、ドメインのみの環境に展開する場合は、ドメイン セキュリティ グループを各ロールに直接関連付けることができます。
ドメイン セキュリティ グループを使用するように構成を更新するには、**InstallJeaFeatures.ps1** を開き、次のように変更します。

1.  ファイルから 3 つの **Group** リソースを削除します。
    1.  "Group MS-Readers-Group"
    2.  "Group MS-Hyper-V-Administrators-Group"
    3.  "Group MS-Administrators-Group"
2.  JeaEndpoint の **DependsOn** プロパティから 3 つの Group リソースを削除します
    1.  "[Group]MS-Readers-Group"
    2.  "[Group]MS-Hyper-V-Administrators-Group"
    3.  "[Group]MS-Administrators-Group"
3.  JeaEndpoint の **RoleDefinitions** プロパティのグループ名を、目的のセキュリティ グループに変更します。 たとえば、Windows Admin Center 管理者ロールにアクセスを割り当てる必要があるセキュリティ グループ *CONTOSO\MyTrustedAdmins* がある場合、`'$env:COMPUTERNAME\Windows Admin Center Administrators'` を `'CONTOSO\MyTrustedAdmins'` に変更します。 更新する必要がある 3 つの文字列は次のとおりです。
    1.  '$env:COMPUTERNAME\Windows Admin Center Administrators'
    2.  '$env:COMPUTERNAME\Windows Admin Center Hyper-V Administrators'
    3.  '$env:COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> ロールごとに一意のセキュリティ グループを使用します。 同じセキュリティ グループを複数のロールに割り当てると、構成は失敗します。

次に、**InstallJeaFeatures.ps1** ファイルの末尾の、スクリプトの一番下に次の PowerShell 行を追加します。

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

最後に、モジュール、DSC リソース、構成を含むフォルダーを各ターゲット ノードにコピーすると、**InstallJeaFeature.ps1** スクリプトを実行できるようになります。
リモートの管理ワークステーションからこれを行うには、次のコマンドを実行できます。

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
