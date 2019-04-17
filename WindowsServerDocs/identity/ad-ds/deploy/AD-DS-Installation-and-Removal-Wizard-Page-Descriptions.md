---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: "AD DS のインストールと削除ウィザードのページの説明"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fa023398822e79ca8c3e93d44bb1e87fc9190cee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>AD DS のインストールと削除ウィザードのページの説明

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、AD DS サーバー役割のインストールおよび削除でサーバー マネージャーを構成する以下のウィザード ページ上のコントロールについて説明します。  
  
-   [展開の構成](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)  
  
-   [ドメイン コント ローラー オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)  
  
-   [DNS のオプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)  
  
-   [RODC オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)  
  
-   [その他のオプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)  
  
-   [パス](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)  
  
-   [準備オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)  
  
-   [オプションの確認](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)  
  
-   [前提条件の確認](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)  
  
-   [結果](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)  
  
-   [役割の削除の資格情報](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)  
  
-   [AD DS 削除のオプションと警告](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)  
  
-   [新しい Administrator パスワード](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)  
  
-   [ロール削除選択を確認します。](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)  
  
## <a name="BKMK_DepConfigPage"></a>展開の構成  
サーバー マネージャーは、すべてのドメイン コント ローラーのインストールを開始、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。 たとえば、新しいフォレストを作成する場合、**準備オプション**ページは表示されませんが、既存のフォレストまたはドメインで Windows Server 2012 を実行する最初のドメイン コント ローラーをインストールする場合。  
  
このページで、後でもう一度前提条件の確認の一部として、一部の検証テストが実行されます。 たとえば、Windows 2000 機能レベルがあるフォレスト内の最初の Windows Server 2012 ドメイン コント ローラーをインストールしようとする場合は、このページでエラーが表示されます。  
  
新しいフォレストを作成するときに、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
-   新しいフォレストを作成するときに、フォレスト ルート ドメインの名前を指定する必要があります。 フォレスト ルート ドメイン名が単一ラベルをすることはできません (たとえば、ことがあります"contoso"ではなく"contoso.com")。 許可されている DNS ドメインの命名規則を使用して必要があります。 国際化ドメイン名 (IDN) を指定することができます。 For more information about DNS domain naming conventions, see [KB 909264](https://support.microsoft.com/kb/909264).  
  
-   外部の DNS 名と同じ名前の新しい Active Directory フォレストを作成できません。 たとえば、インターネットの DNS URL が http://contoso.com である場合、内部のフォレストを将来の互換性の問題を避けるために別の名前を選択する必要があります。 その名前は一意で、corp.contoso.com などの web トラフィックの低いする必要があります。  
  
-   新しいフォレストを作成するサーバーの Administrators グループのメンバーがあります。  
  
フォレストを作成する方法の詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory フォレスト (&) #40; をインストールします。。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
新しいドメインを作成するときに、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)  
  
> [!NOTE]  
> 新しいツリー ドメインを作成する場合、親ドメインの代わりに、フォレスト ルート ドメインの名前を指定する必要がありますが、ウィザードの残りのページとオプション同じです。  
  
-   をクリックして**選択**親ドメインまたは Active Directory のツリーを参照するか、有効な親ドメインまたはツリー名を入力します。 新しいドメインの名前を入力し、**新しいドメイン名**します。  
  
-   ツリー ドメイン: 有効な完全修飾ルート ドメイン名; を指定名前は、単一ラベルをすることはできず、DNS ドメイン名の要件を使用する必要があります。  
  
-   子ドメイン: 有効な単一ラベルの子ドメイン名を提供します。名前は、DNS ドメイン名の要件を使用する必要があります。  
  
-   Active Directory ドメイン サービス構成ウィザードは、ドメイン資格情報の場合は、現在の資格情報がドメインからするように求めます。 をクリックして**変更**ドメイン資格情報を提供します。  
  
ドメインを作成する方法の詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory 子またはツリー ドメイン (&) #40; をインストールします。。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
新しいドメイン コント ローラーを既存のドメインに追加するときに、次のオプションが表示されます。  
  
![AD DS のインストール](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)  
  
-   をクリックして**選択**参照ドメインにするか、有効なドメイン名を入力します。  
  
-   サーバー マネージャーの入力を要求有効な資格情報が必要な場合です。 追加のドメイン コント ローラーをインストールするには、Domain Admins グループのメンバーシップが必要です。  
  
    さらに、フォレスト内の Windows Server 2012 を実行している最初のドメイン コント ローラーをインストールするには、両方 Enterprise Admins および Schema Admins グループのグループ メンバーシップを含む資格情報が必要です。 Active Directory ドメイン サービス構成ウィザードが表示されたら後で、現在の資格情報が適切なアクセス許可またはグループのメンバーシップがあるない場合。  
  
既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメイン (&) #40; でインストール。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DCOptionsPage"></a>ドメイン コント ローラー オプション  
新しいフォレストを作成する場合、これらのオプションをドメイン コント ローラー オプション] ページがあります。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)  
  
-   フォレストおよびドメインの機能レベルは、既定では、Windows Server 2012 に設定されます。  
  
    1 つの新機能、Windows Server 2012 ドメイン機能レベル: ダイナミック アクセス制御と Kerberos 防御 KDC 管理用テンプレート ポリシーのサポートが 2 つの設定 ([常に信頼性情報を提供および防御されていない認証要求を失敗) を Windows Server 2012 ドメインの機能レベルを必要とします。 For more information, see "Support for claims, compound authentication and Kerberos armoring" in [What's new in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx).    
    Windows Server 2012 フォレストの機能レベルが任意の新機能を提供していないが、フォレスト内に作成の任意の新しいドメインを Windows Server 2012 のドメイン機能レベルで自動的に動作するようになります。 Windows Server 2012 ドメインの機能レベルを提供しませんいずれかの新しいダイナミック アクセス制御と Kerberos 防御のサポートの横にあるその他の機能が、ドメイン内の任意のドメイン コント ローラーが Windows Server 2012 が実行されているようになります。 別の機能レベルで使用できるその他の機能の詳細については、次を参照してください。[について Active Directory ドメイン サービス (AD DS) の機能レベル](../active-directory-functional-levels.md)します。  
  
    機能レベルは、Windows Server 2012 を実行するドメイン コント ローラーは、以前のバージョンの Windows Server を実行しているドメイン コント ローラーでのみ利用できる追加の機能を提供します。 たとえば、ドメイン コント ローラーを以前のバージョンの Windows Server を実行することはできませんは、Windows Server 2012 を実行するドメイン コント ローラーを仮想ドメイン コント ローラーの複製を使用できます。  
  
-   DNS サーバーは、新しいフォレストを作成するときに、既定で選択されます。 フォレスト内の最初のドメイン コント ローラーは、グローバル カタログ (GC) サーバーである必要があり、読み取り専用ドメイン コント ローラー (RODC) をすることはできません。  
  
-   ディレクトリ サービス復元モード (DSRM) パスワードが AD DS が実行されていないドメイン コント ローラーにログオンするために必要です。 指定したパスワードは既定では、強力なパスワードは必要ありませんが、サーバーに適用されるパスワード ポリシーに従う必要があります。空白でないパスワードのみです。 常に強力で複雑なパスワードまたは可能であれば、パスフレーズを選択します。 For information about how to synchronize the DSRM password with the password of a domain user account, see [KB 961320](https://support.microsoft.com/kb/961320).  
  
フォレストを作成する方法の詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory フォレスト (&) #40; をインストールします。。レベル 200 & #41 です。](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
子ドメインを作成する場合、これらのオプションをドメイン コント ローラー オプション] ページがあります。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)  
  
-   ドメインの機能レベルは、既定で Windows Server 2012 に設定されます。 少なくとも、フォレストの機能レベル以上の値は、その他の値を指定することができます。  
  
-   構成可能なドメイン コント ローラー オプションは**DNS サーバー**と**グローバル カタログ**です。新しいドメインの最初のドメイン コント ローラーとして、読み取り専用ドメイン コント ローラーを構成することはできません。  
  
    マイクロソフトでは、すべてのドメイン コント ローラーが DNS およびグローバル カタログ サービスはそのため、ウィザードは、新しいドメインを作成するときに既定でこれらのオプションを有効分散環境での高可用性を提供することをお勧めします。  
  
-   **ドメイン コント ローラー オプション**] ページでは、適切な Active Directory 論理を選択することもできます**サイト名**、フォレストの構成からです。 既定では、最も適切なサブネットのサイトを選択します。 1 つのサイトがある場合は、そのサイトを自動的に選択します。  
  
    > [!IMPORTANT]  
    > サーバーが Active Directory のサブネットに属していない複数のサイトがある場合は、何も選択し、 **[次へ]**ボタンは、一覧からサイトを選択するまでは利用できません。  
  
ドメインを作成する方法の詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory 子またはツリー ドメイン (&) #40; をインストールします。。レベル 200 & #41 です。](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
ドメインにドメイン コント ローラーを追加する場合、これらのオプションをドメイン コント ローラー オプション] ページがあります。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)  
  
-   構成可能なドメイン コント ローラー オプションは**DNS サーバー**と**グローバル カタログ**、および**読み取り専用ドメイン コント ローラー**します。  
  
    マイクロソフトでは、すべてのドメイン コント ローラーが DNS およびグローバル カタログ サービスはそのため、ウィザードは、既定でこれらのオプションを有効分散環境での高可用性を提供することをお勧めします。 For more information about deploying RODCs, see [Read-Only Domain Controller Planning and Deployment Guide](https://technet.microsoft.com/library/cc771744(v=WS.10).aspx).  
  
既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメイン (&) #40; でインストール。レベル 200 & #41 です。](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DNSOptionsPage"></a>DNS のオプション  
次の DNS サーバーをインストールする場合**DNS オプション**ページが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)  
  
DNS サーバーをインストールするときに、親ドメイン ネーム システム (DNS) ゾーンのゾーンに対する権限を持つ DNS サーバーを指定する委任レコードを作成してください。 委任レコードは、名前解決の権限を転送し、その他の DNS サーバーと、新しいゾーンに対する権限を持つ行われている新しいサーバーをクライアントに適切な紹介を提供します。 これらのリソース レコードを以下に示します。  
  
-   委任を有効にするネーム サーバー (NS) リソース レコードです。 このリソース レコードを使用して、ns1.na.example.microsoft.com という名前のサーバーに委任されたサブドメインに対する権限を持つサーバーがあるアドバタイズします。  
  
-   ホスト (A または AAAA) リソース レコードとも呼ばれるグルー レコード必要がありますをその IP アドレスのネーム サーバー (NS) リソース レコードに指定されているサーバーの名前を解決するのには存在します。 ネーム サーバー (NS) リソース レコード内の委任された DNS サーバーにこのリソース レコード内のホスト名を解決するプロセスとも呼ば「連結追跡」です。  
  
Active Directory ドメイン サービス構成ウィザードは自動的に作成することができます。 ウィザードをクリックした後に、適切なレコードが親 DNS ゾーンに存在することを確認**次**上、**ドメイン コント ローラー オプション**ページ。 ウィザードは、レコードが親ドメインに存在することを確認できません、ウィザードは自動的に提供する新しいドメインの新しい DNS 委任を作成する (または既存の委任を更新) オプションを使用して、新しいドメイン コント ローラーのインストールを続行します。  
  
または、DNS サーバーをインストールする前に、これらの DNS 委任レコードを作成することができます。 ゾーンの委任を作成するには、開く**DNS マネージャー**親ドメインを右クリックし、[クリックして**新しい委任**します。 委任を作成する新しい委任ウィザードの手順に従います。  
  
インストール プロセスは、他のドメイン内のコンピューターがホストについては、DNS サブドメイン内のドメイン コント ローラー、メンバー コンピューターを含む DNS クエリを解決できることを確認する委任の作成を試みます。 Microsoft DNS サーバーでのみ委任レコードを自動的に作成することに注意してください。 バインドなどのサード パーティの DNS サーバーで、親 DNS ドメイン ゾーンが存在する場合は、前提条件チェック] ページで、DNS 委任レコード作成の失敗に関する警告が表示されます。 For more information about the warning, see [Known issues for installing AD DS](https://technet.microsoft.com/library/cc754463(v=WS.10).aspx).  
  
親ドメインと昇格されるサブドメインの間の委任を作成して、インストールの前後に検証します。 作成または、DNS 委任を更新できないために、新しいドメイン コント ローラーのインストールを延期する必要はありません。  
  
For more information about delegation, see [Understanding Zone Delegation](https://go.microsoft.com/fwlink/?LinkId=164773) (https://go.microsoft.com/fwlink/?LinkId=164773). ゾーンの委任が状況に合ったで可能でない場合、ドメイン内のホストに他のドメインの名前解決を提供するその他の方法を検討します。 たとえば、別のドメインの DNS 管理者構成条件付き転送、スタブ ゾーン、またはセカンダリ ゾーンをドメイン内の名前を解決するためにします。 詳細については、次のトピックを参照してください。  
  
-   [Understanding zone types](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)  
  
-   [Understanding stub zones](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)  
  
-   [Understanding forwarders](https://go.microsoft.com/fwlink/?LinkId=164778) (https://go.microsoft.com/fwlink/?LinkId=164778)  
  
## <a name="BKMK_RODCOptionsPage"></a>RODC オプション  
読み取り専用ドメイン コント ローラー (RODC) をインストールするときに、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)  
  
-   代理管理者のアカウントは、RODC に対するローカル管理者のアクセス許可を獲得します。 これらのユーザーは、ローカル コンピューターの Administrators グループと同等の権限で操作できます。 Domain Admins グループまたはドメインのビルトインの Administrators グループのメンバーではありません。 このオプションは、ドメイン管理者のアクセス許可を与えることがなく支社の管理を委任するのに便利です。 管理の委任を構成する必要はありません。 For more information, see [Administrator Role Separation](https://technet.microsoft.com/library/cc753170(v=WS.10).aspx).  
  
-   パスワード レプリケーション ポリシーは、アクセス制御リスト (ACL) として機能します。 これは、RODC がパスワードをキャッシュできるかどうかを決定します。 RODC は認証されたユーザーまたはコンピューター ログオン要求を受け取った後は、アカウントのパスワードをキャッシュする必要があるかどうかを決定するパスワード レプリケーション ポリシーを指します。 同じアカウントはそれ以降のログオンをより効率的に実行し、できます。  
  
    パスワード レプリケーション ポリシー (PRP) には、パスワードができるは、キャッシュされるアカウントとパスワードがキャッシュされてから明示的に拒否アカウントが一覧表示します。 キャッシュが許可されているユーザーおよびコンピューター アカウントの一覧を RODC がそれらのアカウントのパスワードをキャッシュが必ずしも意味しません。 管理者は、事前にすべてのアカウントに RODC がキャッシュされるとなどを指定します。 これにより、RODC はそれらのアカウントを認証できる場合でもへの WAN リンク、ハブ サイト オフラインです。  
  
    ユーザーまたはコンピューターではない (暗黙を含みます) を許可または拒否パスワードはキャッシュされません。 これらのユーザーまたはコンピューターは、書き込み可能なドメイン コント ローラーへのアクセスを持たない場合は、AD DS が提供するリソースや機能にアクセスできません。 For more information about the PRP, see [Password Replication Policy](https://technet.microsoft.com/library/cc730883(v=ws.10).aspx). For more information about managing the PRP, see [Administering the Password Replication Policy](https://technet.microsoft.com/library/rodc-guidance-for-administering-the-password-replication-policy(v=ws.10).aspx).  
  
Rodc のインストールの詳細については、次を参照してください[、Windows Server 2012 Active Directory 読み取り専用ドメイン コント ローラー (&) #40; をインストールする。RODC & #41 です。& #40 です。レベル 200 & #41 です。](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md).  
  
## <a name="BKMK_AdditionalOptionsPage"></a>その他のオプション  
次のオプションが表示されます、**追加オプション**ページの新しいドメインを作成している場合。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)  
  
次のオプションが表示されます、**追加オプション**ページの既存のドメインに追加のドメイン コント ローラーをインストールする場合。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)  
  
-   レプリケーションのソースとしてドメイン コント ローラーを指定するか、ウィザードがレプリケーション ソースとして任意のドメイン コント ローラーを選択できるようにします。  
  
-   できますをドメイン コント ローラーを使用して、インストールするバックアップ メディア (IFM) オプションからインストールを使用してメディアを作成します。 インストール メディアがローカルに保存されている場合、**メディア パスからインストール**オプションでは、ファイルの場所を参照することができます。 [参照] オプションでは、リモート インストールに使用できません。 をクリックすることができます**確認**指定されたパスが有効なメディアであることを確認します。 別既存 Windows Server 2012 のコンピューターからのみ使用できます。 Windows Server バックアップまたは Ntdsutil.exe IFM オプションで使用されるメディアを作成する必要があります。Windows Server 2008 R2 または以前のオペレーティング システムを使用して、Windows Server 2012 ドメイン コント ローラーのメディアを作成することはできません。 メディアが SYSKEY で保護されている場合、サーバー マネージャーは検証中にイメージのパスワードを要求します。  
  
ドメインを作成する方法の詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory 子またはツリー ドメイン (&) #40; をインストールします。。レベル 200 & #41 です。](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md). 既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメイン (&) #40; でインストール。レベル 200 & #41 です。](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_Paths"></a>パス  
次のオプションが表示されます、**パス**ページ。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)  
  
-   **パス**および SYSVOL 共有のページでは、AD DS データベース、データベースのトランザクション ログの既定のフォルダーの場所を上書きすることができます。 既定の場所は常に %systemroot% 内です。  
  
AD DS データベース (NTDS の場所を指定します。DIT)、ファイル、および SYSVOL ログに記録します。 ローカル インストールの場合、ファイルを保存する場所を参照できます。  
  
## <a name="BKMK_AdprepCreds"></a>準備オプション  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)  
  
Adprep.exe コマンドを実行するための十分な資格情報でログオンしていない、adprep が AD DS のインストールを完了するために実行に必要な場合は、adprep.exe を実行する資格情報の入力を求められます。 既存のドメインまたはフォレストに Windows Server 2012 を実行している最初のドメイン コント ローラーを追加するために実行するには、Adprep が必要です。 具体的には。  
  
-   既存のフォレストに Windows Server 2012 を実行している最初のドメイン コント ローラーを追加する Adprep/forestprep を実行する必要があります。 このコマンドは、Enterprise Admins グループ、Schema Admins グループ、およびスキーマ マスターをホストするドメインの Domain Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了する必要があります接続、コマンドを実行するコンピューターとフォレストのスキーマ マスターの間でします。  
  
-   既存のドメインに Windows Server 2012 を実行している最初のドメイン コント ローラーを追加する、Adprep/domainprep を実行する必要があります。 このコマンドは、Windows Server 2012 を実行しているドメイン コント ローラーをインストールするドメインの Domain Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了する必要があります接続コマンドを実行するコンピューターとドメインのインフラストラクチャ マスターします。  
  
-   最初の RODC を既存のフォレストに追加する、Adprep/rodcprep を実行する必要があります。 このコマンドは、Enterprise Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了する必要があります接続コマンドを実行するコンピューターと、フォレスト内の各アプリケーション ディレクトリ パーティションのインフラストラクチャ マスターします。  
  
For more information about Adprep.exe, see [Adprep.exe integration](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) and see [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx).  
  
## <a name="BKMK_ViewInstallOptionsPage"></a>オプションの確認  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)  
  
-   **オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、お客様の要件を満たしていることを確認します。 これは、サーバー マネージャーを使用してインストールを中止する最後の機会ではありません。 単に、このページを使用すると、確認し、構成を続行する前に、設定を確認できます。  
  
-   **オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。 このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。  
  
## <a name="BKMK_PrerqCheckPage"></a>前提条件の確認  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)  
  
このページに表示される警告は次のとおりです。  
  
-   Windows Server 2008 を実行するかをセキュリティで保護されたチャネル セッションを確立するときに弱い暗号アルゴリズムを妨げる「暗号化アルゴリズムを許可する Windows NT 4 との互換性」の既定の設定を後で、ドメイン コント ローラー。 For more information about the potential impact and a workaround, see KB article [942564](https://support.microsoft.com/kb/942564).  
  
-   DNS 委任の作成または更新できませんでした。 詳細については、次を参照してください。 [DNS オプション](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)します。  
  
-   前提条件の確認には、WMI の呼び出しが必要です。 これらは、ブロックされているファイアウォール規則のブロックには、RPC サーバー利用不可のエラーを返す場合に失敗します。  
  
AD DS のインストールで実行される特定の前提条件チェックの詳細については、次を参照してください。[前提条件のテスト](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests)します。  
  
## <a name="BKMK_Results"></a>結果  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)  
  
このページで、インストールの結果を確認することができます。  
  
ウィザードの完了後に、サーバーは常にそのオプションを選択するかどうかに関係なく再起動する場合は、インストールが成功すると、ターゲット サーバーの再起動を選択することもできます。 場合によっては、ウィザードが完了したら、インストールする前に、ドメインに参加していなかった対象サーバーで、ターゲット サーバーのシステム状態を使用すれば、サーバーに到達できません、ネットワーク上またはシステム状態ことができます回避するためするアクセス許可をリモート サーバーを管理する必要がなくなります。  
  
ターゲット サーバーでは、ここでの再起動が失敗した場合、手動で再起動する必要があります。 Shutdown.exe や Windows PowerShell などのツールは再起動できません。 リモート デスクトップ サービスを使用して、ログオンし、ターゲット サーバーをリモートでシャット ダウンすることができます。  
  
## <a name="BKMK_RemovalCredsPage"></a>役割の削除の資格情報  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)  
  
降格オプションで構成する、**資格情報**ページ。 次の一覧から降格の実行に必要な資格情報を提供します。  
  
-   追加のドメイン コント ローラーを降格するには、Domain Admin 資格情報が必要です。 選択すると**ドメイン コント ローラーの削除を強制**ドメイン コント ローラーは降格されますが、ドメイン コント ローラー オブジェクトのメタデータは Active Directory から削除されません。  
  
    > [!IMPORTANT]  
    > ドメイン コント ローラーが他のドメイン コント ローラーに接続できないしがある場合を除き、このオプションを選択しない*妥当な方法はありません*そのネットワークの問題を解決するのには。 強制的に降格では、フォレスト内の残りのドメイン コント ローラーに、Active Directory に孤立したメタデータを残します。 さらに、パスワードや、新しいユーザー アカウントなど、そのドメイン コント ローラーにレプリケートされていないすべての変更が失われます。 孤立したメタデータは、AD DS、Exchange、SQL、およびその他のソフトウェアの Microsoft カスタマー サポートのケースの大きな割合根本原因です。 場合は、ドメイン コント ローラーを強制的に降格する*必要があります*メタデータのクリーンアップをすぐに手動で実行します。 For steps, review [Clean Up Server Metadata](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
-   ドメイン内の最後のドメイン コント ローラーを降格を必要と Enterprise Admins グループのメンバーシップ、ドメイン自体が削除されます (最後のドメイン、フォレストの場合は、この削除フォレスト)。 サーバー マネージャーは、現在のドメイン コント ローラーがドメイン内の最後のドメイン コント ローラーの場合に通知されます。 選択**ドメイン内の最後のドメイン コント ローラー**コント ローラーがドメイン内の最後のドメイン コント ローラーをドメインを確認します。  
  
AD DS の削除の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン (&) #40 です。レベル 200 & #41 です。](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_RemovalOptionsPage"></a>AD DS 削除のオプションと警告  
オプションの確認] ページのヘルプが必要な場合は、オプションの確認を参照してください。  
  
ドメイン コント ローラーが DNS サーバーの役割やグローバル カタログ サーバーなど、追加の役割をホストしている場合は、次の警告ページが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)  
  
をクリックする必要があります**削除の続行**他の役割が不要になった使用できることができます] をクリックする前に確認するために**次**を続行します。  
  
ドメイン コント ローラーの削除を強制する場合、ドメイン内の他のドメイン コント ローラーに複製されていない Active Directory オブジェクトの変更は失われます。 さらに、ドメイン コント ローラーは、操作マスターの役割、グローバル カタログ、または DNS サーバーの役割をホストしている場合、とおりドメインとフォレストの重要な操作が影響可能性があります。 操作マスターの役割をホストしているドメイン コント ローラーを削除する前に、役割を別のドメイン コントローラに転送するお試しください。 役割を転送することはできない場合、は、まず、このコンピューターから Active Directory ドメイン サービスを削除し、役割を強制する Ntdsutil.exe を使用します。 役割を止めるドメイン コント ローラーで Ntdsutil を使用します。可能であれば、そのドメイン コント ローラーと同じサイト内の最近のレプリケーション パートナーを使用します。 For more information about transferring and seizing operations master roles, see [article 255504](https://go.microsoft.com/fwlink/?LinkId=80395) in the Microsoft Knowledge Base. ウィザードには、ドメイン コント ローラーが操作マスターの役割をホストしている場合を判断できない場合、は、このドメイン コント ローラーが操作マスターの役割を実行するかどうかを決定する netdom.exe コマンドを実行します。  
  
-   グローバル カタログ: フォレスト内のドメインにログオン ユーザーがログインで問題を必要があります。 グローバル カタログ サーバーを削除する前に、十分なグローバル カタログ サーバーがそのフォレストおよびサービスのユーザーのログオンをサイトにあることを確認します。 必要に応じて、別のグローバル カタログ サーバーを指定し、新しい情報がクライアントとアプリケーションを更新します。  
  
-   DNS サーバー: すべての Active Directory 統合ゾーンに格納されている DNS データが失われます。 AD DS を削除した後、この DNS サーバーはれていた Active Directory 統合 DNS ゾーンの名前解決を実行できません。 そのため、現在、新しい DNS サーバーの IP アドレスと名前解決のためには、この DNS サーバーの IP アドレスを参照しているすべてのコンピューターの DNS 構成を更新することをお勧めします。  
  
-   インフラストラクチャ マスター: ドメイン内のクライアントは難易度の他のドメイン内のオブジェクトを検索する必要があります。 続行する前に、グローバル カタログ サーバーではないドメイン コント ローラーにインフラストラクチャ マスターの役割を転送します。  
  
-   RID マスター: 新しいユーザー アカウント、コンピューター アカウント、およびセキュリティ グループの作成で問題がある可能性があります。 続行する前に、このドメイン コント ローラーと同じドメイン内のドメイン コント ローラーに RID マスターの役割を転送します。  
  
-   プライマリ ドメイン コント ローラー (PDC) エミュレーター: グループ ポリシーを更新し、非 AD DS アカウントのパスワードのリセットなど、PDC エミュレーターによって実行される操作は正しく機能しません。 続行する前に、このドメイン コント ローラーと同じドメイン内にあるドメイン コント ローラーに PDC エミュレーター マスターの役割を転送します。  
  
-   スキーマ マスター: このフォレストのスキーマを変更できなくなります。 続行する前に、フォレストのルート ドメイン内のドメイン コント ローラーにスキーマ マスターの役割を転送します。  
  
-   ドメイン名前付けマスター: にドメインを追加したり、このフォレストからドメインを削除することはできなきます。 続行する前に、ドメイン名前付けマスタの役割をフォレストのルート ドメイン内のドメイン コント ローラーに転送します。  
  
-   この Active Directory ドメイン コントローラ上のすべてのアプリケーション ディレクトリ パーティションが削除されます。 ドメイン コント ローラーは、削除操作が完了すると、1 つまたは複数のアプリケーション ディレクトリ パーティションの最新のレプリカを保持している場合、それらのパーティションは存在しません。  
  
ドメイン内の最後のドメイン コント ローラーから Active Directory ドメイン サービスをアンインストールした後に、ドメインが存在しないことに注意してください。  
  
ドメイン コント ローラーが DNS ゾーンのホストを委任されている DNS サーバーの場合は、次のページは、DNS サーバーを DNS ゾーンの委任から削除するオプションを提供します。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)  
  
AD DS の削除の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン (&) #40 です。レベル 200 & #41 です。](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_NewAdminPwdPage"></a>新しい Administrator パスワード  
**新しい Administrator パスワード**] ページでは、降格が完了するし、そのコンピューターがドメイン メンバー サーバーまたはワークグループ コンピューター、ビルトイン ローカル コンピューターの管理者アカウントのパスワードを指定する必要があります。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)  
  
AD DS の削除の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン (&) #40 です。レベル 200 & #41 です。](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_ConfirmRoleRemovalPage"></a>オプションの確認  
**オプションの確認**ページは、その他の降格を自動化するため、降格の構成設定を Windows PowerShell スクリプトにエクスポートする機会を提供します。 をクリックして**降格**AD DS を削除します。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)  
  


