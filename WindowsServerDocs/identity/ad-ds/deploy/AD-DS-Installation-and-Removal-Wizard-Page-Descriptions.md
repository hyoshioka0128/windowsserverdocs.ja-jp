---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: AD DS インストール ウィザードおよび削除ウィザードのページの説明
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b4df753a1635a0935e70a76278b097d2f9f70142
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009096"
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>AD DS インストール ウィザードおよび削除ウィザードのページの説明

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーでの AD DS サーバーの役割のインストールと削除を構成する以下のウィザード ページのコントロールについて説明します。  
  
-   [展開の構成](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)  
  
-   [ドメイン コント ローラー オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)  
  
-   [DNS オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)  
  
-   [RODC オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)  
  
-   [Additional Options (追加オプション)](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)  
  
-   [パス](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)  
  
-   [準備オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)  
  
-   [オプションの確認](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)  
  
-   [前提条件の確認](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)  
  
-   [結果](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)  
  
-   [ロールの削除の資格情報](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)  
  
-   [AD DS 削除のオプションと警告](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)  
  
-   [新しい Administrator パスワード](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)  
  
-   [ロールの削除オプションを確認します。](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)  
  
## <a name="BKMK_DepConfigPage"></a>展開の構成  
サーバー マネージャーは、すべてのドメイン コントローラーのインストールを **[配置構成]** ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。 たとえば、新しいフォレストを作成する場合、**準備オプション**ページは表示されませんが、既存のフォレストまたはドメインで Windows Server 2012 を実行する最初のドメイン コント ローラーをインストールする場合します。  
  
一部の検証テストは、このページで実行され、後で前提条件確認の一部として再度実行されます。 たとえばを Windows 2000 の機能レベルを持つフォレスト内の最初の Windows Server 2012 ドメイン コント ローラーをインストールしようとする場合は、このページでエラーが表示されます。  
  
新しいフォレストを作成するときは、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
-   新しいフォレストを作成するときは、フォレストのルート ドメインの名前を指定する必要があります。 単一ラベルであって、フォレスト ルート ドメイン名をすることはできません (たとえば、"contoso"ではなく"contoso.com"は使用あります)。 許可されている DNS ドメイン命名規則を使用する必要があります。 国際化ドメイン名 (IDN) を指定できます。 DNS ドメイン名前付け規則の詳細については、次を参照してください。 [KB 909264](https://support.microsoft.com/kb/909264)します。  
  
-   新しい Active Directory フォレストは、既存の DNS 名と同じ名前で作成しないでください。 たとえば、インターネットの DNS URL が http: \/ /contoso.com、将来の互換性の問題を回避するために、社内フォレストに別の名前を選択する必要があります。 その名前は、一意で、Web トラフィックにはありそうもないものにする必要があります (corp.contoso.com など)。  
  
-   新しいフォレストを作成するサーバーの Administrators グループのメンバーである必要があります。  
  
フォレストを作成する方法の詳細については、次を参照してください。 [、新しい Windows Server 2012 Active Directory フォレストをインストール&#40;レベル 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)します。  
  
新しいドメインを作成するときは、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)  
  
> [!NOTE]  
> 新しいツリー ドメインを作成する場合は、親ドメインの代わりにフォレストのルート ドメインの名前を指定する必要がありますが、それ以外のウィザードのページとオプションは同じです。  
  
-   **[選択]** をクリックして親ドメインまたは Active Directory のツリーを参照するか、有効な親ドメインまたはツリー名を入力します。 次に、 **[新しいドメイン名]** に新しいドメインの名前を入力します。  
  
-   ツリー ドメイン: 有効な完全修飾ルート ドメイン名を指定します。単一ラベルは使用できず、DNS ドメイン名の要件を満たす必要があります。  
  
-   子ドメイン: 有効な単一ラベルの子ドメイン名を指定します。DNS ドメイン名の要件を満たす必要があります。  
  
-   現在の資格情報がドメインのものではない場合、Active Directory Domain Services 構成ウィザードではドメイン資格情報の入力を求められます。 **[変更]** をクリックしてドメインの資格情報を指定します。  
  
ドメインを作成する方法の詳細については、次を参照してください。[新しい Windows Server 2012 Active Directory 子またはツリー ドメインをインストール&#40;レベル 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)します。  
  
既存のドメインに新しいドメイン コントローラーを追加するときは、次のオプションが表示されます。  
  
![AD DS のインストール](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)  
  
-   **[選択]** をクリックしてドメインを参照するか、有効なドメイン名を入力します。  
  
-   必要な場合、サーバー マネージャーでは有効な資格情報の入力を求められます。 ドメイン コントローラーを追加インストールするには、Domain Admins グループのメンバーである必要があります。  
  
    さらに、フォレストで Windows Server 2012 を実行する最初のドメイン コント ローラーをインストールするには、Enterprise Admins および Schema Admins の両方のグループのグループ メンバーシップを含む資格情報が必要です。 現在の資格情報に適切なアクセス許可またはグループ メンバーシップがない場合、Active Directory Domain Services 構成ウィザードでは後で入力を求められます。  
  
既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください。[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメインにインストール&#40;レベル 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)します。  
  
## <a name="BKMK_DCOptionsPage"></a>ドメイン コント ローラー オプション  
新しいフォレストを作成している場合、[ドメイン コントローラー オプション] ページには次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)  
  
-   フォレストおよびドメインの機能レベルは、既定では、Windows Server 2012 に設定されます。  
  
    1 つで新しい機能が使用可能な Windows Server 2012 ドメインの機能レベル: ダイナミック アクセス制御と Kerberos 防御 KDC 管理用テンプレート ポリシーのサポートが 2 つの設定 (常に信頼性情報および提供防御されていない認証に失敗しました。要求) を Windows Server 2012 ドメインの機能レベルを必要とします。 詳細については、「信頼性情報、複合認証および Kerberos 防御のサポート」を参照してください[Kerberos 認証の新](https://technet.microsoft.com/library/hh831747.aspx)します。    
    Windows Server 2012 フォレストの機能レベルは、新機能を提供しませんが、フォレスト内に作成、新しいドメインを Windows Server 2012 のドメイン機能レベルで自動的に動作するようになります。 Windows Server 2012 ドメインの機能レベルはない新ダイナミック アクセス制御と Kerberos 防御のサポートの横にあるその他の機能が、ドメイン内の任意のドメイン コント ローラーが Windows Server 2012 を実行するようになります。 別の機能レベルで使用できる他の機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。  
  
    機能のレベルは、Windows Server 2012 を実行するドメイン コント ローラーは、Windows Server の以前のバージョンを実行するドメイン コント ローラーでは使用できない追加機能を提供します。 たとえば、以前のバージョンの Windows Server を実行するドメイン コント ローラーのことはできませんに Windows Server 2012 を実行するドメイン コント ローラーの仮想ドメイン コント ローラーの複製に使用できます。  
  
-   新しいフォレストを作成するときは、DNS サーバーが既定で選択されます。 フォレストの最初のドメイン コントローラーはグローバル カタログ (GC) サーバーである必要があり、読み取り専用のドメイン コントローラー (RODC) にはできません。  
  
-   AD DS が実行されていないドメイン コントローラーにログオンするには、ディレクトリ サービス復元モード (DSRM) のパスワードが必要です。 指定するパスワードはサーバーに適用されるパスワード ポリシーに準拠する必要がありますが、既定では強力なパスワードである必要はなく、空白パスワードではないことだけが必要です。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。 ドメイン ユーザー アカウントのパスワードと DSRM パスワードを同期する方法については、次を参照してください。 [KB 961320](https://support.microsoft.com/kb/961320)します。  
  
フォレストを作成する方法の詳細については、次を参照してください。 [、新しい Windows Server 2012 Active Directory フォレストをインストール&#40;レベル 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)します。  
  
子ドメインを作成している場合、[ドメイン コントローラー オプション] ページには次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)  
  
-   ドメインの機能レベルは、既定で Windows Server 2012 に設定されます。 フォレスト機能レベル以上の他の任意の値を指定できます。  
  
-   構成可能なドメイン コントローラー オプションは **[DNS サーバー]** と **[グローバル カタログ]** であり、読み取り専用ドメイン コントローラーを新しいドメインの最初のドメイン コントローラーとして構成することはできません。  
  
    分散環境での高可用性のため、すべてのドメイン コントローラーで DNS サービスとグローバル カタログ サービスを提供することをお勧めします。新しいドメインを作成するときにウィザードにおいてこれらのオプションが既定で有効になるのはそのためです。  
  
-   **[ドメイン コントローラー オプション]** ページでは、フォレストの構成から適切な Active Directory 論理**サイト名**を選択することもできます。 既定では、最も適切なサブネットのサイトが選択されます。 サイトが 1 つだけの場合は、そのサイトが自動的に選択されます。  
  
    > [!IMPORTANT]  
    > 何も選択して、サーバーが Active Directory サブネットに属していないサイトが 1 つ以上の場合は、および**次**ボタンは、一覧からサイトを選択するまでは使用できません。  
  
ドメインを作成する方法の詳細については、次を参照してください。[新しい Windows Server 2012 Active Directory 子またはツリー ドメインをインストール&#40;レベル 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)します。  
  
ドメインにドメイン コントローラーを追加する場合は、[ドメイン コントローラー オプション] ページに次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)  
  
-   構成可能なドメイン コントローラー オプションは、 **[DNS サーバー]** 、 **[グローバル カタログ]** 、 **[読み取り専用ドメイン コントローラー]** です。  
  
    分散環境での高可用性のため、すべてのドメイン コントローラーで DNS サービスとグローバル カタログ サービスを提供することをお勧めします。ウィザードにおいてこれらのオプションが既定で有効になるのはそのためです。 Rodc の展開の詳細については、次を参照してください。[読み取り専用ドメイン コント ローラーの計画と展開ガイド](https://technet.microsoft.com/library/cc771744(v=WS.10).aspx)します。  
  
既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください。[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメインにインストール&#40;レベル 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)します。  
  
## <a name="BKMK_DNSOptionsPage"></a>DNS オプション  
DNS サーバーをインストールする場合は、 **[DNS オプション]** ページが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)  
  
DNS サーバーをインストールするときは、ゾーンに対する権限を持つドメイン ネーム システム (DNS) サーバーを示す委任レコードを、親の DNS ゾーンに作成する必要があります。 委任レコードによって、名前解決の権限が転送され、新しいゾーンに対する権限の付与先となる新しいサーバーのクライアントと他の DNS サーバーへの適切な紹介が提供されます。 これらのリソース レコードは次のとおりです。  
  
-   委任を実現するネーム サーバー (NS) リソース レコード。 このリソース レコードを使用して、ns1.na.example.microsoft.com という名前のサーバーが、委任されたサブドメインに対する権限を持つサーバーであることをアドバタイズします。  
  
-   ホスト (A または AAAA) リソース レコードとも呼ばれますグルー レコード必要があります、IP アドレスをネーム サーバー (NS) リソース レコードで指定されているサーバーの名前を解決するのには存在します。 このリソース レコード内のホスト名をネーム サーバー (NS) リソース レコード内の委任された DNS サーバーに解決するプロセスは、"連結追跡" とも呼ばれます。  
  
これらは Active Directory Domain Services 構成ウィザードで自動的に作成できます。 ウィザードでは、 **[ドメイン コントローラー オプション]** ページで **[次へ]** をクリックした後に、該当するレコードが親の DNS ゾーンに存在するかどうかが確認されます。 レコードが親ドメインに存在することが確認できなかった場合は、ウィザードの自動的に新しいドメインの新しい DNS 委任を作成する (または既存の委任を更新する) オプションを使用して、新しいドメイン コントローラーのインストールを続行できます。  
  
または、DNS サーバーをインストールする前にこれらの DNS 委任レコードを作成することもできます。 ゾーンの委任を作成するには、**DNS マネージャー**を開き、親ドメインを右クリックして、 **[新しい委任]** をクリックします。 新しい委任ウィザードの手順に従って、委任を作成します。  
  
インストール プロセスは、他のドメイン内のコンピューターがホスト (DNS サブドメイン内のドメイン コントローラー、メンバー コンピューターなど) の DNS クエリを解決できるようにする委任の作成を試行します。 委任レコードを自動的に作成できるのは Microsoft DNS サーバーだけであることに注意してください。 親 DNS ドメイン ゾーンが BIND などのサード パーティの DNS サーバーにある場合は、DNS 委任レコード作成の失敗に関する警告が [前提条件のチェック] ページに表示されます。 警告の詳細については、次を参照してください。 [AD DS のインストールの既知の問題](https://technet.microsoft.com/library/cc754463(v=WS.10).aspx)します。  
  
親ドメインと昇格されるサブドメインの間の委任は、インストールの前または後に作成して検証できます。 DNS 委任を作成または更新することはできないので、新しいドメイン コントローラーのインストールを遅延する必要はありません。  
  
委任の詳細については、次を参照してください。 [Understanding Zone Delegation](https://go.microsoft.com/fwlink/?LinkId=164773) (https://go.microsoft.com/fwlink/?LinkId=164773)します。 ご使用の状況で委任が不可能な場合は、他のドメインから現在のドメイン内のホストへの名前解決を指定する別の方法を検討してください。 たとえば、別のドメインの DNS 管理者は、現在のドメイン内の名前を解決するために、条件付き転送、スタブ ゾーン、またはセカンダリ ゾーンを構成できます。 詳しくは、次のトピックをご覧ください。  
  
-   [ゾーンの種類について](https://go.microsoft.com/fwlink/?LinkID=157399)(https://go.microsoft.com/fwlink/?LinkID=157399)  
  
-   [スタブ ゾーンを理解する](https://go.microsoft.com/fwlink/?LinkId=164776)(https://go.microsoft.com/fwlink/?LinkId=164776)  
  
-   [フォワーダーと](https://go.microsoft.com/fwlink/?LinkId=164778)(https://go.microsoft.com/fwlink/?LinkId=164778)  
  
## <a name="BKMK_RODCOptionsPage"></a>RODC オプション  
読み取り専用ドメイン コントローラー (RODC) をインストールするときは、次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)  
  
-   委任される管理者アカウントには、RODC に対するローカル管理アクセス許可が与えられます。 これらのユーザーは、ローカル コンピューターの Administrators グループと同じ特権で操作できます。 これらのユーザーは、Domain Admins グループまたはドメインの組み込みの Administrator グループのメンバーではありません。 このオプションは、ドメインの管理アクセス許可を与えることなく支社の管理を委任する場合に便利です。 管理の委任の構成は必要ありません。 詳細については、次を参照してください。[管理者の役割の分離](https://technet.microsoft.com/library/cc753170(v=WS.10).aspx)します。  
  
-   パスワード レプリケーション ポリシーはアクセス制御リスト (ACL) として機能します。 パスワード レプリケーション ポリシーによって、RODC がパスワードをキャッシュできるかどうかが決まります。 RODC は、認証済みのユーザーまたはコンピューターのログオン要求を受け取った後、パスワード レプリケーション ポリシーを参照して、アカウントのパスワードをキャッシュする必要があるかどうかを判別します。 同じアカウントによる以降のログオンをいっそう効率よく実行できます。  
  
    パスワード レプリケーション ポリシー (PRP) には、パスワードをキャッシュできるアカウント、およびパスワードのキャッシュを明示的に拒否されているアカウントが列記されています。 キャッシュできるアカウントのリストにユーザーおよびコンピューターが含まれていたとしても、RODC がそのアカウントのパスワードを実際にキャッシュしているとは限りません。 たとえば、管理者は事前に RODC がキャッシュするアカウントを指定できます。 これにより、RODC はハブ サイトへの WAN リンクがオフラインであっても、それらのアカウントを認証できます。  
  
    許可されていない (暗黙を含みます)、または拒否されているユーザーまたはコンピューターのパスワードはキャッシュされません。 このようなユーザーまたはコンピューターは、書き込み可能なドメイン コントローラーにアクセスできない場合、AD DS が提供するリソースまたは機能にアクセスできません。 PRP の詳細については、次を参照してください。[パスワード レプリケーション ポリシー](https://technet.microsoft.com/library/cc730883(v=ws.10).aspx)します。 PRP の管理の詳細については、次を参照してください。[パスワード レプリケーション ポリシーを管理する](https://technet.microsoft.com/library/rodc-guidance-for-administering-the-password-replication-policy(v=ws.10).aspx)します。  
  
Rodc のインストールの詳細については、次を参照してください。 [、Windows Server 2012 Active Directory 読み取り専用ドメイン コント ローラーをインストール&#40;RODC&#41; &#40;レベル 200&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)します。  
  
## <a name="BKMK_AdditionalOptionsPage"></a>追加のオプション  
新しいドメインを作成している場合、 **[追加オプション]** ページには次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)  
  
既存のドメインに追加のドメイン コントローラーをインストールしている場合、 **[追加オプション]** ページには次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)  
  
-   レプリケーション ソースとしてのドメイン コントローラーを自分で指定することも、ウィザードに任意のドメイン コントローラーをレプリケーション ソースとして選択させることもできます。  
  
-   また、メディアからのインストール (IFM) オプションを使用して、バックアップされているメディアからドメイン コントローラーをインストールすることもできます。 インストール メディアがローカルに格納されている場合は、 **[メディアからのインストール パス]** オプションを使用してファイルの場所を指定できます。 リモート インストールの場合、参照オプションは使用できません。 **[確認]** をクリックして、指定したパスが有効なメディアであることを確認できます。 もう 1 つ既存 Windows Server 2012 のコンピューターからのみで、Windows Server バックアップまたは Ntdsutil.exe IFM オプションで使用するメディアを作成する必要があります。Windows Server 2008 R2 または以前のオペレーティング システムを使用して、Windows Server 2012 ドメイン コント ローラーのメディアを作成することはできません。 メディアが SYSKEY で保護されている場合、サーバー マネージャーは確認の間にイメージのパスワードの入力を求めます。  
  
ドメインを作成する方法の詳細については、次を参照してください。[新しい Windows Server 2012 Active Directory 子またはツリー ドメインをインストール&#40;レベル 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)します。 既存のドメインにドメイン コント ローラーを追加する方法の詳細については、次を参照してください。[レプリカ Windows Server 2012 ドメイン コント ローラーを既存のドメインにインストール&#40;レベル 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)します。  
  
## <a name="BKMK_Paths"></a>パス  
**[パス]** ページには次のオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)  
  
-   **[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所を上書きできます。 既定の場所は常に %systemroot% 内です。  
  
AD DS データベース (NTDS.DIT)、ログ ファイル、SYSVOL の場所を指定します。 ローカル インストールの場合は、ファイルを保存する場所を指定できます。  
  
## <a name="BKMK_AdprepCreds"></a>準備オプション  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)  
  
現在のログオンで使用している資格情報が adprep.exe コマンドを実行するには十分ではなく、AD DS のインストールを完了するために adprep を実行する必要がある場合は、adprep.exe を実行するための資格情報の入力を求められます。 Adprep は、既存のドメインまたはフォレストに Windows Server 2012 を実行する最初のドメイン コント ローラーを追加するために実行する必要があります。 具体的な機能は次のとおりです。  
  
-   既存のフォレストに Windows Server 2012 を実行する最初のドメイン コント ローラーを追加するのには、Adprep/forestprep を実行する必要があります。 このコマンドは、Enterprise Admins グループ、Schema Admins グループ、およびスキーマ マスターをホストするドメインの Domain Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了するには、コマンドを実行するコンピューターとフォレストのスキーマ マスターが接続されている必要があります。  
  
-   既存のドメインに Windows Server 2012 を実行する最初のドメイン コント ローラーを追加するのには、Adprep/domainprep を実行する必要があります。 このコマンドは、Windows Server 2012 を実行するドメイン コント ローラーをインストールするドメインの Domain Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了するには、コマンドを実行するコンピューターとドメインのインフラストラクチャ マスターが接続されている必要があります。  
  
-   最初の RODC を既存のフォレストに追加するには、adprep /rodcprep を実行する必要があります。 このコマンドは、Enterprise Admins グループのメンバーが実行する必要があります。 このコマンドが正常に完了するには、コマンドを実行するコンピューターと、フォレスト内の各アプリケーション ディレクトリ パーティションのインフラストラクチャ マスターが接続されている必要があります。  
  
Adprep.exe の詳細については、次を参照してください。 [Adprep.exe の統合](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep)して[Adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx)します。  
  
## <a name="BKMK_ViewInstallOptionsPage"></a>オプションの確認  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)  
  
-   **[オプションの確認]** ページでは、インストールを開始する前に、設定を検証し、設定が要件を満たしていることを確認できます。 これがサーバー マネージャーを使用するインストールを停止する最後の機会ではありません。 このページでは、構成を続行する前に設定を検討して確認することだけができます。  
  
-   サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。 これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。  
  
## <a name="BKMK_PrerqCheckPage"></a>前提条件の確認  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)  
  
このページでは次のような警告が表示されます。  
  
-   セキュリティで保護されたチャネル セッションを確立するときに弱い暗号アルゴリズムを防止する暗号化アルゴリズムを許可する Windows NT 4 と互換性のある"の既定の設定を後である Windows Server 2008 を実行するドメイン コント ローラー。 可能性のある影響とサポート技術情報の記事を参照してください、回避策の詳細については[942564](https://support.microsoft.com/kb/942564)します。  
  
-   DNS 委任を作成または更新できませんでした。 詳細については、「[DNS のオプション](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)」を参照してください。  
  
-   前提条件の確認には WMI の呼び出しが必要です。 呼び出しがファイアウォール ルールでブロックされている場合は、呼び出しが失敗し、RPC サーバーを使用できないというエラーが表示される可能性があります。  
  
AD DS のインストールで実行される具体的な前提条件の確認の詳細については、「[前提条件のテスト](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests)」を参照してください。  
  
## <a name="BKMK_Results"></a>結果  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)  
  
このページでは、インストールの結果を確認できます。  
  
また、ウィザードが完了した後で対象のサーバーを再起動することもできますが、インストールが成功した場合は、このオプションを選択するかどうかにかかわらずサーバーは常に再起動されます。 場合によっては、インストール前にはドメインに参加していなかった対象サーバーでウィザードが完了した後、対象サーバーのシステム状態により、ネットワーク上でサーバーに到達できないことや、リモート サーバーを管理するためのアクセス許可がユーザーに与えられないことがあります。  
  
このような状態で対象サーバーの再起動が失敗した場合は、手動で再起動する必要があります。 shutdown.exe や Windows PowerShell などのツールでは再起動できません。 リモート デスクトップ サービスを使用して対象サーバーにログオンし、リモートでシャットダウンできます。  
  
## <a name="BKMK_RemovalCredsPage"></a>ロールの削除の資格情報  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)  
  
降格オプションは **[資格情報]** ページで構成します。 次の一覧から降格の実行に必要な資格情報を指定します。  
  
-   追加ドメイン コントローラーの降格には、Domain Admin 資格情報が必要です。 選択**ドメイン コント ローラーを強制的に削除**と Active Directory からドメイン コント ローラー オブジェクトのメタデータを削除せず、ドメイン コント ローラーは降格されます。  
  
    > [!IMPORTANT]  
    > ドメイン コントローラーが他のドメイン コントローラーに接続できず、そのネットワークの問題を解決するために*他に有効な方法が*ない場合にのみ、このオプションを選択してください。 強制的に降格を行うと、フォレスト内の他のドメイン コントローラーの Active Directory に孤立したメタデータが残ります。 さらに、そのドメイン コントローラーで複製されていないすべての変更 (パスワードや新しいユーザー アカウントなど) が失われます。 孤立したメタデータは、AD DS、Exchange、SQL、他のソフトウェアに関する Microsoft カスタマー サポートへの問い合わせの根本原因として大きな割合を占めます。 ドメイン コントローラーを強制的に降格する場合は、手動でメタデータのクリーンアップをすぐに実行する *必要があります* 。 手順については、「 [Clean Up Server Metadata (サーバー メタデータのクリーンアップ)](https://technet.microsoft.com/library/cc816907(WS.10).aspx)」をご覧ください。  
  
-   ドメインの最後のドメイン コントローラーを降格する場合は、ドメイン自体が削除されるので (フォレストの最後のドメインの場合は、フォレストも削除されます)、Enterprise Admins グループのメンバーシップが必要です。 現在のドメイン コントローラーがドメインにある最後のドメイン コントローラーである場合は、サーバー マネージャーからそのことが通知されます。 ドメイン コントローラーがドメインの最後のドメイン コントローラーであることを確認するには、 **[ドメイン内の最後のドメイン コントローラー]** を選択します。  
  
AD DS を削除する方法の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン&#40;レベル 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)します。  
  
## <a name="BKMK_RemovalOptionsPage"></a>AD DS 削除のオプションと警告  
[オプションの確認] ページに関するヘルプが必要な場合は、「オプションの確認」を参照してください。  
  
ドメイン コントローラーが DNS サーバーの役割やグローバル カタログ サーバーなどの他の役割をホストしている場合、次の警告ページが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)  
  
**[削除の続行]** をクリックして他の役割が使用できなくなることを確認してから、 **[次へ]** をクリックして続行する必要があります。  
  
ドメイン コントローラーを強制的に削除すると、ドメイン内の他のドメイン コントローラーに複製されていない Active Directory オブジェクトの変更は失われます。 さらに、ドメイン コントローラーが操作マスターの役割、グローバル カタログ、または DNS サーバーの役割をホストしている場合、ドメインおよびフォレストの重要な操作が次のような影響を受ける場合があります。 操作マスターの役割をホストしているドメイン コントローラーを削除する前に、役割を別のドメイン コントローラーに転送してください。 役割を転送できない場合は、最初にそのコンピューターから Active Directory Domain Services を削除した後、Ntdsutil.exe を使用して役割を止めてください。 役割を止めるドメイン コントローラーで Ntdsutil を使用します。可能な場合は、そのドメイン コントローラーと同じサイトで最近のレプリケーション パートナーを使用します。 転送して、操作マスターの役割を強制する場合の詳細については、次を参照してください。[記事 255504](https://go.microsoft.com/fwlink/?LinkId=80395)マイクロソフト サポート技術情報でします。 ドメイン コントローラーが操作マスターの役割をホストしているかどうかをウィザードが特定できない場合は、netdom.exe コマンドを実行して、そのドメイン コントローラーが操作マスターの役割を実行しているかどうかを判別します。  
  
-   グローバル カタログ:ユーザーは、フォレスト内のドメインにログインで問題があります。 グローバル カタログ サーバーを削除する前に、ユーザーのログオンに対応するのに十分なグローバル カタログ サーバーがそのフォレストおよびサイトにあることを確認してください。 必要に応じて、別のグローバル カタログ サーバーを委任し、新しい情報でクライアントとアプリケーションを更新します。  
  
-   DNS サーバー:すべての Active Directory 統合ゾーンに格納されている DNS データは失われます。 AD DS を削除すると、その DNS サーバーは Active Directory に統合されていた DNS ゾーンの名前解決を実行できなくなります。 したがって、現在名前解決のためにその DNS サーバーの IP アドレスを参照しているすべてのコンピューターの DNS 構成を、新しい DNS サーバーの IP アドレスで更新することをお勧めします。  
  
-   インフラストラクチャ マスター: ドメイン内のクライアントによる他のドメインのオブジェクトの発見が困難になる場合があります。 続行する前に、グローバル カタログ サーバーではないドメイン コントローラーにインフラストラクチャ マスターの役割を転送してください。  
  
-   RID マスター: 新しいユーザー アカウント、コンピューター アカウント、およびセキュリティ グループの作成で問題が発生する可能性があります。 続行する前に、そのドメイン コントローラーと同じドメイン内の別のドメイン コントローラーに RID マスターの役割を転送してください。  
  
-   プライマリ ドメイン コントローラー (PDC) エミュレーター: PDC エミュレーターによって実行されている操作 (AD DS 以外のアカウントのグループ ポリシーの更新やパスワードのリセットなど) が、正常に機能しなくなります。 続行する前に、そのドメイン コントローラーと同じドメイン内の別のドメイン コントローラーに PDC エミュレーター マスターの役割を転送してください。  
  
-   スキーマ マスター: そのフォレストのスキーマを変更できなくなります。 続行する前に、フォレストのルート ドメイン内の別のドメイン コントローラーにスキーマ マスターの役割を転送してください。  
  
-   ドメイン名前付けマスター: そのフォレストへのドメインの追加およびフォレストからのドメインの削除を行うことができなくなります。 続行する前に、フォレストのルート ドメイン内の別のドメイン コントローラーにドメイン名前付けマスターの役割を転送してください。  
  
-   その Active Directory ドメイン コントローラーのすべてのアプリケーション ディレクトリ パーティションは削除されます。 ドメイン コントローラーが 1 つ以上のアプリケーション ディレクトリ パーティションの最新のレプリカを保持している場合、削除操作が完了すると、それらのパーティションは存在しなくなります。  
  
ドメイン内の最後のドメイン コントローラーから Active Directory Domain Services をアンインストールすると、ドメインが存在しなくなることに注意してください。  
  
ドメイン コントローラーが DNS ゾーンをホストするために委任された DNS サーバーである場合、次のページで DNS サーバーを DNS ゾーンの委任から削除するオプションが表示されます。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)  
  
AD DS を削除する方法の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン&#40;レベル 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)します。  
  
## <a name="BKMK_NewAdminPwdPage"></a>新しい Administrator パスワード  
**新しい Administrator パスワード** ページでは、降格が完了するし、コンピューターがドメイン メンバー サーバーまたはワークグループ コンピューターは、ビルトイン ローカル コンピューターの管理者アカウントのパスワードを指定する必要があります。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)  
  
AD DS を削除する方法の詳細については、次を参照してください。 [Active Directory Domain Services の削除 (レベル 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c)と[を降格するドメイン コント ローラーとドメイン&#40;レベル 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)します。  
  
## <a name="BKMK_ConfirmRoleRemovalPage"></a>オプションの確認  
**[オプションの確認]** ページでは、他の降格を自動的に実行できるように、降格の構成設定を Windows PowerShell スクリプトにエクスポートできます。 AD DS を削除するには **[降格]** をクリックします。  
  
![AD DS のインストール](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)  
  


