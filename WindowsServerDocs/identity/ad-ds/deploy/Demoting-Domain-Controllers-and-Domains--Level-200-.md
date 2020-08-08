---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: ドメイン コントローラーとドメインの降格 (レベル 200)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.openlocfilehash: d9be9555c3e72b13fb86509289ee7459f4d1b687
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959390"
---
# <a name="demoting-domain-controllers-and-domains"></a>ドメインコントローラーとドメインの降格

> 適用先:Windows Server

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して AD DC を削除する方法について説明します。

## <a name="ad-ds-removal-workflow"></a>AD DS 削除のワークフロー

![AD DS 削除ワークフローのグラフ](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)

> [!CAUTION]
> ドメイン コントローラーに昇格した後に Dism.exe または Windows PowerShell DISM モジュールを使用して AD DS 役割を削除することはサポートされておらず、サーバーの正常な起動を妨げます。
>
> サーバー マネージャーや Windows PowerShell の ADDSDeployment モジュールと異なり、DISM は、AD DS やその構成に関する知識を引き継がないネイティブ サービシング システムです。 サーバーがドメイン コントローラーでなくなる場合を除き、AD DS の役割をアンインストールするのに Dism.exe または Windows PowerShell の DISM モジュールを使用しないでください。

## <a name="demotion-and-role-removal-with-powershell"></a>PowerShell を使用した降格とロールの削除

| ADDSDeployment と ServerManager コマンドレット | 引数 (**太字**の引数は必須です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。) |
|--|--|
| Uninstall-addsdomaincontroller | -SkipPreChecks<p>*-LocalAdministratorPassword*<p>-Confirm<p>***-Credential***<p>-DemoteOperationMasterRole<p>*-DNSDelegationRemovalCredential*<p>-Force<p>*-ForceRemoval*<p>*-IgnoreLastDCInDomainMismatch*<p>*-IgnoreLastDNSServerForZone*<p>*-LastDomainControllerInDomain*<p>-Norebootoncompletion<p>*-RemoveApplicationPartitions*<p>*-RemoveDNSDelegation*<p>-RetainDCMetadata |
| Uninstall-WindowsFeature/Remove-WindowsFeature | ***-Name***<p>***-IncludeManagementTools***<p>*-再起動*<p>-Remove<p>-Force<p>-ComputerName<p>-Credential<p>-LogPath<p>-Vhd |

> [!NOTE]
> **-credential** 引数は、Enterprise Admins グループ (ドメイン内の最後の DC を降格) または Domain Admins グループ (レプリカ DC を降格) のメンバーとしてログインしていない場合のみ必須です。**-includemanagementtools** 引数は、すべての AD DC 管理ユーティリティーを削除する場合のみ必須です。

## <a name="demote"></a>降格

### <a name="remove-roles-and-features"></a>役割と機能の削除

サーバー マネージャーには、Active Directory ドメイン サービスの役割を削除するためのインターフェイスが 2 つあります。

* メイン ダッシュボードの、[**管理**] メニューの [**役割と機能の削除**] を使用します。

   ![サーバーマネージャー-役割と機能を削除する](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)

* ナビゲーション ウィンドウの [**AD DS**] または [**すべてのサーバー**] をクリックします。 [**役割と機能**] のセクションにスクロール ダウンします。 [**役割と機能**] リスト内で [**Active Directory ドメイン サービス**] を右クリックし、[**役割または機能の削除**] をクリックします。 このインターフェイスでは、[**サーバーの選択**] ページは使用しません。

   ![サーバーマネージャー-すべてのサーバー-役割と機能を削除する](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)

ServerManager コマンドレット、および**add-windowsfeature**を使用すると、ドメインコントローラーを降格するまで AD DS の役割を削除できなく**なります。**

### <a name="server-selection"></a>サーバーの選択

![役割と機能の削除ウィザード移行先サーバーの選択](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)

[**サーバーの選択**] ダイアログでは、プールに追加済みのサーバーから 1 つ、アクセス可能なものに限り選択することができます。 サーバー マネージャーを実行するローカル サーバーは常に、自動的にアクセス可能となります。

### <a name="server-roles-and-features"></a>サーバーの役割と機能

![役割と機能の削除ウィザード-削除する役割を選択します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)

ドメイン コントローラーを降格するため、[**Active Directory ドメイン サービス**] チェック ボックスをオフにします。サーバーが現在ドメイン コントローラーである場合は、この操作では AD DS 役割は削除されません。代わりに [**検証結果**] ダイアログが開き、ここで降格を実行できます。 それ以外の場合は、他の役割機能と同様にバイナリを削除します。

* この後すぐにまたドメイン コントローラーを昇格する予定がある場合は、DNS、GPMC、RSAT ツールなどの、ほかの AD DS 関連の役割や機能を削除しないでください。 ほかの役割や機能を削除すると、役割を再インストールする際、サーバー マネージャーがそれらの機能を再インストールするため、再昇格に時間がかかります。
* ドメイン コントローラーを再昇格する予定がない場合は、不要な AD DS 役割と機能を削除しても問題ありません。 削除するには、それらの役割と機能のチェック ボックスをオフにします。

   AD DS 関連の役割と機能には以下が含まれます

   * Windows PowerShell 機能の Active Directory モジュール
   * AD DS および AD LDS ツールの機能
   * Active Directory 管理センター機能
   * AD DS スナップインとコマンドライン ツール機能
   * DNS サーバー
   * グループ ポリシー管理コンソール

ADDSDeployment と ServerManager Windows PowerShell で同じことを実行するコマンドレットは以下のとおりです

```
Uninstall-addsdomaincontroller
Uninstall-windowsfeature
```

![役割と機能の削除ウィザード-確認ダイアログ](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)

![役割と機能の削除ウィザード-検証](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)

### <a name="credentials"></a>資格情報

![Active Directory Domain Services 構成ウィザード-資格情報の選択](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)

降格オプションは **[資格情報]** ページで構成します。 次の一覧から降格の実行に必要な資格情報を指定します。

* 追加ドメイン コントローラーの降格には、Domain Admin 資格情報が必要です。 [**このドメインコントローラーの削除を強制**する] を選択すると、Active Directory からドメインコントローラーオブジェクトのメタデータが削除されることなく、ドメインコントローラーが降格されます。

   > [!WARNING]
   > ドメイン コントローラーが他のドメイン コントローラーに接続できず、そのネットワークの問題を解決するために*他に有効な方法が*ない場合にのみ、このオプションを選択してください。 強制的に降格を行うと、フォレスト内の他のドメイン コントローラーの Active Directory に孤立したメタデータが残ります。 さらに、そのドメイン コントローラーで複製されていないすべての変更 (パスワードや新しいユーザー アカウントなど) が失われます。 孤立したメタデータは、AD DS、Exchange、SQL、他のソフトウェアに関する Microsoft カスタマー サポートへの問い合わせの根本原因として大きな割合を占めます。
   >
   > ドメイン コントローラーを強制的に降格する場合は、手動でメタデータのクリーンアップをすぐに実行する*必要があります*。 手順については、「 [Clean Up Server Metadata (サーバー メタデータのクリーンアップ)](ad-ds-metadata-cleanup.md)」をご覧ください。

   ![Active Directory Domain Services 構成ウィザード-資格情報の強制削除](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)

* ドメインの最後のドメイン コントローラーを降格する場合は、ドメイン自体が削除されるので (フォレストの最後のドメインの場合は、フォレストも削除されます)、Enterprise Admins グループのメンバーシップが必要です。 現在のドメイン コントローラーがドメインにある最後のドメイン コントローラーである場合は、サーバー マネージャーからそのことが通知されます。 ドメイン コントローラーがドメインの最後のドメイン コントローラーであることを確認するには、**[ドメイン内の最後のドメイン コントローラー]** チェックボックスをオンにします。

ADDSDeployment Windows PowerShell で同じことを実行する引数は以下のとおりです。

```
-credential <pscredential>
-forceremoval <{ $true | false }>
-lastdomaincontrollerindomain <{ $true | false }>
```

### <a name="warnings"></a>警告

![Active Directory Domain Services 構成ウィザード-資格情報 FSMO の役割への影響](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)

[**警告**] ページでは、このドメイン コントローラーを削除することで生じる可能性のある事態についてお知らせします。 続行するには、[**削除の続行**] を選択します。

> [!WARNING]
> [**資格情報**] ページで [**このドメイン コントローラーの削除を強制**] を選択した場合、[**警告**] ページに、このドメイン コントローラーでホストされるすべてのフレキシブル シングル マスター操作役割が表示されます。 このサーバーを降格した後、*すぐに*別のドメイン コントローラーから役割を強制移動*しなければなりません*。 FSMO の役割の強制移動の詳細については、「 [Seize the Operations Master Role (操作マスター役割の強制移動)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816779(v=ws.10))」をご覧ください。

このページと同じことを実行する ADDSDeployment Windows PowerShell 引数はありません。

### <a name="removal-options"></a>削除オプション

![Active Directory Domain Services 構成ウィザード-[資格情報]、[DNS およびアプリケーションパーティションの削除]](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)

[**資格情報**] ページで以前選択した [**ドメイン内の最後のドメイン コントローラー**] に応じて、[**削除オプション**] ページが表示されます。 このページで、追加の削除オプションを構成することができます。 [**ゾーンの最後の DNS サーバーを無視**し、**アプリケーションパーティションを削除**し、 **DNS 委任を削除**する] を選択して [**次へ**] ボタンを有効にします。

このオプションは、このドメイン コントローラーで使用可能な場合のみ表示されます。 たとえば、このサーバーに DNS 委任が設定されていない場合は、このチェック ボックスは表示されません。

[**変更**] をクリックして、別の DNS 管理者資格情報を指定します。 [**パーティションの表示**] をクリックすると、降格中にウィザードが削除する追加のパーティションを見ることができます。 既定では、追加のパーティションはドメイン DNS とフォレスト DNS ゾーンのみです。 ほかのすべてのパーティションは、Windows のパーティションではありません。

ADDSDeployment コマンドレットで同じことを実行する引数は以下のとおりです

```
-ignorelastdnsserverforzone <{ $true | false }>
-removeapplicationpartitions <{ $true | false }>
-removednsdelegation <{ $true | false }>
-dnsdelegationremovalcredential <pscredential>
```

### <a name="new-administrator-password"></a>新しい Administrator パスワード

![Active Directory Domain Services 構成ウィザード-資格情報の新しい管理者パスワード](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)

降格が完了し、コンピューターがドメインメンバーサーバーまたはワークグループコンピューターになると、[**新しい管理者パスワード**] ページでビルトインローカルコンピューターの管理者アカウントのパスワードを入力する必要があります。

**Uninstall-ADDSDomainController** コマンドレットと引数は、特に指定しない限り、サーバー マネージャーと同じ既定値を使用します。

**LocalAdministratorPassword** 引数は特別で、以下のような特徴があります

* 引数として*指定しない*と、コマンドレットで、マスクされたパスワードを入力し、再入力するよう求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。
* *値とともに*指定する場合、値にはセキュリティで保護された文字列を使用してください。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。

たとえば、**読み取りホスト**コマンドレットを使用して、ユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。

```
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)
```

> [!WARNING]
> 前の2つのオプションではパスワードが確認されないため、細心の注意を払ってください。パスワードは表示されません。

セキュリティで保護された文字列は、変換されるクリア テキストの変数として指定することもできますが、これはお勧めしません。 例:

```
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)
```

> [!WARNING]
> クリア テキストのパスワードを指定したり格納したりすることはお勧めしません。 これは、スクリプトでコマンドを実行する人や、その背後で見ている人はだれでも、そのコンピューターのローカル管理者のパスワードを知ることができるためです。 パスワードを知ると、そのデータすべてにアクセスできるため、サーバー自体を偽装することができます。

### <a name="confirmation"></a>確認

![Active Directory Domain Services 構成ウィザード-確認オプション](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)

[**確認**] ページには計画された降格が表示されます。降格の構成オプションはリストされません。 これは、降格の開始前にウィザードが表示する最後のページです。 [スクリプトの表示] ボタンをクリックすると、Windows PowerShell の降格スクリプトが作成されます。

[**降格**] をクリックすると、以下の AD DS 展開コマンドレットが実行されます

```
Uninstall-ADDSDomainController
```

オプションの **Whatif** 引数を **Uninstall-ADDSDomainController** とコマンドレットで使用すると、構成情報を確認することができます。 これによって、コマンドレットの引数の明示的な値と暗黙的な値を確認できます。

例:

![PowerShell Uninstall-addsdomaincontroller の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)

ADDSDeployment Windows PowerShell を使用している場合は、再開のプロンプトが、この操作をキャンセルする最後のチャンスです。 このプロンプトをオーバーライドするには、**-force** または **confirm:$false** 引数を使用します。

### <a name="demotion"></a>降格

![Active Directory Domain Services 構成ウィザード-降格が進行中です](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)

[**降格**] ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます

* %systemroot%\debug\dcpromo.log
* %systemroot%\debug\dcpromoui.log

**Uninstall-addsdomaincontroller**とそれぞれには1つのアクションが含まれているだけなので、ここでは、最低限必要な引数を指定して確認フェーズに**表示します**。 Enter キーを押すと、変更できない降格プロセスが開始され、コンピューターが再起動します。

![PowerShell Uninstall-addsdomaincontroller の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)

![PowerShell Uninstall-Add-windowsfeature の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)

再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の最後でサーバーが自動的に再起動しないようにするには、**-norebootoncompletion:$false** 引数を使用します。

> [!WARNING]
> 再起動のオーバーライドは推奨されません。 メンバー サーバーを正常に機能させるには、再起動する必要があります。

![PowerShell Uninstall-addsdomaincontroller Force の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)

最低限必要な引数である **-forceremoval** と **-demoteoperationmasterrole** を指定して強制的に降格する例です。 ユーザーは Enterprise Admins グループのメンバーとしてログオンしているため、**-credential** 引数は必要ありません。

![PowerShell Uninstall-addsdomaincontroller の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)

以下に、最低限の必須引数 (**-lastdomaincontrollerindomain** と **-removeapplicationpartitions**) を使って、ドメイン内の最後のドメイン コントローラーを削除する例を示します。

![PowerShell Uninstall-addsdomaincontroller-Lastdomainコントローラー Indomain の例](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)

サーバーを降格する前に AD DS の役割を削除しようとすると、Windows PowerShell によって次のエラーがブロックされます。

![AD ドメインサービスの削除中にアンインストールの前提条件のステップが失敗しました。アンインストールを続行できません。 1. Active Directory ドメインサービスの役割をアンインストールする前に、ドメインコントローラーを降格する必要があります。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)

> [!IMPORTANT]
> サーバーを降格した後、AD-Domain-Services 役割のバイナリを削除する前に、コンピューターを再起動する必要があります。

### <a name="results"></a>結果

![AD DS の削除後に警告が表示されないようにしています](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)

[**結果**] ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 ドメイン コントローラーは、10 秒後に自動的に再起動します。
