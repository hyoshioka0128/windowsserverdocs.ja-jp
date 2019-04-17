---
title: ユーザー アクセスの制御とアクセス許可を構成します。
description: ユーザー アクセスの制御と Active Directory または Azure AD (Project Honolulu) を使用してアクセス許可を構成する方法について説明します
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/19/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b19657f4ce1a1a2cfb94f7234f07805ba0abd42c
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2019
ms.locfileid: "9152047"
---
# ユーザー アクセスの制御とアクセス許可を構成します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

まだ理解[Windows Admin Center でのユーザー アクセス制御のオプション](../plan/user-access-options.md)

>[!NOTE]
> ワークグループ環境または信頼関係のないドメイン間では、Windows Admin Center でグループ ベースのアクセスはサポートされていません。

## ゲートウェイ アクセス ロールの定義

これには、Windows Admin Center ゲートウェイ サービスにアクセスするための 2 つのロールがあります。

**ゲートウェイのユーザー**がそのゲートウェイを介してサーバーを管理する、Windows Admin Center ゲートウェイ サービスに接続できますが、アクセス許可もゲートウェイへの認証に使用される認証メカニズムは変更できません。

**ゲートウェイの管理者**は、ゲートウェイへのユーザーの認証方法と同様のアクセスを取得した構成できます。 管理者のみがゲートウェイでは、表示でき、Windows Admin Center で、アクセスの設定を構成することができます。 ゲートウェイ マシン上のローカル管理者は、Windows Admin Center ゲートウェイ サービスの管理者では常にします。

> [!NOTE]
> ゲートウェイへのアクセスわけではありません表示されている管理対象サーバーへのアクセス、ゲートウェイによってします。 接続ユーザー ターゲット サーバーを管理するには、(またはを自分で渡される Windows 資格情報**としての管理**アクションを使用して Windows Admin Center セッションで提供されている資格情報を使用) を持つ資格情報の管理アクセスを使う必要があります。そのターゲット サーバー。

## Active Directory またはローカル コンピューター グループ

既定では、Active Directory またはローカル コンピューターのグループはゲートウェイ アクセスの制御に使用します。 ゲートウェイ ユーザーと管理者を管理できる場合は、Active Directory ドメインがある場合は、Windows Admin Center インターフェイス内からアクセスします。

[**ユーザー** ] タブは、ゲートウェイ ユーザーとして Windows Admin Center にアクセスできるユーザーを制御できます。 既定では、ゲートウェイ URL にアクセスするすべてのユーザーがアクセスを持つセキュリティ グループを指定しない場合があるとします。 1 つまたは複数のセキュリティ グループをユーザーの一覧に追加すると、アクセスは、これらのグループのメンバーに制限されます。

アクセスはによって制御されている環境内で Active Directory ドメインを使わない場合、```Users```と```Administrators```Windows Admin Center ゲートウェイ マシン上のローカル グループです。

### スマート カード認証

スマート カード ベースのセキュリティ グループの追加_必須_のグループを指定することで、**スマート カード認証**を適用できます。 スマート カード ベースのセキュリティ グループを追加すると、ユーザーのみサービスにアクセスできます Windows Admin Center のセキュリティ グループのメンバーになっていると、スマート カードのグループは、ユーザーの一覧に含まれている場合。

[**管理者**] タブで、ゲートウェイの管理者として Windows Admin Center にアクセスできるユーザーを制御できます。 コンピューターのローカル administrators グループは、完全な管理者のアクセス権を常にあり、一覧から削除することはできません。 セキュリティ グループを追加すると、それらのグループの特権の Windows Admin Center ゲートウェイ設定を変更するメンバーを提供します。 管理者の一覧は、ユーザーの一覧と同じ方法でスマート カード認証をサポートしています: セキュリティ グループとスマート カードのグループに対して AND 条件とします。

## Azure Active Directory

組織では、Azure Active Directory (Azure AD) を使用している場合は、ゲートウェイにアクセスする Azure AD 認証を要求することで Windows Admin Center に**追加**のセキュリティ層を追加することもできます。 Windows Admin Center にアクセスするために、ユーザーの**Windows アカウント**も必要がありますゲートウェイ サーバーへのアクセス (でも Azure AD authentication を使用)。 Azure AD を使用する場合は、内からではなく、Azure ポータルから Windows Admin Center のユーザーと管理者のアクセス許可を管理するが、Windows Admin Center の UI。

### Windows Admin Center にアクセスする Azure AD 認証を有効にします。

によって、ブラウザーを使用すると、一部のユーザーへのアクセスの Windows Admin Center に構成されている Azure AD 認証は、追加プロンプト受信 **、ブラウザーから**Windows を提供する必要がありますアカウントの資格情報のコンピューターWindows Admin Center をインストールします。 その情報を入力すると、ユーザーは、Azure で Azure AD アプリケーションのアクセスが与えられている Azure アカウントの資格情報を必要と追加 Azure Active Directory の認証プロンプトを取得します。

> [!NOTE]
> ユーザーの Windows アカウントを持つ**管理者権限**をゲートウェイ マシンは、Azure AD 認証を求められません。

### Windows Admin Center Preview の Azure Active Directory の認証を構成します。

Windows Admin Center**の設定**に移動 > **アクセス**し、使用を有効にするトグル スイッチ"を使用して、ゲートウェイにセキュリティのレイヤーを追加する Azure Active Directory"します。 ゲートウェイを Azure が登録されていない場合は、そのためにはこの時点でガイドします。

既定では、Azure AD テナントのすべてのメンバーは、Windows Admin Center ゲートウェイ サービスに対するユーザー アクセスを必要します。 ローカル管理者のみが、ゲートウェイ マシンで Windows Admin Center ゲートウェイに管理者のアクセス権があります。 ゲートウェイ マシンでローカル管理者の権限を制限することはできません - ローカルの管理者が行う認証に Azure AD を使用するかどうかに関係なく何も注意してください。

特定の Azure AD ユーザーまたはグループのゲートウェイ ユーザーまたはゲートウェイ管理者が Windows Admin Center サービスにアクセスする場合は、次の操作を行う必要があります。

1.  アクセスの設定で提供されるハイパーリンクを使用して、Azure portal で、Windows Admin Center Azure AD アプリケーションに移動します。 このハイパーリンクは、Azure Active Directory の認証が有効になっている場合にのみ利用可能なに注意してください。 
    -   **Azure Active Directory**に移動して、Azure portal で、アプリケーションを検索することもできます > **エンタープライズ アプリケーション** > **すべてのアプリケーション**と検索**WindowsAdminCenter** (Azure AD アプリケーションの名前はWindowsAdminCenter-<gateway name>)。 検索結果を取得する、**すべて**のアプリケーションの設定**を表示する**には、**アプリケーションの状態**が**任意**に設定していない適用] をクリックしてする場合、は、検索してください。 アプリケーションが決まったらが**ユーザーとグループ**に移動します。
2.  [プロパティ] タブで [はい] に**ユーザーの割り当てが必要な**を設定します。
    この操作が完了したら、**ユーザーとグループ**] タブに表示されているメンバーだけが Windows Admin Center ゲートウェイにアクセスできるされます。
3.  [ユーザーとグループ] タブで、**ユーザーの追加**を選択します。 ゲートウェイのユーザーまたはユーザー グループごとに/追加ゲートウェイ管理者ロールを割り当てる必要があります。

Azure AD 認証を有効にすると、ゲートウェイ サービスを再起動しては、ブラウザーを更新する必要があります。 Azure portal で、いつでも SME Azure AD アプリケーションのユーザー アクセスを更新することができます。

ユーザーは Windows Admin Center ゲートウェイ URL へのアクセスしようとすると、Azure Active Directory の id を使用してサインインを求められます。 ユーザーが Windows Admin Center にアクセスするゲートウェイ サーバー上のローカル ユーザーのメンバーにある必要がありますも注意してください。

ユーザーと管理者は、現在ログインしているアカウントを表示しとサインアウトもこの Azure AD のアカウントの Windows の [**アカウント**] タブ管理センターの設定。

### Windows Admin Center の Azure Active Directory の認証を構成します。

[Azure AD の認証を設定する、ゲートウェイを Azure を最初に登録する必要があります。](azure-integration.md)(必要だけこれを行うに 1 回、Windows Admin Center ゲートウェイの) です。 この手順では、ゲートウェイ ユーザーおよびゲートウェイ管理者のアクセスを管理できる Azure AD アプリケーションを作成します。

特定の Azure AD ユーザーまたはグループのゲートウェイ ユーザーまたはゲートウェイ管理者が Windows Admin Center サービスにアクセスする場合は、次の操作を行う必要があります。

1.  Azure portal で SME Azure AD アプリケーションに移動します。 
    -   **アクセス制御の変更**] をクリックし、Windows Admin Center へのアクセスの設定から**Azure Active Directory**を選択すると、Azure portal で Azure AD アプリケーションにアクセスするのに UI で提供されるハイパーリンクを使用できます。 このハイパーリンクは、保存] をクリックして、アクセス制御の id プロバイダーとして Azure AD を選択した後にもアクセスの設定で利用できます。
    -   **Azure Active Directory**に移動して、Azure portal で、アプリケーションを検索することもできます > **エンタープライズ アプリケーション** > **すべてのアプリケーション**と検索**SME** (Azure AD アプリケーションの名前は SME -<gateway>)。 検索結果を取得する、**すべて**のアプリケーションの設定**を表示する**には、**アプリケーションの状態**が**任意**に設定していない適用] をクリックしてする場合、は、検索してください。 アプリケーションが決まったらが**ユーザーとグループ**に移動します。
2.  [プロパティ] タブで [はい] に**ユーザーの割り当てが必要な**を設定します。
    この操作が完了したら、**ユーザーとグループ**] タブに表示されているメンバーだけが Windows Admin Center ゲートウェイにアクセスできるされます。
3.  [ユーザーとグループ] タブで、**ユーザーの追加**を選択します。 ゲートウェイのユーザーまたはユーザー グループごとに/追加ゲートウェイ管理者ロールを割り当てる必要があります。

Azure AD アクセス制御の保存と**アクセス管理の変更**のウィンドウで、ゲートウェイ サービスが開始されるとする必要がありますブラウザーを更新します。 いつでもでも、Azure portal で Windows Admin Center Azure AD アプリケーションのユーザー アクセスを更新することができます。 

ユーザーは Windows Admin Center ゲートウェイ URL へのアクセスしようとすると、Azure Active Directory の id を使用してサインインを求められます。 ユーザーが Windows Admin Center にアクセスするゲートウェイ サーバー上のローカル ユーザーのメンバーにある必要がありますも注意してください。 

Windows Admin Center の一般的な設定の [ **Azure** ] タブを使用して、ユーザーと管理者表示できる、現在ログインしているアカウント、この Azure AD アカウントのほか、サインアウトします。

### 条件付きアクセスし、多要素認証

追加のセキュリティ層と Azure AD を使用して Windows Admin Center ゲートウェイへのアクセスを制御する利点の 1 つは、条件付きアクセスし、多要素認証などの Azure AD の強力なセキュリティ機能を活用することができます。 

[Azure Active Directory の条件付きアクセスの構成について説明します。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## シングル サインオンを構成します。

**シングル サインオン展開されると Windows Server 上のサービスとして**

Windows 10 で Windows Admin Center をインストールするときは、シングル サインオンを使用する準備が。 Windows Server で Windows Admin Center を使用する場合は、シングル サインオンを使用する前に、いくつかの形式の環境での Kerberos 委任を設定する必要があります。 委任は、ターゲット ノードに委任するには、信頼としてゲートウェイ コンピューターを構成します。 

環境内で[リソースに基づく制約付き委任](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)を構成するには、次の PowerShell コマンドレットを実行します。 (Windows Server 2012 を実行しているドメイン コント ローラーが必要である対応以降である)。

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

この例では、Windows Admin Center ゲートウェイが**WindowsAdminCenterGW**サーバーにインストールされているし、ターゲット ノード名は**ManagedNode**します。

この関係を削除するには、次のコマンドレットを実行します。

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## ロール ベースのアクセス制御

役割ベースのアクセス制御を使用すると、それらの完全なローカル管理者を作成するのではなく、コンピューターへのアクセス制限をユーザーに提供できます。
[役割ベースのアクセス制御と使用可能なロールについて詳しくは、します。](../plan/user-access-options.md#role-based-access-control)

2 つのステップから成る RBAC の設定: ターゲット コンピューターでのサポートを有効にして、関連する役割をユーザーに割り当てることです。

> [!TIP]
> 確認のコンピューターにローカル管理者権限がある役割ベースのアクセス制御のサポートを構成します。

### 役割ベースのアクセス制御を 1 台のコンピューターに適用されます。

1 台のコンピューター展開モデルは、数台のコンピューターを管理するだけでシンプルな環境に最適です。
役割ベースのアクセス制御のサポートを使ったコンピューターの構成とすると、次の変更が発生します。
-   Windows Admin Center に必要な関数と PowerShell モジュールをシステム ドライブでのインストールは`C:\Program Files\WindowsPowerShell\Modules`します。 すべてのモジュールが**Microsoft.Sme**で開始されます。
-   目的の状態の構成は、コンピューター、 **Microsoft.Sme.PowerShell**という名前の Just Enough Administration エンドポイントを構成する 1 回限りの構成が実行されます。 このエンドポイントは、Windows Admin Center で使われる 3 つの役割を定義し、ユーザーが接続するときに一時的なローカル管理者として実行します。
-   どのユーザーでは、どのロールに割り当てられたアクセスはコントロールには、3 つの新しいローカル グループが作成されます。
    -   Windows Admin Center 管理者
    -   Windows Admin Center での HYPER-V の管理者
    -   Windows Admin Center リーダー

単一コンピューター上で役割ベースのアクセス制御のサポートを有効にするには、これらの手順に従います。

1.  Windows Admin Center を起動し、役割ベースのアクセスの制御をターゲット コンピューター上のローカル管理者特権を持つアカウントを使用して構成するコンピューターに接続します。
2.  **概要**ツールでは、[**設定**] をクリックして > **役割ベースのアクセス制御**します。
3.  ターゲット コンピューター上で役割ベースのアクセス制御のサポートを有効にする、ページの下部に**適用**] をクリックします。 アプリケーションのプロセスには、ターゲット コンピューター上の PowerShell スクリプトをコピーし、(PowerShell Desired State Configuration を使用して) 構成の呼び出しが含まれます。 完了するには最大 10 分かかりますと WinRM 再起動が発生します。 これにより、Windows Admin Center、PowerShell、および WMI のユーザーが一時的に切断します。
4.  ページを更新して役割ベースのアクセス制御の状態を確認します。 使用できる状態になりますが、**適用**する状態が変更されます。

構成が適用されると、ロールにユーザーを割り当てることができます。

1.  **ローカル ユーザーとグループ**のツールを開き、[**グループ**] タブに移動します。
2.  **Windows Admin Center リーダー**グループを選択します。
3.  *詳細*ウィンドウで、下部にある、**ユーザーの追加**] をクリックし、Windows Admin Center を通じてサーバーへの読み取り専用のアクセスを付与するユーザーまたはセキュリティ グループの名前を入力します。 ユーザーとグループは、ローカル コンピューターまたは Active Directory ドメインから取得できます。
4.  **Windows Admin Center で HYPER-V の管理者**と**Windows Admin Center の管理者**グループの手順 2 ~ 3 を繰り返します。

[制限付きのグループ ポリシー設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)で、グループ ポリシー オブジェクトを構成することによって、ドメイン間でこれらのグループを一貫して記入することもできます。

### 複数のコンピューターに役割ベースのアクセス制御を適用します。

大規模なエンタープライズ展開では、Windows Admin Center ゲートウェイから、構成パッケージをダウンロードして、コンピューターに役割ベースのアクセスの制御機能をプッシュする、既存の自動化ツールを使用することができます。
PowerShell Desired State Configuration と共に使用して、構成パッケージが設計されていますが、優先するオートメーション ソリューションと連携するように対応することができます。

#### 役割ベースのアクセス制御の構成をダウンロードします。

役割ベースのアクセス制御の構成パッケージをダウンロードするには、Windows Admin Center と PowerShell プロンプトにアクセスする必要があります。

Windows Server では、サービス モードで Windows Admin Center ゲートウェイを実行している場合、は、構成パッケージをダウンロードする次のコマンドを使用します。
必ず、環境用の適切なもので、ゲートウェイ アドレスを更新してください。

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

を、Windows 10 コンピューターで Windows Admin Center ゲートウェイを実行している場合は、代わりに、次のコマンドを実行します。

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Zip アーカイブを展開すると、次のフォルダー構造が表示されます。
- InstallJeaFeatures.ps1
- JustEnoughAdministration (ディレクトリ)
- モジュール (ディレクトリ)
    - Microsoft.SME.\* (ディレクトリ)
    - WindowsAdminCenter.Jea (ディレクトリ)

ノード上で役割ベースのアクセス制御のサポートを構成するには、次の操作を実行する必要があります。
1.  JustEnoughAdministration、Microsoft.SME.\*、および WindowsAdminCenter.Jea モジュールは、ターゲット コンピューター上の PowerShell モジュール ディレクトリにコピーします。 通常、これがある`C:\Program Files\WindowsPowerShell\Modules`します。
2.  RBAC エンドポイントの適切な構成と一致する**InstallJeaFeature.ps1**ファイルを更新します。
3.  DSC リソースをコンパイルする InstallJeaFeature.ps1 を実行します。
4.  すべてのコンピューターの構成を適用するには、DSC 構成を展開します。

次のセクションでは、PowerShell リモート処理を使ってこれを実行する方法について説明します。

#### 複数のコンピューターでの展開します。

複数のコンピューターにダウンロードする構成を展開することを必要があります環境内の適切なセキュリティ グループに含める**InstallJeaFeatures.ps1**スクリプトを更新する各コンピューター、ファイルをコピーし、呼び出す、構成スクリプトです。
この記事では、純粋な PowerShell ベースのアプローチに重点が、これを実現するのに、優先するオートメーション ツールを使用できます。

既定では、設定のスクリプトは、それぞれの役割へのアクセスを制御するコンピューターで、ローカル セキュリティ グループを作成します。
これはワークグループに適したであり、ドメイン参加しているコンピューターが直接する可能性がありますドメインのみの環境で展開する場合は、各ロールにドメインのセキュリティ グループを関連付けます。
ドメインのセキュリティ グループを使用して構成を更新するには、 **InstallJeaFeatures.ps1**を開き、次を変更します。

1.  3 つの**グループ**のリソース ファイルから削除します。
    1.  「グループ MS リーダー グループ」
    2.  「グループ MS ・ Hyper V-管理者のグループ」
    3.  「グループ MS Administrators グループ」
2.  JeaEndpoint**によって異なります**プロパティから 3 つのグループのリソースを削除します。
    1.  「[グループ] MS ・ リーダー グループ」
    2.  「[グループ] MS ・ Hyper V の管理者のグループ」
    3.  「[グループ] MS Administrators」
3.  必要なセキュリティ グループに JeaEndpoint **RoleDefinitions**プロパティ内のグループ名を変更します。 たとえば、ある場合は、セキュリティ グループ*CONTOSO\MyTrustedAdmins* Windows Admin Center の管理者ロールにアクセスを割り当てる必要がありますが、変更`'$env:COMPUTERNAME\Windows Admin Center Administrators'`に`'CONTOSO\MyTrustedAdmins'`します。 更新する必要がある 3 つの文字列は次のとおりです。
    1.  ' $env: COMPUTERNAME\Windows Admin Center の管理者
    2.  ' $env: COMPUTERNAME\Windows Admin Center で HYPER-V 管理者
    3.  ' $env: COMPUTERNAME\Windows Admin Center リーダーの

> [!NOTE]
> ロールごとに一意のセキュリティ グループを使用することを確認します。 構成には、同じセキュリティ グループが複数のロールに割り当てられている場合は失敗します。

次に、 **InstallJeaFeatures.ps1**ファイルの末尾には、スクリプトの下に次の PowerShell の行を追加します。

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

最後に、モジュール、DSC リソースおよび各ターゲット ノードに構成が含まれているフォルダーをコピーし、 **InstallJeaFeature.ps1**スクリプトを実行できます。
これを行うにリモートで管理ワークステーションから、次のコマンドを実行できます。

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
