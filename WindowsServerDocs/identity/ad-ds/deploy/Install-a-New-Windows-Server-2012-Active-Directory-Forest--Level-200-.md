---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: "フォレストをインストールする新しい Windows Server 2012 Active Directory (レベル 200)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b8a7502a1b9d27b0f61353f2544182a64d311496
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>フォレストをインストールする新しい Windows Server 2012 Active Directory (レベル 200)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックは、基本的なレベルで新しい Windows Server 2012 Active Directory ドメイン サービス ドメイン コントローラーの昇格機能について説明します。 Windows Server 2012 の AD DS が置き換えられます Dcpromo ツール、サーバー マネージャーと Windows PowerShell ベースの展開システムです。  
  
-   [Active Directory ドメイン サービスの簡略化された管理](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [技術概要](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [サーバー マネージャーでフォレストを展開します。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Windows PowerShell を使用したフォレストを展開します。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Active Directory ドメイン サービスの簡略化された管理  
Windows Server 2012 では、Active Directory ドメイン サービス簡略化された管理の次世代を紹介しは、最も革新ドメイン構想の見直し Windows 2000 Server 以来します。 AD DS の簡略化された管理受け取り Active Directory の 12 年から得られた教訓よりサポート可能なより柔軟なより直感的な管理エクスペリエンスの設計者および管理者します。 Windows Server 2008 R2 でリリースされたコンポーネントの機能を拡張すると、既存のテクノロジの新しいバージョンを作成するようになります。  
  
### <a name="what-is-ad-ds-simplified-administration"></a>簡略化された管理を AD DS は何ですか。  
AD DS の簡略化された管理は、ドメインの展開の再イメージ化、です。 これらの機能は次のとおりです。  
  
-   AD DS の役割の展開は、新しいサーバー マネージャー アーキテクチャの一部になりでき、リモート インストールできます。  
  
-   AD DS の展開と構成のエンジンは、グラフィカルなセットアップを使用する場合でも、Windows PowerShell ではようになりましたです。  
  
-   昇格ようになりましたにははフォレストおよびドメインの準備、新しいドメイン コント ローラー、障害が発生したプロモーションの機会を削減を検証する前提条件のチェックが含まれます。  
  
-   Windows Server 2012 フォレスト レベルでは新しい機能が実装されていませんし、ドメインの機能レベルは、頻繁の管理者の軽減、Kerberos の新機能のサブセットにのみ必要な機能は、同種のドメイン コント ローラー環境の必要があります。  
  
### <a name="purpose-and-benefits"></a>目的と利点  
これらの変更より複雑な簡単になる場合があります。 ただし、AD DS 展開プロセスを再設計するで少数の簡単操作に多くの手順とベスト プラクティスを結合する機会が発生しました。 たとえば、以前は 12 ではなく 8 個のダイアログを新しいレプリカ ドメイン コント ローラーのグラフィカルな構成ができるようになりましたがあることを意味します。 新しい Active Directory フォレストを作成する必要があります、*単一*のみでの Windows PowerShell コマンド*1 つ*引数: ドメインの名前。  
  
このようなに重点を置いた Windows Server 2012 での Windows PowerShell はなぜですか。 分散コンピューティングが進化する、Windows PowerShell の構成とグラフィックの両方のメンテナンスとコマンド ライン インターフェイスの単一のエンジンことができます。 API が開発者に付与する IT プロフェッショナル向けのすべてのコンポーネントのと同じ最初のクラスの公的完全に機能を備えたスクリプトが許可されます。 としてクラウド ベースのコンピューティングのユビキタス化と、Windows PowerShell もいよいよ機能を備えるようありませんグラフィカル インターフェイスを搭載したコンピューターが、モニターやマウスで 1 つとして、同じ管理機能を持つサーバーをリモートで管理します。  
  
ベテラン AD DS 管理者、以前の知識を大いに活かせる検索する必要があります。 先頭の管理者では、経験の浅い習得を検索します。  
  
## <a name="BKMK_TechOverview"></a>技術概要  
  
### <a name="what-you-should-know-before-you-begin"></a>新機能を開始する前に知っておくべき  
このトピックでは、Active Directory ドメイン サービスでは、以前のリリースに関する知識を前提としていて、その目的と機能といった基本事項については提供しません。 AD DS の詳細については、下記のリンクを TechNet ポータルのページを参照してください。  
  
-   [Windows Server 2008 R2 用 active Directory ドメイン サービス](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Windows Server 2008 の active Directory ドメイン サービス](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Windows Server テクニカル リファレンス](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>機能の説明  
  
#### <a name="ad-ds-role-installation"></a>AD DS の役割のインストール  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Active Directory ドメイン サービスのインストールは、その他のすべてのサーバーの役割と Windows Server 2012 の機能と同様に、サーバー マネージャーおよび Windows PowerShell でを使用します。 Dcpromo.exe プログラムには、GUI 構成オプションが提供は行われません。  
  
ローカルおよびリモートの両方のインストール環境では、Windows PowerShell の ServerManager モジュールまたはサーバー マネージャーのグラフィカルなウィザードを使用します。 ようなウィザードやコマンドレットの複数のインスタンスを実行するいると、さまざまなサーバーを対象とする、ことができますを展開する AD DS を複数のドメイン コント ローラーに同時に、1 つのコンソールからすべてします。 これらの新しい機能は Windows Server 2008 R2 またはそれ以前のオペレーティング システムとの下位互換性がない、従来のコマンドラインからローカルの役割のインストールの Windows Server 2008 R2 で導入された Dism.exe アプリケーションもいまだに使用できます。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>AD DS の役割の構成  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
「以前は DCPROMO と呼ばれる」active Directory ドメイン サービス構成、現時点では、役割のインストールとは別の操作します。 AD DS の役割をインストールした後は、管理者は、サーバー マネージャー内の別のウィザードを使用して、または Windows PowerShell の ADDSDeployment モジュールを使用して、ドメイン コント ローラーとして、サーバーを構成します。  
  
AD DS の役割の構成には 12 年間の現場での経験の上に構築して、最新の Microsoft のベスト プラクティスに基づいてドメイン コント ローラーを構成できるようになりました。 たとえば、ドメイン ネーム システムとグローバル カタログは、すべてのドメイン コント ローラーでは既定でインストールします。  
  
サーバー マネージャー AD DS 構成ウィザードでは、多数の個別ダイアログが少数のプロンプトにマージし、不要になった「詳細」モードでの設定を非表示にします。 昇格プロセス全体が 1 つの展開] ダイアログ ボックスでのインストール中にします。 ウィザードおよび Windows PowerShell の ADDSDeployment モジュールは、重要な変更と追加情報へのリンクをセキュリティ上の問題を説明します。  
  
Dcpromo.exe は、コマンドラインの無人インストールのみ、Windows Server 2012 のままし、不要になったグラフィカル インストール ウィザードを実行します。 強くお勧め Dcpromo.exe の無人インストールの使用を中止して、ADDSDeployment モジュールに ように、ここで推奨されなくなった実行可能ファイルは、次のバージョンの Windows に含まれません。  
  
これらの新しい機能は、下位互換性を Windows Server 2008 R2、または以前のオペレーティング システムを受けません。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]  
> Dcpromo.exe は、グラフィカルなウィザードが含まれていませんし、不要になった役割または機能のバイナリをインストールします。 エクスプ ローラー シェルを返しますから Dcpromo.exe を実行しようとしています。  
>   
> "Active Directory ドメイン サービス インストール ウィザードはサーバー マネージャーに移動されます。 For more information, see https://go.microsoft.com/fwlink/?LinkId=220921."  
>   
> 実行 Dcpromo.exe/unattend しようとしています。 引き続き以前のオペレーティング システムと同様に、バイナリがインストールが警告が表示されます。  
>   
> "Dcpromo 無人操作は、Windows PowerShell の ADDSDeployment モジュールに置き換えられます。 For more information, see https://go.microsoft.com/fwlink/?LinkId=220924."  
>   
> Windows Server 2012 で dcpromo.exe したりされることの機能強化このオペレーティング システムの将来のバージョンの Windows に含まれません。 管理者は使用を中止し、コマンドラインからドメイン コント ローラーを作成する場合は、サポートされている Windows PowerShell モジュールに切り替えます。  
  
#### <a name="prerequisite-checking"></a>前提条件のチェック  
ドメイン コント ローラーの構成では、フォレストおよびドメインのドメイン コント ローラーの昇格を続行する前に評価される前提条件のチェック フェーズも実装します。 これには、FSMO の役割の可用性、ユーザー権限、拡張スキーマの互換性、およびその他の要件が含まれます。 この新しい設計には、ドメイン コント ローラーの昇格が開始し、途中で重大な構成エラーを停止し、問題が軽減されます。 孤立したドメイン コント ローラー メタデータがフォレスト内の可能性が少なくなります。 またはと間違って認識しているサーバーがドメイン コント ローラー。  
  
## <a name="BKMK_SMForest"></a>サーバー マネージャーでフォレストを展開します。  
このセクションでは、グラフィカルな Windows Server 2012 コンピューターにサーバー マネージャーを使用して、フォレスト ルート ドメインの最初のドメイン コント ローラーをインストールする方法について説明します。  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>サーバー マネージャー AD DS の役割のインストール プロセス  
次の図は、以降 ServerManager.exe を実行するいると、ドメイン コント ローラーの昇格の直前で終わってでは、Active Directory ドメイン サービスの役割インストール プロセスを示しています。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>サーバー プールおよび役割の追加  
サーバー マネージャーを実行しているコンピューターからアクセス可能なすべての Windows Server 2012 コンピューターは、プールに適合します。 プール、それらのサーバーのリモート インストール AD DS またはサーバー マネージャー内で使用できる構成オプションを選択します。  
  
サーバーを追加するには、次のいずれかを選択します。  
  
-   をクリックして**管理するその他のサーバーの追加**[ダッシュ ボードのようこそタイル  
  
-   をクリックして、**管理**メニューをクリックし**サーバーの追加**  
  
-   右クリック**すべてのサーバー**選択および**サーバーの追加**  
  
サーバーの追加] ダイアログが表示されます。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
これにより、3 つの方法を使用またはグループ化のプールにサーバーを追加します。  
  
-   Active Directory 検索 (LDAP を使用する必要があります、コンピューターをドメインに属している、オペレーティング システムに基づいてフィルタできますワイルドカードをサポートしています)  
  
-   DNS 検索 (DNS エイリアスまたは IP アドレスを ARP または NetBIOS のブロードキャストか WINS 参照では、使用できないオペレーティング システム フィルター ワイルドカードをサポートしない)  
  
-   インポート (CR/LF で区切られたサーバーのテキスト ファイルのリストを使用)  
  
をクリックして**今すぐ検索**その同じ Active Directory ドメインに参加しているコンピューターからサーバーの一覧を返す、サーバーの一覧から 1 つまたは複数のサーバー名をクリックします。 サーバーを追加する右の矢印をクリックして、**選択された**一覧します。 使用して、**サーバーの追加**のダイアログ ボックスが選択したサーバーをダッシュ ボードの役割のグループに追加します。 をクリックしてまたは**管理**、] をクリックし、**サーバー グループの作成**、] をクリックしてまたは**サーバー グループの作成**ダッシュ ボードで**サーバー マネージャーへようこそ**タイルをカスタム サーバー グループを作成します。  
  
> [!NOTE]  
> サーバーの追加の手順では、サーバーがオンラインまたはアクセス可能であるは検証されません。 ただし、次回の更新時の管理状態ビューでサーバー マネージャーでフラグが到達できないサーバー  
  
役割をインストールするリモートで任意の Windows Server 2012 でコンピュータはのように、プールを追加します。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Windows Server 2012 より前のオペレーティング システムを実行しているサーバーを完全に管理することはできません。 **追加の役割と機能**選択には、Windows PowerShell ServerManager モジュールが実行されている**Install-windowsfeature**します。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
既に AD DS] ダッシュ ボード タイルを右クリックし、選択によって事前に選択の役割を持つリモート サーバー AD DS のインストールを選択する、既存のドメイン コント ローラーでサーバー マネージャー ダッシュ ボードを使用することも**別のサーバーを AD DS に追加**します。 これを呼び出して**Install-windowsfeature AD ドメイン サービス**します。  
  
[サーバー マネージャーを実行しているコンピューター プールに自動的にされます。 AD DS の役割をインストールするにはクリックして、**管理**] メニューとクリック**追加の役割と機能**します。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>インストールの種類  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
**インストールの種類**ダイアログは Active Directory ドメイン サービスをサポートしていないオプションを提供:**リモート デスクトップ サービス シナリオ ベースのインストール**します。 そのオプションは、のみ、リモート デスクトップ サービスをマルチ サーバー分散ワークロードにできます。 選択した場合に、AD DS をインストールできません。  
  
常に、デフォルト値のままインプレース AD DS をインストールするときに:**役割ベースまたは機能ベースのインストール**します。  
  
#### <a name="server-selection"></a>サーバーの選択  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
**サーバーの選択**] ダイアログでは、アクセス可能である限り、前に、プールに追加したサーバーのいずれかを選択することができます。 サーバー マネージャーを実行しているローカル サーバーは自動的に利用可能です。  
  
さらに、Windows Server 2012 オペレーティング システムでのオフラインの HYPER-V VHD ファイルを選択し、サーバー マネージャーは、コンポーネント サービスを使用して直接に、役割を追加します。 これにより、さらにそれらを構成する前に必要なコンポーネントを使って仮想サーバーをプロビジョニングすることができます。  
  
#### <a name="server-roles-and-features"></a>サーバーの役割と機能  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
選択、 **Active Directory Domain Services**ドメイン コント ローラーの昇格を行う場合は、ロール。 すべての Active Directory の管理機能、必要なサービスは、他の役割の一部である表面上に表示されない選択した、サーバー マネージャー インターフェイスまたはいて、自動的にインストールします。  
  
サーバー マネージャーで暗黙的にこの役割をインストールします。 管理機能を示す情報のダイアログの表示もこれに相当、 **-includemanagementtools**引数。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
追加**機能**ここに追加することができます必要に応じて、します。  
  
#### <a name="active-directory-domain-services"></a>Active Directory ドメイン サービス  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
**Active Directory Domain Services**ダイアログは、要件とベスト プラクティスに関する限られた情報を提供します。 AD DS の役割を選択したことの確認を求める主に機能します"この画面が表示されない場合選択しなかった AD DS します。  
  
#### <a name="confirmation"></a>確認  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
**確認**役割のインストールを開始する前に、ダイアログは、最後のチェックポイントです。 役割のインストール後に必要なコンピューターを再起動するためのオプションを提供しますが、AD DS のインストールでは、再起動は必要ありません。  
  
をクリックして**インストール**、役割のインストールを開始する準備ができたらすることを確認します。 開始されると、役割のインストールをキャンセルすることはできません。  
  
#### <a name="results"></a>結果  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
**結果**ダイアログは、現在のインストールの進行状況と現在のインストール状態を示しています。 役割のインストールは、サーバー マネージャーが閉じているかどうかに関係なく続行されます。  
  
インストールの結果を確認するもお勧めします。 閉じた場合、**結果**ダイアログ ボックスでインストールが完了する前に、サーバー マネージャーの通知フラグを使用して結果を確認することができます。 サーバー マネージャーでは、AD DS の役割がインストールされているが、構成されていないさらにドメイン コント ローラーとしてサーバーに対し警告メッセージも表示されます。  
  
**タスクの通知**  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**AD DS 詳細**  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**タスクの詳細**  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>ドメイン コント ローラーに昇格させる  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
AD DS の役割のインストールの末尾には、続行する構成を使用して、**このサーバーのドメイン コント ローラーを昇格**リンクします。 これは、サーバー、ドメイン コント ローラーを作成する必要しますが、すぐに、構成ウィザードを実行する必要はありません。 たとえば、可能性がありますのみするを後で構成のもう 1 つのブランチ オフィスに送信する前に、AD DS バイナリを持つサーバーをプロビジョニングします。 出荷前に、AD DS 役割を追加するには、先に達したときの時間を節約できます。 また、数日から数週間のない、ドメイン コント ローラーをオフライン状態に保つのベスト プラクティスを従ってください。 最後に、これによりドメイン コント ローラーの昇格、後の再起動の少なくとも 1 つを保存する前にコンポーネントを更新できます。  
  
後でこのリンクを選択すると、ADDSDeployment のコマンドレットを呼び出します。 **install-addsforest で**、 **install-addsdomain で**、または**install-addsdomaincontroller**します。  
  
### <a name="uninstallingdisabling"></a>アンインストールする/を無効にします。  
ドメイン コント ローラーにサーバーを昇格したかどうかに関係なく、他のロールと同様に、AD DS 役割を削除します。 ただし、AD DS 役割を削除するには、完了時に再起動が必要です。  
  
Active Directory ドメイン サービスの役割の削除は、というドメイン コント ローラーの降格を完了する前に、インストールと異なります。 これは、そのフォレスト内の適切なメタデータのクリーンアップせずアンインストールの役割のバイナリを持つからドメイン コント ローラーを防ぐために必要です。 詳細については、次を参照してください。[を降格するドメイン コント ローラーとドメイン (&) #40 です。レベル 200 & #41 です。](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
> [!WARNING]  
> ドメイン コント ローラーに昇格はサポートされていませんし、サーバーが正常に起動できなくなります後に Dism.exe または Windows PowerShell の DISM モジュールでの AD DS 役割を削除しています。  
>   
> 、サーバー マネージャーまたは Windows PowerShell 用の AD DS 展開モジュールとは異なり DISM はネイティブのサービス システムを AD DS のないに固有の情報またはその構成を持つです。 サーバーがドメイン コント ローラーで不要になった場合、AD DS の役割をアンインストールするのに Dism.exe または Windows PowerShell の DISM モジュールを使用することはしません。  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>サーバー マネージャーと AD DS フォレスト ルート ドメインを作成します。  
次の図は Active Directory Domain Services 構成プロセスの場合は、以前、AD DS の役割をインストールして開始、 **Active Directory ドメイン サービス構成ウィザード**サーバー マネージャーを使用します。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>展開の構成  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
サーバー マネージャーですべてのドメイン コントローラーの昇格を開始する、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。  
  
新しい Active Directory フォレストを作成する] をクリックして**新しいフォレストの追加**します。 有効なルート ドメイン名; を指定する必要があります。単一ラベル名をすることはできません (たとえば、名前がある必要があります*contoso.com*または類似したとだけでなく*contoso*) および許可されている DNS ドメイン名前付け要件を満たすを使用する必要があります。  
  
For more information on valid domain names, see KB article [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
> [!WARNING]  
> 外部の DNS 名と同じ名前の新しい Active Directory フォレストを作成できません。 たとえば、インターネットの DNS URL が http://contoso.com である場合、内部のフォレストを将来の互換性の問題を避けるために別の名前を選択する必要があります。 その名前は一意で、web トラフィックの低いする必要があります。 例: corp.contoso.com です。  
  
新しいフォレストでは、ドメインの Administrator アカウントの新しい資格情報を必要はありません。 ドメイン コント ローラーの昇格プロセスでは、フォレストのルートを作成するために使用する最初のドメイン コント ローラーからビルトイン Administrator アカウントの資格情報を使用します。 方法はありません (既定)、ビルトイン Administrator アカウントをロックアウトまたは無効にして、その他のドメイン管理者アカウントは使用できない場合に、フォレストへの唯一のエントリ ポイントがある可能性があります。 新しいフォレストを展開する前に、パスワードを知ることが重要です。  
  
**DomainName**を必要と有効な完全修飾ドメイン DNS 名が必要です。  
  
#### <a name="domain-controller-options"></a>ドメイン コント ローラー オプション  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
**ドメイン コント ローラー オプション**を構成することができます、**フォレストの機能レベル**と**ドメインの機能レベル**、新しいフォレスト ルート ドメインのします。 既定では、これらの設定は、新しいフォレスト ルート ドメインの Windows Server 2012 はします。 Windows Server 2012 フォレストの機能レベルでは、Windows Server 2008 R2 フォレストの機能レベル経由で任意の新しい機能は提供されません。 Kerberos の新しい設定を実装するためにのみ、Windows Server 2012 のドメイン機能レベルが必要「常に信頼性情報を提供する」および「防御されていない要求を失敗します」。 Windows Server 2012 での機能レベルの主な用途は、最小限のオペレーティング システムの要件を満たすドメイン コント ローラーへの参加を制限することです。 つまり、Windows Server 2012 ドメイン機能レベルのみドメイン コント ローラーを Windows Server 2012 を実行するドメインをホストできますを指定することができます。  Windows Server 2012 実装と呼ばれる新しいドメイン コント ローラー フラグ**DS_WIN8_REQUIRED**で、 **DSGetDcName**だけ Windows Server 2012 ドメイン コント ローラーを検出が NetLogon の関数です。 これにより、柔軟性より同種または異機種混在環境のフォレストのドメイン コント ローラー上で実行するどのオペレーティング システムが許可されているようにできます。  
  
For more information about domain controller Location, review [Directory Service Functions](https://msdn.microsoft.com/library/ms675900(VS.85).aspx).  
  
のみ構成可能なドメイン コント ローラーの機能は、DNS サーバー オプションです。 マイクロソフトでは、すべてのドメイン コント ローラーが DNS サービスはそのため、任意のモードまたはドメインで、ドメイン コント ローラーをインストールするときに、既定では、このオプションが選択されている分散環境での高可用性を提供することをお勧めします。 グローバル カタログと読み取り専用ドメイン コント ローラー オプションは使用できません。 新しいフォレスト ルート ドメインを作成するときに最初のドメイン コント ローラーは、GC である必要があり、読み取り専用ドメイン コント ローラー (RODC) にすることはできません。  
  
指定した**ディレクトリ サービス復元モード パスワード**既定では、強力なパスワードは必要ありませんが、サーバーに適用されるパスワード ポリシーに従う必要があります空白でないもののみです。 常に強力で複雑なパスワードまたは可能であれば、パスフレーズを選択します。  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
**DNS オプション**ページでは、DNS 委任を構成し、別の DNS 管理者資格情報を提供することができます。  
  
構成できません DNS のオプションや委任 Active Directory ドメイン サービス構成ウィザードで新しい Active Directory フォレスト ルート ドメイン選択したをインストールするときに、 **DNS サーバー**上、**ドメイン コント ローラー オプション**ページ。 **DNS 委任の作成**オプションは、既存の DNS サーバー インフラストラクチャに新しいフォレスト ルート DNS ゾーンを作成するときに使用します。 このオプションでは、代替 DNS 管理者資格情報を DNS ゾーンを更新する権限を持つを提供することができます。  
  
For more information about whether you need to create a DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
#### <a name="additional-options"></a>その他のオプション  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
**追加オプション**] ページに、ドメインの NetBIOS 名、およびそれを上書きすることができます。 既定では、NetBIOS ドメイン名は上で提供される完全修飾ドメイン名の一番左のラベルと一致する、**展開構成**ページ。 たとえば、corp.contoso.com の完全修飾ドメイン名を指定した場合、既定の NetBIOS ドメイン名は CORP です。  
  
名前が 15 文字以内と競合しない別の NetBIOS 名では変更します。 別の NetBIOS 名と競合している、名前に、数字が付加されます。 名前が 15 文字以内の場合、ウィザードは、切り捨てられた一意の候補を提供します。 ウィザードの最初の検証どちらの場合、名前が既に WINS 参照で使用されていないおよび NetBIOS ブロードキャストします。  
  
For more information on valid domain names, see KB article [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
#### <a name="paths"></a>パス  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
**パス**および SYSVOL 共有のページでは、AD DS データベース、データベースのトランザクション ログの既定のフォルダーの場所を上書きすることができます。 既定の場所は、常に %systemroot% (つまり C:\Windows) のサブディレクトリ内にします。  
  
#### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
**オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、要件を満たしていることを確認します。 これは、サーバー マネージャーを使っているときに、インストールを停止する最後の機会ではありません。 これは、単に、構成を続行する前に、設定を確認するオプション  
  
**オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。 このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。 例えば：  
  
```powershell 
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSForest `  
-CreateDNSDelegation `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainName "corp.contoso.com" `  
-DomainNetBIOSName "CORP" `  
-ForestMode "Win2012" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NoRebootOnCompletion:$false `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> サーバー マネージャーは、一般にすべての引数と値のプロモーションおよび (サービス パックまたは Windows の将来のバージョン間で変わる可能性がある) のように既定の設定に依存しないときに入力します。 1 つの例外は、 **-safemodeadministratorpassword**引数です (これは意図的に省略すると、スクリプトから)。 確認プロンプトを強制するには、コマンドレットを対話的に実行するときに値を省略します。  
  
#### <a name="prerequisites-check"></a>前提条件の確認  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
**前提条件のチェック**AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバーの構成が新しい AD DS フォレストをサポートできることを検証します。  
  
新しいフォレスト ルート ドメインをインストールする場合、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、一連のモジュラー テストを呼び出します。 これらのテストでは、推奨される修復のオプションを使用してアラートです。 必要なだけ何度でもテストを実行することができます。 すべての前提条件のテストまで、ドメイン コントローラーのプロセスを続行できません渡します。  
  
**前提条件のチェック**以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかです。  
  
具体的な前提条件チェックの詳細については、次を参照してください。[前提条件のチェック](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)します。  
  
#### <a name="installation"></a>インストール  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
ときに、**インストール**ページが表示されます、ドメイン コントローラーの構成を開始、停止またはできません取り消されます。 操作の詳しい内容は、このページに表示され、ログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> 複数の役割のインストールと AD DS 構成ウィザードは同じサーバー マネージャー コンソールから同時に実行できます。  
  
#### <a name="results"></a>結果  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  
## <a name="BKMK_PSForest"></a>Windows PowerShell を使用したフォレストを展開します。  
このセクションでは、コア Windows Server 2012 コンピューター上の Windows PowerShell を使用して、フォレスト ルート ドメインの最初のドメイン コント ローラーをインストールする方法について説明します。  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>Windows powershell を使った AD DS の役割のインストール プロセス  
いくつかの単純な ServerManager 展開コマンドレットを実装すると、展開プロセスに、さらに期待したビジョンを AD DS の簡略化された管理します。  
  
次の図は、以降で実行する、Active Directory ドメイン サービスの役割インストール プロセスを示しています。 **PowerShell.exe**し、ドメイン コント ローラーの昇格の直前で終わっています。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager コマンドレット|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|WindowsFeature/追加-Install-windowsfeature|***名***<br /><br />*-再起動します。*<br /><br />*-IncludeAllSubFeature*<br /><br />*-Includemanagementtools*<br /><br />ソース<br /><br />*-ComputerName*<br /><br />資格情報<br /><br />-Logpath<br /><br />*Vhd*<br /><br />*-$Servernames-configurationfilepath*|  
  
> [!NOTE]  
> 必須ではありません、引数**-includemanagementtools** AD DS の役割のバイナリをインストールするときに強くお勧め  
  
ServerManager モジュールは、Windows PowerShell 用の新しい DISM モジュールの役割のインストール、状態、および削除の部分を公開します。 このレイヤリングが、ほとんどのタスクを簡略化され、強力な (ただし、使い方を間違うと危険な) の直接使用する必要が減ります DISM モジュール。  
  
使用**Get-command**エイリアスと ServerManager コマンドレットをエクスポートします。  
  
```powershell  
Get-Command -module ServerManager  
```  
  
例えば：  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
Active Directory ドメイン サービスの役割を追加するだけで実行、 **Install-windowsfeature** AD DS の役割の名前を引数としてとします。 サーバー マネージャーと同様に暗黙的に、AD DS の役割のすべての必要なサービスが自動的にインストールします。  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
-インストールされている AD DS の管理ツールをして、これを強くお勧めの場合は、提供、 **-includemanagementtools**引数。  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
例えば：  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
すべての機能とそのインストール状態を持つロールを一覧表示するには使用**Get-windowsfeature**引数なしで実行します。 指定**- ComputerName**引数をリモート サーバーからインストール状態を指定します。  
  
```powershell  
Get-WindowsFeature  
```  
  
**Get-windowsfeature**ができない、フィルタ リング メカニズムを使う必要があります**Where-object**とパイプラインを特定の機能を検索します。 パイプラインは、チャンネルのデータを渡すための複数のコマンドレット間で使用し、Where-object コマンドレットはフィルターとして機能します。 組み込み**$_**変数は、現在のオブジェクトを含むことが任意のプロパティと共にパイプラインに渡すとして機能します。  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
たとえば、すべて検索する機能が含まれる"Active Dir"、**表示名**プロパティ。  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
例を次に示します。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
For more information about more Windows PowerShell operations with pipelines and Where-Object, see [Piping and the Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
Windows PowerShell 3.0 は、このパイプライン操作に必要なコマンドライン引数を大幅に簡略化されたにも注意してください。 Windows PowerShell 2.0 は必要があります。  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Windows PowerShell パイプラインを使用すると、判読しやすい結果を作成できます。 例えば：  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
注: 方法を使用して、 **Select-object**コマンドレットと、 **- expandproperty**引数興味深いデータが返されます。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> **Select-object expandproperty**引数が少し全体的なインストール パフォーマンス速度が低下します。  
  
### <a name="BKMK_PS"></a>Windows PowerShell による AD DS フォレスト ルート ドメインを作成します。  
ADDSDeployment モジュールを使用して新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```powershell  
Install-addsforest  
```  
  
**Install-addsforest**コマンドレットはだけです (前提条件のチェックとインストール) の 2 つのフェーズです。 以下の 2 つの図の最低限の必須引数を使用したインストール フェーズを表示する**- domainname**します。  
  
|||  
|-|-|  
|ADDSDeployment コマンドレット|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Install-addsforest|-確認します。<br /><br />*-CreateDNSDelegation*<br /><br />*-DatabasePath*<br /><br />*DomainMode-*<br /><br />***-DomainName***<br /><br />***-Domainnetbiosname***<br /><br />*-DNSDelegationCredential*<br /><br />*ForestMode-*<br /><br />フォース<br /><br />*-InstallDNS*<br /><br />*-Logpath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-Safemodeadministratorpassword*<br /><br />-SkipAutoConfigureDNS<br /><br />-SkipPreChecks<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-Domainnetbiosname** DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合、または名前が 15 文字を超える場合は、引数が必要です。  
  
相当のサーバー マネージャー**展開構成**ADDSDeployment コマンドレットと引数は。  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
相当のサーバー マネージャーのドメイン コント ローラー オプション ADDSDeployment コマンドレット引数は次のとおりです。  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
**Install-addsforest**引数が指定されていない場合はサーバー マネージャーと同じ既定値に従います。  
  
**SafeModeAdministratorPassword**引数の操作は特別な。  
  
-   場合*が指定されていない*を引数としてコマンドレットは、して、マスクされたパスワードの確認入力を求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
    たとえば、corp.contoso.com という名前の新しいフォレストを作成して、マスクされたパスワードの確認入力を求め。  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   指定されている場合*値を持つ*、値が、セキュリティで保護された文字列を指定する必要があります。 コマンドレットを対話的に実行するときに推奨される使用方法はありません。  
  
たとえば、手動での入力を求めるパスワードを使用して、**Read-host**コマンドレットをセキュリティで保護された文字列をユーザーに確認します。  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> 前のオプションは、パスワードを確認しない、細心の注意を使用して、: パスワードは表示されません。  
  
これはお勧めはクリア テキストの変換済みの変数として、セキュリティで保護された文字列を提供できます。  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
最後に、ファイル、暗号化されたパスワードに格納され、クリア テキストのパスワードが表示されることがなく、後で再する可能性があります。 例えば：  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> テキストをクリアや暗号化されたパスワードの保存を提供または推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのドメイン コントローラーの DSRM パスワードを認識します。 その暗号化されたパスワードを取り消すファイルへのアクセスを持つユーザー可能性があります。 した情報を使って、DSRM で起動された DC にログオンし、最終的にドメイン コントローラー自体は、自分の権限を Active Directory フォレストで最も高いレベルに昇格を偽装します。 追加の手順を使用してセット**System.Security.Cryptography**データはことをお勧めがスコープ外にテキスト ファイルを暗号化します。 パスワードの保存を絶対に避けることをお勧めします。  
  
ADDSDeployment コマンドレットは、DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップする追加のオプションを提供します。 サーバー マネージャーを使用する場合、この構成オプションをスキップすることはできません。 この引数が重要なは、ドメイン コントローラーを構成する前に、DNS サーバーの役割をインストールした場合にのみ。  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
**DomainNetBIOSName**操作も特殊です。  
  
-   場合、 **DomainNetBIOSName**引数が NetBIOS ドメイン名と、単一ラベル プレフィックスのドメイン名で指定されていない、 **DomainName**引数が 15 文字以下、自動的に生成された名前で昇格が続行します。  
  
-   場合、 **DomainNetBIOSName**引数が NetBIOS ドメイン名と、単一ラベル プレフィックスのドメイン名で指定されていない、 **DomainName**引数が 16 文字以上し、昇格は失敗します。  
  
-   場合、 **DomainNetBIOSName**引数が 15 文字以下の NetBIOS ドメイン名と共に指定し、指定された名前で昇格が続行します。  
  
-   場合、 **DomainNetBIOSName**引数が NetBIOS ドメイン名が 16 文字以上指定し、昇格は失敗します。  
  
相当のサーバー マネージャーの追加のオプションの ADDSDeployment コマンドレット引数です。  
  
```powershell  
-domainnetbiosname <string>  
```  
  
相当のサーバー マネージャー**パス**ADDSDeployment コマンドレット引数は。  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
オプションを使用して**Whatif**引数を使用、 **Install-addsforest**コマンドレットを構成情報を確認します。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示できます。  
  
例えば：  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
バイパスすることはできません、**の前提条件チェック**ときは、サーバー マネージャーを使用して進むことができます、プロセスは次の引数を使用して、AD DS 展開コマンドレットを使用する場合。  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft は、部分的なドメイン コントローラーの昇格につながるまたは AD DS フォレストが破損している前提条件のチェックをスキップすることです。  
  
注: 同様、サーバー マネージャー、 **Install-addsforest**昇格プロセスで、サーバーの再起動は自動的にされることを知らせます。  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![新しいフォレストをインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めします。 正常に機能するドメイン コントローラーを再起動しなければなりません。  
  
## <a name="see-also"></a>参照してください。  
[Active Directory Domain Services (TechNet ポータル)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Windows Server 2008 R2 用 active Directory ドメイン サービス](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Windows Server 2008 の active Directory ドメイン サービス](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Windows Server テクニカル リファレンス (Windows Server 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[Active Directory 管理センター: 作業 (Windows Server 2008 R2) の開始](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[Windows PowerShell (Windows Server 2008 R2) による active Directory の管理](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[依頼 the Directory Services Team (正式な Microsoft コマーシャル テクニカル サポートのブログ)](http://blogs.technet.com/b/askds)  
  

