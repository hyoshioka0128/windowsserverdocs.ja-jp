---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: Windows Server 2012 の新しい Active Directory フォレストをインストールする (レベル 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f87c383618bc1cef09652ea36e172fc634f5128e
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948814"
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>Windows Server 2012 の新しい Active Directory フォレストをインストールする (レベル 200)

>適用対象: Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、新しい Windows Server 2012 Active Directory Domain Services のドメイン コントローラーの昇格機能について、基本的なレベルでの説明を行います。 Windows Server 2012 において、AD DS は Dcpromo ツールに代えて、サーバー マネージャーおよび Windows PowerShell ベースの展開システムを使用します。  
  
-   [Active Directory Domain Services の簡略化された管理](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [技術概要](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [サーバーマネージャーを使用したフォレストの展開](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Windows PowerShell を使用してフォレストを展開する](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Active Directory Domain Services の簡略化された管理  
Windows Server 2012 では、次世代を見据えた Active Directory Domain Services の簡略化された管理が導入され、Windows 2000 Server 以来、最も革新的なドメイン構想の見直しが行われています。 AD DS の簡略化された管理は、Active Directory の 12 年に及ぶ実績から学んだ教訓を活かし、アーキテクトや管理者にとってサポート性、柔軟性、直感性に優れた管理エクスペリエンスを提供します。 このことは、既存テクノロジの新しいバージョンを創出すると共に、Windows Server 2008 R2 でリリースされたコンポーネントの機能を拡張することを意味していました。  
  
### <a name="what-is-ad-ds-simplified-administration"></a>AD DS の簡略化された管理とは  
AD DS の簡略化された管理とは、ドメイン展開の再イメージ化です。 その一部の機能を次に示します。  
  
-   AD DS の役割の展開は、新しいサーバー マネージャー アーキテクチャに組み込まれ、リモート インストールが可能になりました。  
  
-   AD DS の展開と構成のエンジンは、GUI によるセットアップを使用するときも、Windows PowerShell になりました。  
  
-   昇格機能には、新しいドメイン コントローラーに対するフォレストとドメインの準備状態を検証する前提条件のチェックが含まれており、昇格に失敗する可能性が低減されます。  
  
-   Windows Server 2012 のフォレストの機能レベルでは新しい機能は実装されず、ドメインの機能レベルは Kerberos の新機能のサブセットについてのみ必要となるので、管理者は同種のドメイン コントローラー環境を頻繁に用意する必要性から解放されます。  
  
### <a name="purpose-and-benefits"></a>目的と利点  
このような変更点は、簡略化されたというよりは、複雑になったように思えるかもしれません。 しかし、AD DS の展開プロセスを再設計することで、多くの手順とベスト プラクティスを、より少ない、より簡単な操作にまとめることができました。 たとえば、新しいレプリカ ドメイン コントローラーの GUI での構成は、以前は 12 個のダイアログが必要でしたが、今では 8 個のダイアログでできるようになりました。 新しい Active Directory フォレストを作成するときは、1 つの Windows PowerShell コマンドと、 引数を 1 つだけ (ドメインの名前) 指定すれば済みます。  
  
Windows Server 2012 の Windows PowerShell がこれほどまでに重要視される理由は何でしょうか。 分散コンピューティングが進化するにつれて、Windows PowerShell は、グラフィカル インターフェイスとコマンドライン インターフェイスの両方から構成と保守を行える単一のエンジンとなりました。 多くの機能を駆使してあらゆるコンポーネントのスクリプト処理が可能で、その最上級の能力は IT 技術者にとって API と同等です。 クラウドベース コンピューティングのユビキタス化と歩調を合わせて、Windows PowerShell もいよいよサーバーをリモート管理する機能を備えるようになりました。グラフィカル インターフェイスを持たないコンピューターが、モニターやマウスのあるコンピューターと同じ管理機能を発揮できるのです。  
  
経験豊富な AD DS 管理者は、以前の知識を大いに活かせることに気が付くでしょう。 経験の浅い管理者は、習得のしやすさを実感します。  
  
## <a name="BKMK_TechOverview"></a>技術概要  
  
### <a name="what-you-should-know-before-you-begin"></a>始めに知っておくべきこと  
このトピックは、以前のリリースの Active Directory Domain Services に関する知識があることを前提としており、その目的と機能といった基本事項については説明しません。 AD DS の詳細については、次にリンク設定された TechNet ポータルのページを参照してください。  
  
-   [Windows Server 2008 R2 の Active Directory Domain Services](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Windows Server 2008 向け Active Directory Domain Services](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Windows Server テクニカルリファレンス](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>機能の説明  
  
#### <a name="ad-ds-role-installation"></a>AD DS の役割のインストール  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Active Directory ドメイン サービスのインストールでは、Windows Server 2012 における他のすべてのサーバーの役割と機能と同様に、サーバー マネージャーと Windows PowerShell を使用します。 Dcpromo.exe プログラムによる GUI 構成オプションの提供は行われません。  
  
ローカルとりモートの両方のインストールで、サーバー マネージャーの GUI によるウィザードまたは Windows PowerShell の ServerManager モジュールを使用します。 このようなウィザードやコマンドレットのインスタンスを複数実行し、さまざまなサーバーをターゲットにすることで、1 つのコンソールから複数のドメイン コントローラーに対して AD DS を同時展開できます。 これらの新しい機能は Windows Server 2008 R2 以前のオペレーティング システムとの下位互換性はないものの、従来のコマンドラインから実行するローカルの役割のインストールでは、Windows Server 2008 R2 で導入された Dism.exe アプリケーションもいまだに使用することができます。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>AD DS の役割の構成  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
Active Directory Domain Services 構成 "以前の DCPROMO" は、役割のインストールからの個別の操作になりました。 AD DS の役割のインストール後、管理者は、サーバー マネージャー内の別のウィザードまたは Windows PowerShell の ADDSDeployment モジュールを使って、サーバーをドメイン コントローラーとして構成します。  
  
AD DS の役割の構成では、12 年間の現場実績を基盤として、現在は Microsoft の最新のベスト プラクティスに基づいてドメイン コントローラーを構成します。 たとえば、ドメイン ネーム システムとグローバル カタログは既定で、すべてのドメイン コントローラーにインストールされます。  
  
サーバーマネージャー AD DS 構成ウィザードでは、多くの個々のダイアログがより少数のプロンプトにマージされ、"詳細" モードでは設定が非表示になりません。 昇格プロセス全体が、インストール時の 1 つの拡張ダイアログ ボックスで行われます。 ウィザードおよび Windows PowerShell の ADDSDeployment モジュールでは、重要な変更とセキュリティに関する考慮事項が、詳細情報へのリンクと共に表示されます。  
  
Dcpromo.exe はコマンドラインからの無人インストールのためだけに Windows Server 2012 に残され、GUI でのインストール ウィザードは実行しなくなりました。 無人インストールの目的で Dcpromo.exe を使用することは今後停止して、代わりに ADDSDeployment モジュールを使用することを強くお勧めします。現時点で非推奨の実行可能ファイルは、次のバージョンの Windows に含まれないからです。  
  
これらの新しい機能は、Windows Server 2008 R2 以前のオペレーティング システムとの下位互換性がありません。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]
> Dcpromo.exe は GUI によるウィザードを提供しなくなり、役割や機能のバイナリをインストールをしなくなりました。 Explorer シェルから Dcpromo.exe を実行すると、次のメッセージが返されます。  
> 
> "Active Directory ドメインサービスインストールウィザードはサーバーマネージャーで再配置されます。 詳細については、「<https://go.microsoft.com/fwlink/?LinkId=220921>」を参照してください。  
> 
> Dcpromo.exe /unattend を実行すると、以前のオペレーティング システムの場合と同様にバイナリがインストールされますが、次の警告が表示されます。  
> 
> "Dcpromo の無人操作は、Windows PowerShell の ADDSDeployment モジュールに置き換えられています。 詳細については、「<https://go.microsoft.com/fwlink/?LinkId=220924>」を参照してください。  
> 
> Windows Server 2012 では dcpromo.exe を非推奨としており、この実行可能ファイルは、Windows の将来のバージョンに含まれることもなければ、このオペレーティング システムで機能拡張されることもありません。 管理者はその使用を今後停止して、コマンドラインからドメイン コントローラーを作成したい場合は、サポートされている Windows PowerShell モジュールに切り替える必要があります。  
  
#### <a name="prerequisite-checking"></a>前提条件のチェック  
ドメイン コントローラーの構成には前提条件のチェック フェーズも実装されており、これによって、ドメイン コントローラーの昇格を続行する前のフォレストとドメインの評価が行われます。 前提条件には、FSMO 役割の可用性、ユーザー権限、拡張スキーマの互換性などの要件が含まれます。 この新しい設計によって、ドメイン コントローラーの昇格が開始された後、重大な構成エラーによって昇格が途中で停止される問題が軽減されます。 また、ドメイン コントローラーのメタデータがフォレスト内で孤立状態になる可能性や、サーバーが自身をドメイン コントローラーであると間違って認識する可能性が少なくなります。  
  
## <a name="BKMK_SMForest"></a>サーバーマネージャーを使用したフォレストの展開  
ここでは、GUI による Windows Server 2012 コンピューター上で、サーバー マネージャーを使って最初のドメイン コントローラーをフォレスト ルート ドメインにインストールする方法について説明します。  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>サーバー マネージャーでの AD DS の役割のインストール プロセス  
次の図は、Active Directory Domain Services の役割のインストール プロセスを示しています。管理者が ServerManager.exe を実行するところから始まり、ドメイン コントローラーの昇格の直前で終わっています。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>サーバー プールおよび役割の追加  
サーバー マネージャーを実行しているコンピューターからアクセスできる Windows Server 2012 コンピューターはいずれも、プールの対象となります。 プールしたサーバーは、AD DS のリモート インストールなど、サーバー マネージャーで使用できる構成オプションの対象として選択できます。  
  
サーバーを追加するには、次のいずれかを選択します。  
  
-   ダッシュボードのようこそタイルにある **[管理するサーバーの追加]** をクリックする  
  
-   **管理** メニューをクリックし、**サーバーの追加** をクリックする  
  
-   **[すべてのサーバー]** を右クリックし、 **[サーバーの追加]** をクリックする  
  
[サーバーの追加] ダイアログが表示されます。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
これで、使用またはグループ化するためのプールに 3 つの方法でサーバーを追加できます。  
  
-   Active Directory 検索 (LDAP を使用する、コンピューターがドメインに属している必要がある、オペレーティング システム フィルターを許可する、ワイルドカードをサポートする)  
  
-   DNS 検索 (ARP または NetBIOS のブロードキャストか WINS 参照で DNS エイリアスまたは IP アドレスを使用する、オペレーティング システム フィルターを許可しない、ワイルドカードをサポートしない)  
  
-   インポート (CR/LF で区切られたテキスト ファイルのサーバー リストを使用する)  
  
**[検索開始]** をクリックすると、そのコンピューターが参加している同じ Active Directory ドメインからサーバーの一覧が返されます。その一覧で 1 つ以上のサーバー名をクリックします。 右矢印をクリックして **[選択済み]** の一覧に追加します。 **[サーバーの追加]** ダイアログを使って、選択したサーバーをダッシュボードの役割のグループに追加します。 または、 **[管理]** をクリックして **[サーバー グループの作成]** をクリックするか、ダッシュボードの **[サーバー マネージャーへようこそ]** タイル上にある **[サーバー グループの作成]** をクリックして、カスタム サーバー グループを作成します。  
  
> [!NOTE]  
> [サーバーの追加] の手順では、サーバーがオンライン (アクセス可能) かどうかは確認されません。 ただし、次回の更新時に、サーバー マネージャーの管理状態ビューで、到達できないサーバーすべてにフラグが設定されます。  
  
次に示すように、プールに追加された任意の Windows Server 2012 コンピューターには役割をリモートでインストールできます。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Windows Server 2012 より前のオペレーティング システムを搭載しているサーバーを完全に管理することはできません。 **[役割と機能の追加]** の選択によって、Windows PowerShell ServerManager モジュールの **Install-WindowsFeature**が実行されます。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
既存のドメイン コントローラー上のサーバー マネージャー ダッシュボードを使って、役割が事前に選択されたリモート サーバー AD DS インストールを選択することもできます。それには、AD DS ダッシュボード タイルを右クリックし、 **別のサーバーへの AD DS の追加** をクリックします。 これにより **Install-WindowsFeature AD-Domain-Services**が起動されます。  
  
サーバー マネージャーを実行しているコンピューターはそれ自身を自動的にプールします。 ここで AD DS の役割をインストールするには、単に、 **[管理]** メニューをクリックし、 **[役割と機能の追加]** をクリックします。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>インストールの種類  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
**[インストールの種類]** ダイアログには、Active Directory ドメイン サービスをサポートしないオプション、 **[リモート デスクトップ サービスのシナリオ ベースのインストール]** があります。 このオプションは、マルチサーバー分散ワークロードでのリモート デスクトップ サービスを許可するだけです。 これを選択した場合、AD DS をインストールすることはできません。  
  
AD DS をインストールするときは、常に既定のオプション選択のままにしてください( **[役割ベースまたは機能ベースのインストール]** )。  
  
#### <a name="server-selection"></a>サーバーの選択  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
**[サーバーの選択]** ダイアログでは、プールに追加済みのサーバーから 1 つ、アクセス可能なものに限り選択することができます。 サーバー マネージャーを実行しているローカル サーバーは自動的に利用可能になります。  
  
また、Windows Server 2012 オペレーティング システムではオフラインの Hyper-V VHD ファイルを選択でき、サーバー マネージャーはコンポーネント サービスを直接介して、それらのファイルに役割を追加します。 このしくみにより、必要なコンポーネントを使って仮想サーバーをプロビジョニングしてから、それらをさらに構成できます。  
  
#### <a name="server-roles-and-features"></a>サーバーの役割と機能  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
ドメイン コントローラーの昇格を行う場合は、 **Active Directory ドメイン サービス** の役割を選択します。 Active Directory の管理機能と必須サービスはすべて自動的にインストールされます。表面上は別の役割の一部であったり、サーバー マネージャー インターフェイスに選択状態で表示されない場合であってもです。  
  
サーバー マネージャーはまた、追加する役割によってどの管理機能が暗黙的にインストールされるかを示す情報のダイアログを表示します。この機能は **-IncludeManagementTools** 引数を指定するのと同じです。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
ここでは必要に応じて他の **機能** を追加できます。  
  
#### <a name="active-directory-domain-services"></a>[Active Directory Domain Services]  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
**[Active Directory ドメイン サービス]** ダイアログは、要件とベスト プラクティスに関する限定された情報を提供します。 主に、"この画面が表示されない場合は AD DS を選択していません" という AD DS の役割を選択したことを示す確認として機能します。  
  
#### <a name="confirmation"></a>確認  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
**[確認]** ダイアログは、役割のインストールを開始する前の最後のチェックポイントです。 役割のインストール後に必要に応じてコンピューターを再起動するオプションがありますが、AD DS のインストールでは再起動は必要ありません。  
  
**[インストール]** をクリックすることで、役割のインストールを開始する準備が整っていることを確認します。 いったん開始されたインストールを取り消すことはできません。  
  
#### <a name="results"></a>結果  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
**[結果]** ダイアログには、インストールの現在の進行状況と状態が表示されます。 サーバー マネージャーが閉じているかどうかにかかわらず、役割のインストールは続行されます。  
  
それでも、インストールの結果を確認することをお勧めします。 インストールが完了する前に **[結果]** ダイアログを閉じた場合は、サーバー マネージャーの通知フラグを使って結果を確認できます。 サーバー マネージャーは、AD DS の役割がインストール済みであるものの、ドメイン コントローラーとしての追加構成が行われていないサーバーに対して警告のメッセージも表示します。  
  
**タスクの通知**  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**AD DS の詳細**  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**タスクの詳細**  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>ドメイン コントローラーに昇格する  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
AD DS の役割のインストール終了時、 **[このサーバーをドメイン コントローラーに昇格する]** リンクを使って構成を続行できます。 この作業はサーバーをドメイン コントローラーにするために必要ですが、すぐに構成ウィザードを実行する必要はありません。 たとえば、AD DS バイナリを使ってプロビジョニングだけ完了した状態のサーバーを、他のブランチ オフィスに送って、後で構成を行いたい場合があります。 出荷の前に AD DS の役割を追加しておけば、出荷先に着いたときに時間を節約できます。 また、ドメイン コントローラーを何日もまたは何週間もオフラインにしないことをお勧めします。 そうすることでドメイン コントローラーの昇格の前にコンポーネントを更新できるようになり、後の再起動を 1 回以上省略できます。  
  
このリンクを後で選択すると、ADDSDeployment のコマンドレット ( **install-addsforest**、 **install-addsdomain**、または **install-addsdomaincontroller**) が呼び出されます。  
  
### <a name="uninstallingdisabling"></a>アンインストール/無効化  
AD DS の役割は他のすべての役割と同様に削除します。サーバーをドメイン コントローラーに昇格したかどうかは関係ありません。 ただし、AD DS の役割を削除するときは、完了時に再起動が必要になります。  
  
Active Directory Domain Services の役割の削除は、作業完了の前にドメイン コントローラーの降格が必要になるという点で、インストールとは異なります。 メタデータのクリーンアップがフォレスト内で適切に行われることなく、ドメイン コントローラーがその役割のバイナリをアンインストールされてしまうことを防ぐために降格は必要です。 詳細については、「[ドメインコントローラーと&#40;ドメインレベル&#41;200 の降格](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)」を参照してください。  
  
> [!WARNING]  
> ドメイン コントローラーに昇格した後に Dism.exe または Windows PowerShell DISM モジュールを使用して AD DS 役割を削除することはサポートされておらず、サーバーの正常な起動を妨げます。  
>   
> サーバー マネージャーまたは Windows PowerShell の AD DS 展開モジュールとは異なり、DISM はネイティブのサービス システムであり、AD DS またはその構成に関する知識を元々備えていません。 サーバーがドメイン コントローラーでなくなる場合を除き、AD DS の役割をアンインストールするのに Dism.exe または Windows PowerShell の DISM モジュールを使用しないでください。  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>サーバー マネージャーを使って AD DS フォレスト ルート ドメインを作成する  
次の図は Active Directory ドメイン サービスの構成プロセスを示しています。ここでは、既にサーバー マネージャーを使って AD DS の役割をインストールし、 **Active Directory ドメイン サービス構成ウィザード** を開始しています。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>展開構成  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
サーバー マネージャーは各ドメイン コントローラーの昇格を **[配置構成]** ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。  
  
新しい Active Directory フォレストを作成するには、 **[新しいフォレストを追加する]** をクリックします。 有効なルート ドメイン名を指定する必要があります。名前は単一ラベルであってはならず (たとえば、単に *contoso* ではなく、 *contoso.com*のようにする必要があります)、許可されている DNS ドメイン名前付け要件に従う必要があります。  
  
有効なドメイン名の詳細については、サポート技術情報の記事「 [Naming conventions in Active Directory for computers, domains, sites, and OUs (Active Directory 内のコンピューター、ドメイン、サイト、および OU の名前付け規則)](https://support.microsoft.com/kb/909264)」を参照してください。  
  
> [!WARNING]  
> 新しい Active Directory フォレストを、外部の DNS 名と同じ名前で作成しないでください。 たとえば、インターネット DNS URL が http://contoso.com 場合は、今後の互換性の問題を回避するために、内部フォレストに別の名前を選択する必要があります。 その名前は、一意で、Web トラフィックにはありそうもないものにする必要があります。 たとえば、corp.contoso.com のようにします。  
  
新しいフォレストには、ドメインの Administrator アカウントの新しい資格情報は必要ありません。 ドメイン コントローラーの昇格プロセスでは、フォレスト ルートの作成に使用した最初のドメイン コントローラーの組み込みの Administrator アカウントの資格情報を使用します。 組み込みの Administrator アカウントを、無効にしたり、ロックアウトしたりすることはできません (既定)。他のドメイン管理者アカウントを使用できない場合は、組み込みの Administrator アカウントがフォレストへの唯一のエントリ ポイントとなる場合があります。 新しいフォレストを展開する前に、そのパスワードを知っておくことが重要です。  
  
**DomainName** は有効な完全修飾ドメイン DNS 名である必要があり、これは必須です。  
  
#### <a name="domain-controller-options"></a>ドメイン コントローラー オプション  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
**[ドメイン コントローラー オプション]** では、新しいフォレスト ルート ドメインの **フォレストの機能レベル** と **ドメインの機能レベル** を構成できます。 既定では、これらの設定は、新しいフォレストルートドメインの Windows Server 2012 です。 Windows Server 2012 フォレストの機能レベルでは、Windows Server 2008 R2 フォレストの機能レベルよりも新しい機能は提供されません。 Windows Server 2012 ドメインの機能レベルは、新しい Kerberos 設定を実装するためにのみ必要です。 "常に信頼性情報を提供する" と "防御認証要求に失敗" します。 Windows Server 2012 の機能レベルの主な用途は、ドメインへの参加を、最小限のオペレーティングシステム要件を満たすドメインコントローラーに制限することです。 言い換えると、windows server 2012 を2012実行しているドメインコントローラーがドメインをホストできるドメイン機能レベルのみを指定できます。  Windows Server 2012 では、Windows Server 2012 ドメインコントローラーを排他的に特定する NetLogon の**DSGetDcName**関数で**DS_WIN8_REQUIRED**と呼ばれる新しいドメインコントローラーフラグが実装されています。 このフラグにより、ドメイン コントローラー上での実行を許可されるオペレーティング システムの種類という観点から、より同種のサーバーまたは同種のフォレストを柔軟に構成できるようになります。  
  
ドメイン コントローラー検出の詳細については、「 [Directory Service Functions (ディレクトリ サービスの関数)](https://msdn.microsoft.com/library/ms675900(VS.85).aspx)」を参照してください。  
  
唯一構成可能なドメイン コントローラーの機能は、DNS サーバー オプションです。 分散環境において高可用性を実現するため、すべてのドメイン コントローラーが DNS サービスを提供することをお勧めします。ドメイン コントローラーを、どのモードで、どのドメインにインストールするときでも、このオプションが既定で選択されるのはそのためです。 新しいフォレスト ルート ドメインを作成するとき、グローバル カタログと読み取り専用ドメイン コントローラーのオプションは使用できません。最初のドメイン コントローラーはグローバル カタログ (GC) である必要があり、読み取り専用ドメイン コントローラー (RODC) であってはいけません。  
  
指定する **ディレクトリ サービスの復元モード パスワード** は、サーバーに適用されるパスワード ポリシーに準拠する必要がありますが、既定では強力なパスワードである必要はなく、空白パスワードではないことだけが必要です。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
**[DNS オプション]** ページでは、DNS 委任を構成し、代替の DNS 管理者資格情報を指定できます。  
  
新しい Active Directory フォレスト ルート ドメインをインストールするとき、Active Directory ドメイン サービス構成ウィザードの **[ドメイン コントローラー オプション]** ページにある **[DNS サーバー]** を選択して、DNS のオプションや委任を構成することはできません。 既存の DNS サーバー インフラストラクチャ内に新しいフォレスト ルート DNS ゾーンを作成するときは、 **[DNS 委任の作成]** を使用できます。 このオプションを使用すると、DNS ゾーンを更新する権限を持つ、代替の DNS 管理者資格情報を指定できます。  
  
DNS 委任を作成する必要があるかどうかの詳細については、「 [ゾーンの委任とは](https://technet.microsoft.com/library/cc771640.aspx)」を参照してください。  
  
#### <a name="additional-options"></a>追加オプション  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
**[追加オプション]** ページには、ドメインの NetBIOS 名が表示されます。この名前はオーバーライドできます。 既定では、NetBIOS ドメイン名は **[配置構成]** ページで指定された完全修飾ドメイン名の一番左のラベルに一致します。 たとえば、完全修飾ドメイン名として corp.contoso.com を指定した場合、既定の NetBIOS ドメイン名は CORP です。  
  
15 文字以下で、他の NetBIOS 名と競合していない名前は、変更されません。 他の NetBIOS 名と競合している場合は、番号が付加されます。 15 文字を超えている場合は、一意の、もっと短い名前の候補がウィザードによって示されます。 ウィザードでは、いずれの場合も、WINS 参照および NetBIOS ブロードキャストを介して、名前が既に使用されていないかどうかが最初に検証されます。  
  
有効なドメイン名の詳細については、サポート技術情報の記事「 [Naming conventions in Active Directory for computers, domains, sites, and OUs (Active Directory 内のコンピューター、ドメイン、サイト、および OU の名前付け規則)](https://support.microsoft.com/kb/909264)」を参照してください。  
  
#### <a name="paths"></a>パス  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
**[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所をオーバーライドできます。 既定の場所は常に、%systemroot% (つまり C:\Windows) のサブディレクトリ内です。  
  
#### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
**[オプションの確認]** ページでは、インストールを開始する前に、設定を確認し、それらが要件を満たしているかどうか確認することができます。 これがサーバー マネージャーの使用中においてインストールを中止する最後の機会ではありません。 構成を続行する前に設定を確認するためのオプションにすぎません。  
  
サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。 これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。 たとえば次のようになります。  
  
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
> サーバー マネージャーでは通常、昇格時にすべての引数とその値を入力し、既定値に依存しません (既定値は将来のバージョンの Windows 間またはサービス パック間で変わる可能性があるため)。 唯一の例外は **-safemodeadministratorpassword** 引数です (これはあえてスクリプトから除外されています)。 確認プロンプトを強制的に表示するには、コマンドレットを対話的に実行するときに値を省略します。  
  
#### <a name="prerequisites-check"></a>前提条件のチェック  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
**[前提条件のチェック]** は、AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバー構成が新しい AD DS フォレストをサポートできるかどうかを検証します。  
  
新しいフォレスト ルート ドメインをインストールするときは、サーバー マネージャーの Active Directory Domain Services 構成ウィザードによって、一連のモジュール テストが実施されます。 これらのテストでは、警告と共に、候補となる修正オプションが提示されます。 テストは必要なだけ何度でも実行できます。 前提条件のテストにすべて合格するまで、ドメイン コントローラー プロセスを続行することはできません。  
  
**[前提条件のチェック]** では、以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかになります。  
  
具体的な前提条件チェックの詳細については、「 [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)」を参照してください。  
  
#### <a name="installation"></a>インストール  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
**[インストール]** ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> 同じサーバー マネージャー コンソールから、役割インストールと AD DS 構成の複数のウィザードを同時に実行できます。  
  
#### <a name="results"></a>結果  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**[結果]** ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  
## <a name="BKMK_PSForest"></a>Windows PowerShell を使用してフォレストを展開する  
ここでは、コア Windows Server 2012 コンピューター上で、Windows PowerShell を使って最初のドメイン コントローラーをフォレスト ルート ドメインにインストールする方法について説明します。  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>Windows PowerShell を使った AD DS の役割のインストール プロセス  
いくつかの単純な ServerManager 展開コマンドレットを展開プロセスに組み込むことで、AD DS の簡素化された管理の構想をさらに実現できます。  
  
次の図は、Active Directory ドメイン サービスの役割のインストール プロセスを示しています。管理者が **PowerShell.exe** を実行するところから始まり、ドメイン コントローラーの昇格の直前で終わっています。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager コマンドレット|引数 (**太字** の引数は必須です。 *斜体* の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。)|  
|Install-WindowsFeature/Add-WindowsFeature|***-Name***<br /><br />*-再起動*<br /><br />*-IncludeAllSubFeature*<br /><br />*-IncludeManagementTools*<br /><br />-Source<br /><br />*-ComputerName*<br /><br />-Credential<br /><br />-LogPath<br /><br />*-Vhd*<br /><br />*-ConfigurationFilePath*|  
  
> [!NOTE]  
> 必須ではありませんが、AD DS の役割のバイナリをインストールするときは、引数 **-IncludeManagementTools** を指定することを強くお勧めします。  
  
ServerManager モジュールは、Windows PowerShell の新しい DISM モジュールによる役割インストール、状態、および削除の部分を公開します。 このレイヤリングによって、ほとんどのタスクが簡素化され、強力な (ただし、使い方を間違うと危険な) DISM モジュールを直接使用する必要が減ります。  
  
ServerManager 内のエイリアスとコマンドレットをエクスポートするには、 **Get-Command** を使用します。  
  
```powershell  
Get-Command -module ServerManager  
```  
  
たとえば次のようになります。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
Active Directory ドメイン サービスの役割を追加するには、AD DS の役割の名前を引数として指定して **Install-WindowsFeature** を実行するだけです。 サーバー マネージャーと同様、AD DS の役割に暗黙的に必要とされるすべてのサービスは自動的にインストールされます。  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
AD DS の管理ツールもインストールしたい場合は (強くお勧めします)、 **-IncludeManagementTools** 引数を指定します。  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
たとえば次のようになります。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
すべての機能と役割をそのインストール状態と共に一覧表示するには、 **Get-WindowsFeature** を引数なしで実行します。 リモート サーバーからインストール状態を確認する場合は、 **-ComputerName** 引数を指定します。  
  
```powershell  
Get-WindowsFeature  
```  
  
**Get-WindowsFeature** にはフィルター メカニズムがないため、特定の機能を検索するためには **Where-Object** とパイプラインを使用する必要があります。 パイプラインは複数のコマンドレット間でデータを渡すのに使うチャネルであり、Where-Object コマンドレットはフィルターとして機能します。 組み込みの **$_** 変数は、任意のプロパティと共にパイプラインに渡される現在のオブジェクトとして機能します。  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
たとえば、 **表示名** プロパティに "Active Dir" を含む機能をすべて検索するには、次のコマンドを使用します。  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
他の例も次に示します。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
パイプラインと Where-Object を使った他の Windows PowerShell 操作の詳細については、「 [Piping and the Pipeline in Windows PowerShell (Windows PowerShell のパイプ処理とパイプライン)](https://technet.microsoft.com/library/ee176927.aspx)」を参照してください。  
  
また、Windows PowerShell 3.0 では、このパイプライン操作に必要なコマンドライン引数が大幅に簡素化されています。 Windows PowerShell 2.0 では次のように指定する必要がありました。  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Windows PowerShell パイプラインを使用することで、判読しやすい結果が生成されます。 たとえば次のようになります。  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
**Select-Object** コマンドレットと **-expandproperty** 引数を組み合わせると、興味深い結果になります。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> **Select-Object -expandproperty** 引数を指定すると、全体的なインストール パフォーマンスが多少遅くなります。  
  
### <a name="BKMK_PS"></a>Windows PowerShell を使用して AD DS フォレストのルートドメインを作成する  
ADDSDeployment モジュールを使って新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```powershell  
Install-addsforest  
```  
  
**Install-AddsForest** コマンドレットのフェーズは 2 つだけです (前提条件のチェックおよびインストール)。 下記に示す 2 つの図は、最小限必要な **-domainname**引数を使用したインストール フェーズを示しています。  
  
|||  
|-|-|  
|ADDSDeployment コマンドレット|引数 (**太字** の引数は必須です。 *斜体* の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。)|  
|install-addsforest|-Confirm<br /><br />*-CreateDNSDelegation*<br /><br />*-DatabasePath*<br /><br />*-DomainMode*<br /><br />***-DomainName***<br /><br />***-DomainNetBIOSName***<br /><br />*-DNSDelegationCredential*<br /><br />*-ForestMode*<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-SafeModeAdministratorPassword*<br /><br />-SkipAutoConfigureDNS<br /><br />-SkipPreChecks<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-DomainNetBIOSName** 引数は、DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合と、名前が 15 文字を超えている場合に必須です。  
  
サーバー マネージャーの **[配置構成]** と同等の ADDSDeployment コマンドレットと引数を次に示します。  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
サーバー マネージャーの [ドメイン コントローラー オプション] と同等の ADDSDeployment コマンドレットと引数を次に示します。  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
**Install-ADDSForest** の引数は、指定しない場合、サーバー マネージャーと同じ既定値が続きます。  
  
**SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります。  
  
-   この引数を *指定しない* 場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。  
  
    たとえば、corp.contoso.com という名前の新しいフォレストを作成し、マスクされたパスワードの入力と確認入力を求めらるようにするには、次のように指定します。  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   この引数を *値と共に*指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。  
  
たとえば、 **Read-Host** コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> この方法ではパスワードの確認入力が行われないため、細心の注意が必要です。パスワードは表示されません。  
  
セキュリティで保護された文字列は、変換されるクリア テキストの変数として指定することもできますが、これはお勧めしません。  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
最後に、暗号化したパスワードをファイルに保存して後で使用することができます。こうするとクリア テキストのパスワードを表示せずに済みます。 たとえば次のようになります。  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> クリア テキストや暗号化されたテキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。 そのファイルにアクセスできる人はだれでも、暗号化されたパスワードを元に戻すことができます。 そのパスワードがわかれば、DSRM で起動された DC にログオンし、最終的にドメイン コントローラーそのものを偽装して、自分の権限を Active Directory フォレストで最も高いレベルに昇格させることができます。 テキスト ファイル データを暗号化するための **System.Security.Cryptography** の一連の使用手順を読むことが推奨されますが、ここでは取り上げません。 ベスト プラクティスは、パスワードの保存を絶対に避けることです。  
  
ADDSDeployment コマンドレットには、DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップする追加オプションがあります。 サーバー マネージャーを使用しているときは、この構成オプションをスキップできません。 この引数が重要なのは、ドメイン コントローラーを構成する前に DNS サーバーの役割をインストールした場合だけです。  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
**DomainNetBIOSName** 操作も特殊です。  
  
-   **DomainNetBIOSName** 引数が NetBIOS ドメイン名と共に指定されず、 **DomainName** 引数の単一ラベル プレフィックスのドメイン名が 15 文字以下の場合、昇格は自動的に生成される名前を使って続行されます。  
  
-   **DomainNetBIOSName** 引数が NetBIOS ドメイン名と共に指定されず、 **DomainName** 引数の単一ラベル プレフィックスのドメイン名が 16 文字以上の場合、昇格は失敗します。  
  
-   **DomainNetBIOSName** 引数が 15 文字以下の NetBIOS ドメイン名と共に指定された場合、昇格は指定された名前を使って続行されます。  
  
-   **DomainNetBIOSName** 引数が 16 文字以上の NetBIOS ドメイン名と共に指定された場合、昇格は失敗します。  
  
サーバー マネージャーの [追加オプション] と同等の ADDSDeployment コマンドレット引数を次に示します。  
  
```powershell  
-domainnetbiosname <string>  
```  
  
サーバー マネージャーの **[パス]** と同等の ADDSDeployment コマンドレット引数を次に示します。  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
構成情報を確認するには、 **Install-ADDSForest** コマンドレットと共にオプションの **Whatif** 引数を使用します。 これによって、コマンドレットの引数の明示的な値と暗黙的な値を確認できます。  
  
たとえば次のようになります。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
サーバー マネージャーを使用する場合は **[前提条件のチェック]** を省略することはできませんが、AD DS 展開コマンドレットと以下の引数を使用すると省略できます。  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> ただし Microsoft では前提条件のチェックを省略することはお勧めしません。ドメイン コントローラーの昇格が部分的に行われたり、AD DS フォレストに障害が発生したりする恐れがあります。  
  
サーバー マネージャーの場合とまったく同じように、 **Install-ADDSForest** でも、昇格によってサーバーが自動的に再起動されることが通知されます。  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![新しいフォレストをインストールする](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の終了時にサーバーが自動的に再起動されないようにするには、 **-norebootoncompletion** 引数を使用します。  
  
> [!WARNING]  
> 再起動のオーバーライドは推奨されません。 ドメイン コントローラーを正常に機能させるには、再起動する必要があります。  
  
## <a name="see-also"></a>関連項目  
[Active Directory Domain Services (TechNet ポータル)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Windows Server 2008 R2 の Active Directory Domain Services](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Windows Server 2008 向け Active Directory Domain Services](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Windows Server テクニカルリファレンス (Windows Server 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[Active Directory 管理センター: はじめに (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[Windows PowerShell を使用した Active Directory 管理 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[ディレクトリサービスチームに質問する (Microsoft の公式テクニカルサポートブログ)](https://blogs.technet.com/b/askds)  
  

