---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: "降格のドメイン コントローラーとドメイン (レベル 200)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c254a01da5534c1ddc673bc1e60382c166ddeda7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="demoting-domain-controllers-and-domains-level-200"></a>降格のドメイン コントローラーとドメイン (レベル 200)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して、AD DS を削除する方法について説明します。  
  
-   [AD DS 削除のワークフロー](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Workflow)  
  
-   [降格と役割削除の Windows PowerShell](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_PS)  
  
-   [降格](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Demote)  
  
## <a name="BKMK_Workflow"></a>AD DS 削除のワークフロー  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)  
  
> [!CAUTION]  
> ドメイン コント ローラーに昇格はサポートされていませんし、サーバーが正常に起動できなくなります後に Dism.exe または Windows PowerShell の DISM モジュールでの AD DS 役割を削除しています。  
>   
> サーバー マネージャーまたは Windows PowerShell の ADDSDeployment モジュールとは異なり DISM はネイティブのサービス システムなしの AD DS に固有の情報またはその構成があります。 サーバーがドメイン コント ローラーで不要になった場合、AD DS の役割をアンインストールするのに Dism.exe または Windows PowerShell の DISM モジュールを使用することはしません。  
  
## <a name="BKMK_PS"></a>降格と役割削除の Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment と ServerManager コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Uninstall-AddsDomainController|-SkipPreChecks<br /><br />*-LocalAdministratorPassword*<br /><br />-確認します。<br /><br />***資格情報***<br /><br />-DemoteOperationMasterRole<br /><br />*-DNSDelegationRemovalCredential*<br /><br />フォース<br /><br />*-ForceRemoval*<br /><br />*-IgnoreLastDCInDomainMismatch*<br /><br />*-IgnoreLastDNSServerForZone*<br /><br />*-LastDomainControllerInDomain*<br /><br />-Norebootoncompletion<br /><br />*-RemoveApplicationPartitions*<br /><br />*-RemoveDNSDelegation*<br /><br />-RetainDCMetadata|  
|アンインストール-WindowsFeature/Remove-windowsfeature|***名***<br /><br />***-Includemanagementtools***<br /><br />*-再起動します。*<br /><br />-の削除します。<br /><br />フォース<br /><br />-ComputerName<br /><br />資格情報<br /><br />-Logpath<br /><br />Vhd|  
  
> [!NOTE]  
> **-Credential**引数はかどうか、既にログオンしていない (ドメイン内の最後の DC を降格)、Enterprise Admins グループのメンバーとしてに必要なだけと、Domain Admins グループ (レプリカ DC).The **-includemanagementtools**引数は、のみ必要になるすべての AD DS 管理ユーティリ ティーを削除します。  
  
## <a name="BKMK_Demote"></a>降格  
  
### <a name="remove-roles-and-features"></a>役割と機能を削除します。  
サーバー マネージャーには、Active Directory ドメイン サービスの役割を削除する 2 つのインターフェイスが用意されています。  
  
-   **管理**メイン ダッシュ ボード] メニューを使用して**役割の削除と機能**  
  
 ![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)  
  
-   をクリックして**AD DS**または**すべてのサーバー**のナビゲーション ペインでします。 下にスクロールして、**役割と機能の**セクションです。 右クリック**Active Directory Domain Services**で、**役割と機能の**を一覧表示し] をクリックして**を削除する役割または機能**します。 このインターフェイスをスキップ、**サーバーの選択**ページ。  
  
 ![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)  
  
ServerManager コマンドレット**Uninstall-windowsfeature**と**Remove-windowsfeature**をドメイン コントローラーを降格するまでに、AD DS の役割を削除します。  
  
### <a name="server-selection"></a>サーバーの選択  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)  
  
**サーバーの選択**] ダイアログでは、アクセス可能である限り、前に、プールに追加したサーバーのいずれかを選択することができます。 サーバー マネージャーを実行しているローカル サーバーが自動的に利用可能では常にです。  
  
### <a name="server-roles-and-features"></a>サーバーの役割と機能  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)  
  
クリア、**Active Directory Domain Services**をドメイン コントローラーを降格する] チェック ボックスサーバーがドメイン コントローラーでは現在、これは、AD DS の役割を削除しないと代わりに移動、**検証結果**ダイアログに降格を提供します。 それ以外の場合、単に他の役割機能と同様にバイナリが削除されます。  
  
-   すぐにもう一度、ドメイン コントローラーの昇格を行う場合にその他の AD DS 関連の役割または DNS、GPMC、RSAT ツールなどの機能を削除しないでください。 他の役割と機能を削除すると、役割を再インストールするときに、サーバー マネージャーがこれらの機能、再昇格する時間が長くなります。  
  
-   永続的に、ドメイン コントローラーを降格する場合は、不要な AD DS 役割と、独自の判断での機能を削除します。 これは、それらの役割と機能のチェック ボックスをクリアする必要があります。  
  
    AD DS に関連する役割と機能の完全な一覧は次のとおりです。  
  
    -   Active Directory 用 Windows PowerShell モジュールの機能  
  
    -   AD DS および AD LDS ツールの機能  
  
    -   Active Directory 管理センター機能  
  
    -   AD DS スナップインとコマンド ライン ツール機能  
  
    -   DNS サーバー  
  
    -   グループ ポリシー管理コンソール  
  
それと同等の ADDSDeployment と ServerManager Windows PowerShell コマンドレットは次のとおりです。  
  
```  
Uninstall-addsdomaincontroller  
Uninstall-windowsfeature  
  
```  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)  
  
### <a name="credentials"></a>資格情報  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)  
  
降格オプションで構成する、**資格情報**ページ。 次の一覧から降格の実行に必要な資格情報を提供します。  
  
-   追加のドメイン コント ローラーを降格するには、Domain Admin 資格情報が必要です。 選択すると**このドメイン コントローラーの強制的な削除**ドメイン コントローラーは降格されますが、ドメイン コントローラー オブジェクトのメタデータは Active Directory から削除されません。  
  
    > [!WARNING]  
    > ドメイン コント ローラーが他のドメイン コント ローラーに接続できないしがある場合を除き、このオプションを選択しない*妥当な方法はありません*そのネットワークの問題を解決するのには。 強制的に降格では、フォレスト内の残りのドメイン コント ローラーに、Active Directory に孤立したメタデータを残します。 さらに、パスワードや、新しいユーザー アカウントなど、そのドメイン コント ローラーにレプリケートされていないすべての変更が失われます。 孤立したメタデータは、AD DS、Exchange、SQL、およびその他のソフトウェアの Microsoft カスタマー サポートのケースの大きな割合根本原因です。  
    >   
    > 場合は、ドメイン コント ローラーを強制的に降格する*必要があります*メタデータのクリーンアップをすぐに手動で実行します。 For steps, review [Clean Up Server Metadata](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
   ![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)  
  
-   ドメイン内の最後のドメイン コントローラーを降格を必要と Enterprise Admins グループのメンバーシップ、ドメイン自体が削除されます (かどうかは、フォレスト内の最後のドメイン、削除されるので、フォレスト)。 サーバー マネージャーは、現在のドメイン コント ローラーがドメイン内の最後のドメイン コント ローラーの場合に通知されます。 選択、**ドメイン内の最後のドメイン コントローラー**ドメイン コントローラーを確認する] チェック ボックスは、ドメイン内の最後のドメイン コントローラー。  
  
それと同等の ADDSDeployment Windows PowerShell 引数は次のとおりです。  
  
```  
-credential <pscredential>  
-forceremoval <{ $true | false }>  
-lastdomaincontrollerindomain <{ $true | false }>  
  
```  
  
### <a name="warnings"></a>警告  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)  
  
**警告**] ページにはこのドメイン コントローラーを削除した場合の結果が生じる可能性に警告します。 続けるには、選択する必要があります**削除の続行**します。  
  
> [!WARNING]  
> 選択した場合**このドメイン コントローラーの強制的な削除**で、**資格情報**] ページで、**警告**ページはこのドメイン コントローラーによってホストされているすべてのフレキシブル シングル マスター操作役割を示しています。 *必要があります*別のドメイン コントローラーから役割を強制*直ちに*このサーバーを降格した後です。 FSMO 役割の強制移動の詳細については、次を参照してください。[操作マスターの役割を止める](https://technet.microsoft.com/library/cc816779(WS.10).aspx)します。  
  
このページには、それと同等の ADDSDeployment Windows PowerShell 引数はありません。  
  
### <a name="removal-options"></a>削除オプション  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)  
  
**削除オプション**に応じて以前選択したページが表示されます**ドメイン内の最後のドメイン コントローラー**上、**資格情報**ページ。 このページでは、追加の削除のオプションを構成することができます。 選択**ゾーンの最後の DNS サーバーを無視する**、**アプリケーション パーティションの削除**、および**DNS 委任の削除**を公開する、**[次へ]**ボタンをクリックします。  
  
オプションは、このドメイン コントローラーに該当する場合にのみ表示されます。 たとえば、このサーバーの DNS 委任が存在しない場合、そのチェック ボックスは表示されません。  
  
をクリックして**変更**を別の DNS 管理者資格情報を指定します。 をクリックして**パーティションの表示**、降格中に、ウィザードを削除する追加のパーティションを表示します。 既定では、のみ追加のパーティションはドメイン DNS とフォレスト DNS ゾーンを使用します。 その他のすべてのパーティションは、Windows 以外のパーティションです。  
  
それと同等の ADDSDeployment コマンドレット引数は次のとおりです。  
  
```  
-ignorelastdnsserverforzone <{ $true | false }>  
-removeapplicationpartitions <{ $true | false }>  
-removednsdelegation <{ $true | false }>  
-dnsdelegationremovalcredential <pscredential>  
```  
  
### <a name="new-administrator-password"></a>新しい Administrator パスワード  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)  
  
**新しい Administrator パスワード**] ページでは、降格が完了するし、そのコンピューターがドメイン メンバー サーバーまたはワークグループ コンピューター、ビルトイン ローカル コンピューターの管理者アカウントのパスワードを指定する必要があります。  
  
**Uninstall-addsdomaincontroller**コマンドレットと引数に従って、サーバー マネージャーと同じ既定値が指定されていない場合。  
  
**LocalAdministratorPassword**引数は特別な。  
  
-   場合*が指定されていない*を引数として、コマンドレットを求めるメッセージが入力し、マスクされたパスワードを確認します。 これは、コマンドレットを対話的に実行する際の推奨される使用方法です。  
  
-   指定されている場合*値を持つ*、値が、セキュリティで保護された文字列を指定する必要があります。 これには、コマンドレットを対話的に実行しているときに、推奨される使用方法ではありません。  
  
たとえば、手動での入力を求めるパスワードを使用して、**Read-host**コマンドレットをセキュリティで保護された文字列を求めるダイアログ  
  
```  
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> 前の 2 つのオプションは、パスワードを確認していない、細心の注意を使用して、: パスワードは表示されません  
  
これはお勧めはクリア テキストの変換済みの変数として、セキュリティで保護された文字列を提供できます。 例えば：  
  
```  
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
> [!WARNING]  
> 提供するかクリア テキストのパスワードを保存するは推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのコンピューターのローカル管理者のパスワードを認識します。 その知識、すべてのデータへのアクセスを保持しているサーバー自体を偽装することができます。  
  
### <a name="confirmation"></a>確認  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)  
  
**確認**ページは、計画された降格; を示しています。ページには、降格の構成オプションは表示されません。 これは、ウィザードが表示する、降格の開始前に、最後のページです。 スクリプトの表示] ボタンでは、Windows PowerShell の降格スクリプトを作成します。  
  
をクリックして**降格**次の AD DS 展開コマンドレットを実行します。  
  
```  
Uninstall-DomainController  
  
```  
  
オプションを使用して**Whatif**引数を使用、**Uninstall-addsdomaincontroller**と構成情報を確認するコマンドレットです。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示できます。  
  
例えば：  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)  
  
再起動を求めるメッセージは、ADDSDeployment Windows PowerShell を使用する場合は、この操作をキャンセルする、最後の機会です。 そのプロンプトを上書きするには、使用、**-強制**または**ことを確認: $false**引数。  
  
### <a name="demotion"></a>降格  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)  
  
ときに、**降格**ページが表示されます、ドメイン コントローラーの構成を開始、停止またはできません取り消されます。 操作の詳しい内容は、このページに表示され、ログに書き込みます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
**Uninstall-addsdomaincontroller**と**Uninstall-windowsfeature**のみアクションを 1 つずつ、この確認段階で最低限の必須引数では、ここに表示します。 Enter キーを押して、変更できない降格プロセスが開始され、コンピューターが再起動します。  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)  
  
再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion: $false**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めします。 正常に機能する必要があります、メンバー サーバーを再起動します。  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)  
  
最低限の必須引数を強制的に降格する例を次に示します**- forceremoval**と**- demoteoperationmasterrole**します。 **-Credential**引数は必要ありませんので、ユーザーが Enterprise Admins グループのメンバーとしてログオンします。  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)  
  
最低限必要な引数を使用してドメイン内の最後のドメイン コントローラーを削除した場合の例を次に示します**- lastdomaincontrollerindomain**と**- removeapplicationpartitions**:  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)  
  
サーバーを降格する前に、AD DS の役割を削除しようとすると、Windows PowerShell は意図的なエラーでブロックします。  
  
```  
Uninstall-WindowsFeature : An uninstallation prerequisite step failed duringthe removal of AD-Domain-Services, and uninstallation cannot continue.1. The domain controller needs to be demoted before the Active DirectoryDomain Services Role can be uninstalled.  
```  
  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)  
  
> [!IMPORTANT]  
> AD ドメイン-サービスの役割のバイナリを削除する前に、サーバーを降格した後、コンピューターを再起動する必要があります。  
  
### <a name="results"></a>結果  
![DC を降格します。](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  

