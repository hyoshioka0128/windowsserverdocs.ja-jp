---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: Windows Server 2012 の Active Directory 読み取り専用ドメイン コントローラー (RODC) をインストールする (レベル 200)
description: このトピックでは、段階的 RODC アカウントを作成して、RODC インストール中にそのアカウントにサーバーをアタッチする方法について説明します。 また、段階的インストールを実行せずに RODC をインストールする方法についても説明します。
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a46d18a0d2f589cb0ae7ee5915af0c84b0c8982f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950406"
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Windows Server 2012 の Active Directory 読み取り専用ドメイン コントローラー (RODC) をインストールする (レベル 200)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、段階的 RODC アカウントを作成して、RODC インストール中にそのアカウントにサーバーをアタッチする方法について説明します。 また、段階的インストールを実行せずに RODC をインストールする方法についても説明します。

## <a name="stage-rodc-workflow"></a>段階 RODC のワークフロー
段階的読み取り専用ドメイン コントローラー (RODC) のインストールは、以下の 2 つのフェーズで行われます。

1.  使用されていないコンピューター アカウントをステージングする

2.  昇格中に、そのアカウントに RODC をアタッチする

以下の図に、Active Directory ドメイン サービス読み取り専用ドメイン コントローラーのステージング プロセスを示します。このプロセスで、Active Directory 管理センター (Dsac.exe) を使用して、ドメイン内に空の RODC コンピューター アカウントを作成します。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)

## <a name="stage-rodc-windows-powershell"></a><a name=BKMK_StagePS></a>段階 RODC の Windows PowerShell

| ADDSDeployment コマンドレット | 引数 (**太字**の引数は必須です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。) |
|--|--|
| Add-addsreadonlydomaincontrolleraccount | -SkipPreChecks<p>***-DomainControllerAccountName***<p>***-DomainName***<p>***-SiteName***<p>*-AllowPasswordReplicationAccountName*<p>***-Credential***<p>*-DelegatedAdministratorAccountName*<p>*-DenyPasswordReplicationAccountName*<p>*-NoGlobalCatalog*<p>*-InstallDNS*<p>-ReplicationSourceDC |

> [!NOTE]
> **-credential** 引数は、Domain Admins グループのメンバーとしてログオンしていない場合にのみ必須です。

## <a name="attach-rodc-workflow"></a>RODC アタッチのワークフロー
以下の図に、Active Directory Domain Services 構成プロセスを示します。このプロセスでは、既に AD DS 役割をインストールし、RODC アカウントをステージングし、さらに新しい RODC を既存のドメイン内に作成して段階的コンピューター アカウントにアタッチするために、サーバー マネージャーを使用して [**このサーバーをドメイン コントローラーに昇格する**] を開始しました。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)

## <a name="attach-rodc-windows-powershell"></a><a name=BKMK_AttachPS></a>RODC アタッチの Windows PowerShell

| ADDSDeployment コマンドレット | 引数 (**太字**の引数が必要です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。) |
|--|--|
| Install-AddsDomaincontroller | -SkipPreChecks<p>***-DomainName***<p>*-SafeModeAdministratorPassword*<p>*-ApplicationPartitionsToReplicate*<p>*-CreateDNSDelegation*<p>***-Credential***<p>-CriticalReplicationOnly<p>*-DatabasePath*<p>*-DNSDelegationCredential*<p>*-InstallationMediaPath*<p>*-LogPath*<p>-Norebootoncompletion<p>*-ReplicationSourceDC*<p>*-SystemKey*<p>*-SYSVOLPath*<p>***-UseExistingAccount*** |

> [!NOTE]
> **-credential** 引数は、Domain Admins グループのメンバーとしてログオンしていない場合にのみ必須です。

## <a name="staging"></a>ステージング
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)

読み取り専用ドメイン コントローラー コンピューター アカウントのステージングを行うには、Active Directory 管理センター (**Dsac.exe**) を開きます。 ナビゲーション ウィンドウ内でドメインの名前をクリックします。 管理リスト内で [**ドメイン コントローラー**] をダブルクリックします。 タスク ウィンドウ内で [**読み取り専用ドメイン コントローラー アカウントの事前作成**] をクリックします。

Active Directory 管理センターの詳細については、「 [Active Directory 管理センター &#40;レベル 200&#41;を使用した高度な AD DS の管理](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)」および「Active Directory 管理センターを確認する[: はじめに](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560651(v=ws.10))」を参照してください。

読み取り専用ドメイン コントローラー作成の経験をお持ちの場合は、インストール ウィザードのグラフィカル インターフェイスが Windows Server 2008 の Active Directory ユーザーとコンピューター スナップインと同じで、さらに非推奨の dcpromo で使用される無人セットアップ ファイル形式に構成をエクスポートすることを含め同じコードを使用することにお気づきになるでしょう。

Windows Server 2012 では RODC コンピューター アカウントをステージングするための新しい ADDSDeployment コマンドレットを使用しますが、ウィザードではこの操作にコマンドレットを使用しません。 以降のセクションでは、それぞれの情報についてよりよくご理解いただくため、同じことを実行するコマンドレットと引数を示します。

Active Directory 管理センターの作業ウィンドウの [**読み取り専用ドメインコントローラーアカウントの事前作成**] リンクは、ADDSDeployment Windows PowerShell コマンドレットと同じです。

```
Add-addsreadonlydomaincontrolleraccount

```

### <a name="welcome"></a>ようこそ
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)

[**Active Directory Domain Services インストール ウィザードの開始**] ダイアログには、[**詳細モード インストールを使用する**] というオプションがあります。 このオプションを選択して [**次へ**] をクリックすると、パスワード レプリケーション ポリシー オプションが表示されます。 パスワード レプリケーション ポリシー オプションに既定値を使用するには、このオプションをオフにします (これについては、このセクションでさらに詳しく説明します)。

### <a name="network-credentials"></a>ネットワーク資格情報
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)

[**ネットワーク資格情報**] ダイアログのドメイン名オプションは、Active Directory 管理センターが既定で対象とするドメインを表示します。 既定では現在の資格情報が使用されます。 その資格情報に Domain Admins グループのメンバーシップがない場合は、[**代替の資格情報**] をクリックし、[**設定**] をクリックして、Domain Admins のメンバーであるユーザー名とパスワードをウィザードに指定してください。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-credential <pscredential>
```

ステージング システムは Windows Server 2008 R2 からの直接ポートであり、新しい Adprep 機能はありません。 段階的 RODC アカウントを展開する予定の場合は、自動 rodcprep 操作が実行されるよう、まずそのドメイン内で非段階的 RODC を展開するか、またはまず手動で adprep.exe /rodcprep を実行します。

そうしないと、adprep/rodcprep がまだ実行されていないため、このドメインに読み取り専用ドメインコントローラーをインストールできないというエラーが表示されます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)

### <a name="specify-the-computer-name"></a>コンピューター名を指定します
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)

[**コンピューター名の指定**] ダイアログでは、存在しないドメイン コントローラーの単一ラベルの [**コンピューター名**] が必要です。 後で構成してこのアカウントにアタッチするドメイン コントローラーは同じ名前にする必要があります。そうしないと昇格操作が段階的アカウントを検出できません。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-domaincontrolleraccountname <string>
```

### <a name="select-a-site"></a>サイトの選択
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)

[**サイトの選択**] ダイアログには、現在のフォレストの Active Directory サイトがリストされます。 段階的読み取り専用ドメイン コントローラー操作では、リストからサイトを 1 つ選択する必要があります。 RODC はこの情報を使って構成パーティション内に NTDS 設定オブジェクトを作成し、展開後に最初に開始されたときに正しいサイトに参加します。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-sitename <string>
```

### <a name="additional-domain-controller-options"></a>追加ドメイン コント ローラーのオプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)

[**追加のドメイン コントローラー オプション**] ダイアログでは、ドメイン コントローラーが、[**DNS サーバー**] および [**グローバル カタログ**] としても実行されることを指定できます。 Microsoft では、読み取り専用ドメイン コントローラーが DNS と GC サービスを提供することを推奨しているため、どちらも既定でインストールされます。RODC 役割の目的のひとつは支社のシナリオであり、広域ネットワークが利用できず、これらの DNS およびグローバル カタログサービスなしには支社のコンピューターが AD DS リソースと機能を使用できないような場合を想定しています。

[**読み取り専用ドメイン コントローラー (RODC)**] オプションはあらかじめ選択されており、無効化できません。 ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-installdns <string>
-NoGlobalCatalog <{$true | $false}>

```

> [!NOTE]
> 既定では、 **-NoGlobalCatalog**の値は $false です。これは、引数が指定されていない場合に、ドメインコントローラーがグローバルカタログサーバーになることを意味します。

### <a name="specify-the-password-replication-policy"></a>パスワード レプリケーション ポリシーの指定
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)

[**パスワード レプリケーション ポリシーの指定**] ダイアログでは、この読み取り専用ドメイン コントローラー上でパスワードをキャッシュすることが許可されるアカウントの既定のリストに変更を加えることができます。 リスト内で [**拒否**] に設定されたアカウントまたはリストにないアカウント (暗黙的) は、パスワードをキャッシュしません。 RODC で上のパスワードのキャッシュが許可されておらず、書き込み可能なドメイン コントローラーに接続して認証することができないアカウントは、Active Directory のリソースや機能にアクセスできません。

> [!IMPORTANT]
> このダイアログは、ウィザードの開始画面で [**詳細モード インストールを使用する**] チェック ボックスを選択した場合のみ表示されます。 このチェック ボックスをオフにすると、ウィザードは以下の既定のグループと値を使用します。
>
> -   Administrators - Deny
> -   Server Operators - Deny
> -   Backup Operators - Deny
> -   Account Operators - Deny
> -   Denied RODC Password Replication Group - Deny
> -   Allowed RODC Password Replication Group - Allow

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-allowpasswordreplicationaccountname <string []>
-denypasswordreplicationaccountname <string []>
```

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)

### <a name="delegation-of-rodc-installation-and-administration"></a>RODC のインストールと管理の委任
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)

[**RODC のインストールと管理の委任**] ダイアログでは、サーバーを RODC コンピューター アカウントにアタッチすることが許可されているユーザーまたはユーザー グループを構成することができます。 ドメイン内のユーザーまたはグループを参照するには [**設定**] をクリックします。 このダイアログで指定したユーザーまたはグループには、RODC へのローカル管理者アクセス権が与えられます。 指定されたユーザーまたは指定されたグループのメンバーは、コンピューターの管理者グループと同等の権限を持つ RODC に対して操作を実行できます。 ただし Domain Admins やドメインのビルトイン管理者グループのメンバーでは*ありません*。

このオプションを使用すると、Domain Admins グループに支社の管理者メンバーシップを与えずに支社の管理を委任することができます。 RODC 管理の委任は必須ではありません。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-delegatedadministratoraccountname <string>
```

### <a name="summary"></a>まとめ
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)

[**要約**] ダイアログでは、設定を確認することができます。 これは、ウィザードが段階的アカウントを作成する前にインストールを停止する最後の機会です。 段階的 RODC コンピューター アカウントを作成する準備ができたら [**次へ**] をクリックします。  応答ファイルを非推奨の dcpromo 無人セットアップファイル形式で保存するには、[**設定のエクスポート**] をクリックします。

### <a name="creation"></a>作成
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)

**Active Directory Domain Services インストール ウィザード**は、Active Directory 内に段階的読み取り専用ドメイン コントローラーを作成します。 この操作はいったん開始されるとキャンセルできません。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)

ADDSDeployment Windows PowerShell モジュールを使用して読み取り専用ドメイン コントローラーのコンピューター アカウントをステージングするには、以下のコマンドレットを使用します。

```
Add-addsreadonlydomaincontrolleraccount

```

必須およびオプションの引数について詳しくは、[RODC ステージングの Windows PowerShell に関する説明](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS)をご覧ください。

**Add-addsreadonlydomaincontrolleraccount** が実行するアクションは 1 つでそのフェーズは 2 つだけ (前提条件のチェックとインストール) ですので、以下のスクリーン ショットに、最低限の必須引数を使用したインストール フェーズを示します。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)

段階 RODC 操作により、Active Directory 内に RODC コンピューター アカウントが作成されます。 Active Directory 管理センターでは、[**ドメイン コントローラーの種類**] として [**使用されていないドメイン コントローラー アカウント**] と表示されます。 このドメイン コントローラーの種類は、段階的 RODC アカウントに読み取り専用ドメイン コントローラーとしてサーバーをアタッチできる準備が整っていることを示しています。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)

> [!IMPORTANT]
> サーバーを読み取り専用ドメイン コントローラーのコンピューター アカウントにアタッチするために Active Directory 管理センターを使用する必要はなくなりました。 新しい RODC をその段階的アカウントにアタッチするには、サーバー マネージャーと Active Directory Domain Services 構成ウィザードまたは ADDSDeployment Windows PowerShell モジュール コマンドレット **Install-AddsDomainController** を使用してください。 手順は新しい書き込み可能なドメイン コントローラーを既存のドメインに追加するときと同様ですが、違いは、RODC コンピューター アカウントをステージングしたときに決定した構成オプションが段階的 RODC コンピューター アカウントに含まれる点です。

## <a name="attaching"></a>アタッチ

### <a name="deployment-configuration"></a>デプロイ構成
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)

サーバー マネージャーは各ドメイン コントローラーの昇格を [**配置構成**] ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。

既存のドメインに読み取り専用のドメイン コントローラーを追加するには、[**既存のドメインにドメイン コントローラーを追加する**] を選択し、[**選択**] ボタンをクリックして [**このドメインのドメイン情報を指定する**] に進みます。 サーバー マネージャーが有効な資格情報を求めます。または [**変更**] をクリックして指定することもできます。

RODC をアタッチするには、Windows Server 2012 の Domain Admins グループのメンバーシップが必要です。 現在の資格情報に適切なアクセス許可またはグループ メンバーシップがない場合、Active Directory ドメイン サービス構成ウィザードでは後で入力を求められます。

**配置構成**の ADDSDeployment Windows PowerShell コマンドレットと引数は以下のとおりです。

```
Install-AddsDomainController
-domainname <string>
-credential <pscredential>
```

### <a name="domain-controller-options"></a>ドメイン コントローラー オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)

[**ドメイン コントローラー オプション**] ページに、新しいドメイン コントローラーのドメイン コントローラー オプションが表示されます。 このページが表示される際、Active Directory Domain Services 構成ウィザードが既存のドメイン コントローラーに LDAP クエリを送信し、使用されていないアカウントがないかどうか調べます。 現在のコンピューターと同じ名前を共有している非アクティブなドメインコントローラーコンピューターアカウントが検出された場合、ウィザードでは、**ディレクトリ内に存在する対象サーバーの名前と一致する事前に作成された RODC アカウントを読み取る情報メッセージがページの上部に表示されます。この既存の RODC アカウントを使用するか、このドメインコントローラーを再インストールするかを選択し**ます。 ウィザードは [**既存の RODC アカウントを使用する**] を既定の構成として使用します。

> [!IMPORTANT]
> ドメイン コントローラーに物理的な問題があって機能が回復できない場合は [**このドメイン コントローラーを再インストール**] を使用することができます。 これにより、Active Directory のドメイン コントローラー コンピューター アカウントとオブジェクト メタデータを残すことができるため、代わりのドメイン コントローラーの構成時間が節約できます。 新しいコンピューターを*同じ名前で*インストールし、ドメイン内のドメイン コントローラーとして昇格します。 ドメインコントローラーオブジェクトのメタデータを Active Directory から削除した場合 (メタデータのクリーンアップ)、[**このドメインコントローラーを再インストール**する] オプションは使用できません。

サーバーを RODC コンピューター アカウントにアタッチする場合はドメイン コントローラー オプションを構成できません。 段階的 RODC コンピューター アカウントを作成する際にドメイン コントローラーを構成します。

[**ディレクトリ サービスの復元モード パスワード**] には、サーバーに適用されるパスワード ポリシーに従ったパスワードを指定する必要があります。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。

**ドメイン コントローラー オプション**の ADDSDeployment Windows PowerShell 引数は以下のとおりです。

```
-UseExistingAccount <{$true | $false}>
-SafeModeAdministratorPassword <secure string>
```

> [!IMPORTANT]
> **-sitename** に引数として指定するサイト名は既に存在している必要があります。 **install-AddsDomainController** コマンドレットはサイト名を作成しません。 新しいサイトを作成するには **new-adreplicationsite** コマンドレットを使用します。

**Install-ADDSDomainController** 引数は、特に指定しない限り、サーバー マネージャーと同じ既定値を使用します。

**SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります。

-   この引数を*指定しない*場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。

    たとえば、新しい RODC を corp.contoso.com に作成し、マスクされたパスワードの入力と確認入力を求められるようにするには、以下のように実行します。

    ```
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)
    ```

-   この引数を*値と共に*指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。

たとえば、**Read-Host** コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。

```
-safemodeadministratorpassword (read-host -prompt Password: -assecurestring)

```

> [!WARNING]
> この方法ではパスワードの確認入力が行われないため、細心の注意が必要です。パスワードは表示されません。

セキュリティで保護された文字列は、変換されるクリア テキストの変数として指定することもできますが、これはお勧めしません。

```
-safemodeadministratorpassword (convertto-securestring Password1 -asplaintext -force)
```

最後に、暗号化したパスワードをファイルに保存して後で使用することができます。こうするとクリア テキストのパスワードを表示せずに済みます。 例:

```
$file = c:\pw.txt
$pw = read-host -prompt Password: -assecurestring
$pw | ConvertFrom-SecureString | Set-Content $file

-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)

```

> [!WARNING]
> クリア テキストや暗号化されたテキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。  そのファイルにアクセスできる人はだれでも、暗号化されたパスワードを元に戻すことができます。 それができると、DSRM で開始された DS にログオンでき、その後ドメイン コントローラー自体を偽装し、アクセス権を AD フォレスト内で最高レベルに昇格することができます。 テキスト ファイル データを暗号化するための **System.Security.Cryptography** の一連の使用手順を読むことが推奨されますが、ここでは取り上げません。 ベスト プラクティスは、パスワードの保存を絶対に避けることです。

### <a name="additional-options"></a>追加オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)

[**追加オプション**] ページには、レプリケーション ソースとして特定のドメイン コントローラーを指定するか、またはどのドメイン コントローラーでもレプリケーション ソースとして使用できるかを指定する構成オプションがあります。

また、メディアからのインストール (IFM) オプションを使用して、バックアップされているメディアからドメイン コントローラーをインストールすることもできます。 [**メディアからのインストール**] チェック ボックスをオンにすると参照オプションが表示されます。指定したパスが有効なメディアであることを示すため [**検証**] をクリックする必要があります。

IFM ソースのガイドライン:
*    IFM オプションによって使用されるメディアは、Windows Server バックアップまたは同じオペレーティングシステムのバージョンを持つ別の既存の Windows Server ドメインコントローラーから Ntdsutil.exe で作成されます。 たとえば、windows server 2008 R2 以前のオペレーティングシステムを使用して、Windows Server 2012 ドメインコントローラー用のメディアを作成することはできません。
*    IFM ソースデータは、書き込み可能なドメインコントローラーからのものである必要があります。 RODC からのソースは、技術的に新しい RODC の作成に使用されますが、IFM ソース RODC がレプリケートされていないことを示す偽陽性のレプリケーション警告があります。

IFM の変更内容について詳しくは、[Ntdsutil.exe メディアからのインストールの変更に関する説明](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)をご覧ください。 SYSKEY で保護されているメディアを使用する場合、サーバー マネージャーは確認の間にイメージのパスワードの入力を求めます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)

[**追加オプション**] の ADDSDeployment コマンドレット引数は以下のとおりです。

```
-replicationsourcedc <string>
-installationmediapath <string>
-systemkey <secure string>
```

### <a name="paths"></a>パス
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)

**[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所をオーバーライドできます。 既定の場所は常に %systemroot% のサブディレクトリです。 [**ドメイン コントローラー オプション**] の ADDSDeployment コマンドレット引数は以下のとおりです。

```
-databasepath <string>
-logpath <string>
-sysvolpath <string>
```

### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)

**[オプションの確認]** ページでは、インストールを開始する前に、設定を検証し、設定が要件を満たしていることを確認できます。 これがサーバー マネージャーを使用するインストールを停止する最後の機会ではありません。 このページでは、構成を続行する前に設定を検討して確認することだけができます。 サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。 これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。 例:

```
#
# Windows PowerShell Script for AD DS Deployment
#

Import-Module ADDSDeployment
Install-ADDSDomainController `
-Credential (Get-Credential) `
-CriticalReplicationOnly:$false `
-DatabasePath C:\Windows\NTDS `
-DomainName corp.contoso.com `
-LogPath C:\Windows\NTDS `
-SYSVOLPath C:\Windows\SYSVOL `
-UseExistingAccount:$true `
-Norebootoncompletion:$false
-Force:$true

```

> [!NOTE]
> サーバー マネージャーでは通常、昇格時にすべての引数とその値を入力し、既定値に依存しません (既定値は将来のバージョンの Windows 間またはサービス パック間で変わる可能性があるため)。 唯一の例外は、**-safemodeadministratorpassword** 引数です。 確認メッセージを強制するには、コマンドレットを対話的に実行する際に値を省略してください。

オプションの **Whatif** 引数を **Install-ADDSDomainController** コマンドレットで使用すると、構成情報を確認することができます。 これにより、コマンドレットの引数の明示的および暗黙的な値を見ることができます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)

### <a name="prerequisites-check"></a>前提条件のチェック
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)

[**前提条件のチェック**] は、AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバー構成が新しい AD DS フォレストをサポートできるかどうかを検証します。

新しいフォレスト ルート ドメインをインストールするときに、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードが、シリアル化された一連のモジュラー テストを呼び出します。 これらのテストでは、警告と共に、候補となる修正オプションが提示されます。 テストは必要なだけ何度でも実行できます。 ドメイン コントローラーのインストール プロセスは、すべての前提条件テストに合格するまで続行できません。

[**前提条件のチェック**] では、以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかになります。 前提条件チェックについて詳しくは、[前提条件のチェックに関する説明](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)をご覧ください。

サーバー マネージャーを使用する場合は [**前提条件のチェック**] を省略することはできませんが、AD DS 展開コマンドレットと以下の引数を使用すると省略できます。

```
-skipprechecks

```

> [!WARNING]
> ただし Microsoft では前提条件のチェックを省略することはお勧めしません。ドメイン コントローラーの昇格が部分的に行われたり、AD DS フォレストに障害が発生したりする恐れがあります。

ドメイン コントローラーの昇格プロセスを開始するには、[**インストール**] をクリックします。 ここが、インストールをキャンセルする最後のチャンスとなります。 昇格プロセスが開始されると、キャンセルすることはできません。 昇格の結果に関係なく、昇格プロセスの最後でコンピューターが自動的に再起動します。

### <a name="installation"></a>インストール
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)

[インストール] ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます。

-   %systemroot%\debug\dcpromo.log

-   %systemroot%\debug\dcpromoui.log

ADDSDeployment モジュールを使って新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。

```
Install-addsdomaincontroller

```

必須およびオプションの引数について詳しくは、[RODC アタッチの Windows PowerShell に関する説明](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS)をご覧ください。

**Install-addsdomaincontroller** コマンドレットのフェーズは 2 つだけです (前提条件のチェックとインストール)。 以下の 2 つの図は、**-domainname**、**-useexistingaccount**、および **-credential** の最低限の必須引数を使用したインストール フェーズを示しています。 **Install-ADDSDomainController** は、サーバー マネージャーと同様、昇格プロセスによって自動的にサーバーが再起動されることを知らせます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)

再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の終了時にサーバーが自動的に再起動されないようにするには、**-norebootoncompletion** 引数を使用します。

> [!WARNING]
> 再起動のオーバーライドは推奨されません。 ドメイン コントローラーを正常に機能させるには、再起動する必要があります。

### <a name="results"></a>結果
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)

[**結果**] ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 ドメイン コントローラーは、10 秒後に自動的に再起動します。

## <a name="rodc-without-staging-workflow"></a>ステージングなしの RODC のワークフロー
以下の図に、既に AD DS 役割をインストール済みで、既存の Windows Server 2012 ドメイン内に新しい非段階的読み取り専用ドメイン コントローラーを作成するためにサーバー マネージャーを使用して Active Directory ドメイン サービス構成ウィザードを開始した場合の、Active Directory ドメイン サービスの構成プロセスを示します。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)

## <a name="rodc-without-staging-windows-powershell"></a>ステージングなしの RODC の Windows PowerShell

| ADDSDeployment コマンドレット | 引数 (**太字**の引数が必要です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。) |
|--|--|
| Install-AddsDomainController | -SkipPreChecks<p>***-DomainName***<p>*-SafeModeAdministratorPassword*<p>***-SiteName***<p>*-ApplicationPartitionsToReplicate*<p>*-CreateDNSDelegation*<p>***-Credential***<p>*-CriticalReplicationOnly*<p>*-DatabasePath*<p>*-DNSDelegationCredential*<p>-DNSOnNetwork<p>*-InstallationMediaPath*<p>*-InstallDNS*<p>*-LogPath*<p>-MoveInfrastructureOperationMasterRoleIfNecessary<p>*-NoGlobalCatalog*<p>-Norebootoncompletion<p>*-ReplicationSourceDC*<p>-SkipAutoConfigureDNS<p>*-SystemKey*<p>*-SYSVOLPath*<p>*-AllowPasswordReplicationAccountName*<p>*-DelegatedAdministratorAccountName*<p>*-DenyPasswordReplicationAccountName*<p>***-ReadOnlyReplica*** |

> [!NOTE]
> **-credential** 引数は、Domain Admins グループのメンバーとしてログオンしていない場合にのみ必須です。

## <a name="rodc-without-staging-deployment"></a>ステージングなしの RODC の展開

### <a name="deployment-configuration"></a>デプロイ構成
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)

サーバー マネージャーは各ドメイン コントローラーの昇格を [**配置構成**] ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。

既存の Windows Server 2012 ドメインに非段階的な読み取り専用ドメイン コントローラーを追加するには、[**既存のドメインにドメイン コントローラーを追加する**] を選択し、[**選択**] ボタンをクリックして [**このドメインのドメイン情報を指定する**] に進みます。 サーバー マネージャーが有効な資格情報を求めます。または [**変更**] をクリックして指定することもできます。

RODC をアタッチするには、Windows Server 2012 の Domain Admins グループのメンバーシップが必要です。 現在の資格情報に適切なアクセス許可またはグループ メンバーシップがない場合、Active Directory ドメイン サービス構成ウィザードでは後で入力を求められます。

**配置構成**の ADDSDeployment Windows PowerShell コマンドレットと引数は以下のとおりです。

```
Install-AddsDomainController
-domainname <string>
-credential <pscredential>
```

### <a name="domain-controller-options"></a>ドメイン コントローラー オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)

[**ドメイン コントローラー オプション**] ページでは、新しいドメイン コントローラーのドメイン コントローラー機能を指定します。 構成可能なドメイン コントローラー機能は、**[DNS サーバー]**、**[グローバル カタログ]**、**[読み取り専用ドメイン コントローラー]** です。 Microsoft では、分散環境で高可用性を実現するため、すべてのドメイン コントローラーで、DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択されます。DNS サーバーは、現在のドメインが、Start of Authority クエリに基づいて既にその DC 上にある DNS をホストする場合に、既定で選択されます。

**[ドメイン コントローラー オプション]** ページでは、フォレストの構成から適切な Active Directory 論理**サイト名**を選択することもできます。 既定では、最も適切なサブネットのサイトが選択されます。 サイトが 1 つだけの場合は、そのサイトが自動的に選択されます。

> [!IMPORTANT]
> サーバーが Active Directory サブネットに属せず、複数の Active Directory サイトが存在する場合は、何も選択されず、リストからサイトを選択するまでは [**次へ**] ボタンが使用できません。

[**ディレクトリ サービスの復元モード パスワード**] には、サーバーに適用されるパスワード ポリシーに従ったパスワードを指定する必要があります。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。**ドメイン コントローラー オプション**の ADDSDeployment Windows PowerShell 引数は以下のとおりです

```
-UseExistingAccount <{$true | $false}>
-SafeModeAdministratorPassword <secure string>
```

> [!IMPORTANT]
> **-sitename** に引数として指定するサイト名は既に存在している必要があります。 **install-AddsDomainController** コマンドレットはサイト名を作成しません。 新しいサイトを作成するには **new-adreplicationsite** コマンドレットを使用します。

**Install-ADDSDomainController** 引数は、特に指定しない限り、サーバー マネージャーと同じ既定値を使用します。

**SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります。

-   この引数を*指定しない*場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。

    たとえば、新しい RODC を corp.contoso.com に作成し、マスクされたパスワードの入力と確認入力を求められるようにするには、以下のように実行します。

    ```
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)
    ```

-   この引数を*値と共に*指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。

たとえば、**Read-Host** コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。

```
-safemodeadministratorpassword (read-host -prompt Password: -assecurestring)

```

> [!WARNING]
> この方法ではパスワードの確認入力が行われないため、細心の注意が必要です。パスワードは表示されません。

セキュリティで保護された文字列は、変換されるクリア テキストの変数として指定することもできますが、これはお勧めしません。

```
-safemodeadministratorpassword (convertto-securestring Password1 -asplaintext -force)
```

最後に、暗号化したパスワードをファイルに保存して後で使用することができます。こうするとクリア テキストのパスワードを表示せずに済みます。 例:

```
$file = c:\pw.txt
$pw = read-host -prompt Password: -assecurestring
$pw | ConvertFrom-SecureString | Set-Content $file

-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)

```

> [!WARNING]
> クリア テキストや暗号化されたテキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。  そのファイルにアクセスできる人はだれでも、暗号化されたパスワードを元に戻すことができます。 それができると、DSRM で開始された DS にログオンでき、その後ドメイン コントローラー自体を偽装し、アクセス権を AD フォレスト内で最高レベルに昇格することができます。 テキスト ファイル データを暗号化するための **System.Security.Cryptography** の一連の使用手順を読むことが推奨されますが、ここでは取り上げません。 ベスト プラクティスは、パスワードの保存を絶対に避けることです。

### <a name="rodc-options"></a>RODC オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)

[**RODC オプション**] ページでは、以下の設定を変更することができます

-   委任済みの管理者アカウント

-   パスワードを RODC にレプリケートすることが許可されているアカウント

-   パスワードを RODC にレプリケートすることが許可されていないアカウント

委任される管理者アカウントには、RODC に対するローカル管理アクセス許可が与えられます。 これらのユーザーは、ローカルコンピューターの Administrators グループに相当する特権を使用して操作できます。  これらのユーザーは、Domain Admins グループまたはドメインの組み込みの Administrator グループのメンバーではありません。 このオプションは、ドメインの管理アクセス許可を与えることなく支社の管理を委任する場合に便利です。 管理の委任の構成は必要ありません。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-delegatedadministratoraccountname <string>
```

RODC で上のパスワードのキャッシュが許可されておらず、書き込み可能なドメイン コントローラーに接続して認証することができないアカウントは、Active Directory のリソースや機能にアクセスできません。

> [!IMPORTANT]
> 変更しないと、既定のグループと設定が使用されます。
>
> -   Administrators - Deny
> -   Server Operators - Deny
> -   Backup Operators - Deny
> -   Account Operators - Deny
> -   Denied RODC Password Replication Group - Deny
> -   Allowed RODC Password Replication Group - Allow

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-allowpasswordreplicationaccountname <string []>
-denypasswordreplicationaccountname <string []>
```

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)

### <a name="additional-options"></a>追加オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)

[**追加オプション**] ページには、レプリケーション ソースとして特定のドメイン コントローラーを指定するか、またはどのドメイン コントローラーでもレプリケーション ソースとして使用できるかを指定する構成オプションがあります。

また、メディアからのインストール (IFM) オプションを使用して、バックアップされているメディアからドメイン コントローラーをインストールすることもできます。 [**メディアからのインストール**] チェック ボックスをオンにすると参照オプションが表示されます。指定したパスが有効なメディアであることを示すため [**検証**] をクリックする必要があります。

IFM ソースのガイドライン:
*    IFM オプションによって使用されるメディアは、Windows Server バックアップまたは同じオペレーティングシステムのバージョンを持つ別の既存の Windows Server ドメインコントローラーから Ntdsutil.exe で作成されます。 たとえば、windows server 2008 R2 以前のオペレーティングシステムを使用して、Windows Server 2012 ドメインコントローラー用のメディアを作成することはできません。
*    IFM ソースデータは、書き込み可能なドメインコントローラーからのものである必要があります。 RODC からのソースは、技術的に新しい RODC の作成に使用されますが、IFM ソース RODC がレプリケートされていないことを示す偽陽性のレプリケーション警告があります。

IFM の変更内容について詳しくは、[Ntdsutil.exe メディアからのインストールの変更に関する説明](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)をご覧ください。 SYSKEY で保護されているメディアを使用する場合、サーバー マネージャーは確認の間にイメージのパスワードの入力を求めます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)

[追加オプション] の ADDSDeployment コマンドレット引数は以下のとおりです。

```
-replicationsourcedc <string>
-installationmediapath <string>
-systemkey <secure string>
```

### <a name="paths"></a>パス
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)

**[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所をオーバーライドできます。 既定の場所は常に %systemroot% のサブディレクトリです。 [**ドメイン コントローラー オプション**] の ADDSDeployment コマンドレット引数は以下のとおりです。

```
-databasepath <string>
-logpath <string>
-sysvolpath <string>
```

### <a name="preparation-options"></a>準備オプション
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)

[**準備オプション**] ページでは、AD DS 構成に、スキーマの拡張 (forestprep) とドメインの更新 (domainprep) が含まれることが通知されます。 このページは、フォレストまたはドメインが、以前の Windows Server 2012 ドメイン コントローラー インストールまたは手動で実行された Adprep.exe で準備されていない場合のみ表示されます。 たとえば、既存の Windows Server 2012 フォレストのルート ドメインに新しいレプリカ ドメイン コントローラーを追加した場合は、Active Directory ドメイン サービス構成ウィザードにこのページが表示されません。

[**次へ**] をクリックしても、スキーマの拡張やドメインの更新は実行されません。 これらのイベントは、インストール フェーズでのみ発生します。 このページの目的は、インストール中の後の段階で発生するイベントについて通知することだけです。

このページでは、現在のユーザーの資格情報が Schema Admin と Enterprise Admins グループのメンバーであるかどうかも確認します。これは、ドメイン準備のためにスキーマを拡張するにはこれらのグループのメンバーシップが必要であるためです。 現在の資格情報に十分なアクセス権がないと表示された場合は、[**変更**] をクリックして適切なユーザー資格情報を指定してください。

[追加オプション] の ADDSDeployment コマンドレットの引数は以下のとおりです。

```
-adprepcredential <pscredential>
```

> [!IMPORTANT]
> 以前のバージョンの Windows Server と同様、Windows Server 2012 の自動ドメイン準備では GPPREP は実行されません。 Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 用に準備されていないすべてのドメインに対して、**adprep.exe /gpprep** を手動で実行してください。 特定のドメインに対して 1 度だけ (アップグレードのたびにではなく) GPPrep を実行する必要があります。 Adprep.exe は /gpprep を自動的に実行しません。これは、その操作により SYSVOL フォルダー内のすべてのファイルとフォルダーがすべてのドメイン コントローラー上で再レプリケートされる可能性があるためです。
>
> 自動 RODCPrep は、ドメイン内で最初の非段階的 RODC を昇格したときに実行されます。 最初の書き込み可能な Windows Server 2012 ドメイン コントローラーを昇格したときには実行されません。 読み取り専用ドメイン コントローラーを展開する予定がある場合は、手動で **adprep.exe /rodcprep** を実行することもできます。

### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)

**[オプションの確認]** ページでは、インストールを開始する前に、設定を検証し、設定が要件を満たしていることを確認できます。 これがサーバー マネージャーを使用するインストールを停止する最後の機会ではありません。 このページでは、構成を続行する前に設定を検討して確認することだけができます。

サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。 これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。 例:

```
#
# Windows PowerShell Script for AD DS Deployment
#

Import-Module ADDSDeployment
Install-ADDSDomainController `
-AllowPasswordReplicationAccountName @(CORP\Allowed RODC Password Replication Group, CORP\Chicago RODC Admins, CORP\Chicago RODC Users and Computers) `
-Credential (Get-Credential) `
-CriticalReplicationOnly:$false `
-DatabasePath C:\Windows\NTDS `
-DelegatedAdministratorAccountName CORP\Chicago RODC Admins `
-DenyPasswordReplicationAccountName @(BUILTIN\Administrators, BUILTIN\Server Operators, BUILTIN\Backup Operators, BUILTIN\Account Operators, CORP\Denied RODC Password Replication Group) `
-DomainName corp.contoso.com `
-InstallDNS:$true `
-LogPath C:\Windows\NTDS `
-ReadOnlyReplica:$true `
-SiteName Default-First-Site-Name `
-SYSVOLPath C:\Windows\SYSVOL
-Force:$true

```

> [!NOTE]
> サーバー マネージャーでは通常、昇格時にすべての引数とその値を入力し、既定値に依存しません (既定値は将来のバージョンの Windows 間またはサービス パック間で変わる可能性があるため)。 唯一の例外は、**-safemodeadministratorpassword** 引数です。 確認プロンプトを強制的に表示するには、コマンドレットを対話的に実行するときに値を省略します。

オプションの Whatif 引数を Install-ADDSDomainController コマンドレットで使用すると、構成情報を確認することができます。 これにより、コマンドレットの引数の明示的および暗黙的な値を見ることができます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)

### <a name="prerequisites-check"></a>前提条件のチェック
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)

[**前提条件のチェック**] は、AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバー構成が新しい AD DS フォレストをサポートできるかどうかを検証します。

新しいフォレスト ルート ドメインをインストールするときに、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードが、シリアル化された一連のモジュラー テストを呼び出します。 これらのテストでは、警告と共に、候補となる修正オプションが提示されます。 テストは必要なだけ何度でも実行できます。 前提条件のテストにすべて合格するまで、ドメイン コントローラー プロセスを続行することはできません。

[**前提条件のチェック**] では、以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかになります。

サーバー マネージャーを使用する場合は [**前提条件のチェック**] を省略することはできませんが、AD DS 展開コマンドレットと以下の引数を使用すると省略できます。

```
-skipprechecks

```

ドメイン コントローラーの昇格プロセスを開始するには、[**インストール**] をクリックします。 ここが、インストールをキャンセルする最後のチャンスとなります。 昇格プロセスが開始されると、キャンセルすることはできません。 昇格の結果に関係なく、昇格プロセスの最後でコンピューターが自動的に再起動します。

### <a name="installation"></a>インストール
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)

[**インストール**] ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます。

-   %systemroot%\debug\dcpromo.log

-   %systemroot%\debug\dcpromoui.log

ADDSDeployment モジュールを使って新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。

```
Install-addsdomaincontroller

```

必須およびオプションの引数については、このセクションの最初にある **ADDSDeployment コマンドレット**の表をご覧ください。

**Install-addsdomaincontroller** コマンドレットのフェーズは 2 つだけです (前提条件のチェックとインストール)。 以下の 2 つの図は、**-domainname**、**-readonlyreplica**、**-sitename**、および **-credential** の最低限の必須引数を使用したインストール フェーズを示しています。 **Install-ADDSDomainController** は、サーバー マネージャーと同様、昇格プロセスによって自動的にサーバーが再起動されることを知らせます。

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)

![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)

再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の終了時にサーバーが自動的に再起動されないようにするには、**-norebootoncompletion** 引数を使用します。

> [!WARNING]
> 再起動のオーバーライドはお勧めしません。 ドメイン コントローラーを正常に機能させるには、再起動する必要があります。 ドメイン コントローラーからログオフすると、再起動するまで、対話的にログオンし直すことはできません。

### <a name="results"></a>結果
![RODC のインストール](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)

[**結果**] ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 ドメイン コントローラーは、10 秒後に自動的に再起動します。
