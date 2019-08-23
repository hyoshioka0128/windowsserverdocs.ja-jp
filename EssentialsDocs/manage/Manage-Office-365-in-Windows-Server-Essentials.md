---
title: Windows Server Essentials での Office 365 の管理
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: bd7787b853395bf461165802251de8b2be5d5a39
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980267"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials での Office 365 の管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials サーバーと Microsoft Office 365 を統合すると、Windows Server Essentials ダッシュボードから、Office 365 サービスとオンラインアカウントをオンプレミスのリソースと共に管理できます。 このトピックでは、サーバーと Office 365 を統合することによって得られるメリット、その方法、Office 365 統合の管理およびトラブルシューティングを行う方法について説明します。  
  
  
  
> [!IMPORTANT]
>   Office 365 統合は、単一ドメインコントローラー環境でのみサポートされています。 また、Office 365 統合ウィザードは、ドメインコントローラー上で実行する必要があります。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [Office 365 をサーバーと統合する必要があるのはなぜですか。](#BKMK_IntegrationOverview)  
  
-   [Office 365 統合のセットアップ](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 統合の管理](#BKMK_ManageIntegration)  
  
-   [Office 365 統合のトラブルシューティング](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a>Office 365 をサーバーと統合する必要があるのはなぜですか。  
 Office 365 を Windows Server Essentials サーバーと統合するには、さまざまな理由があります。 社内の一部のリソースを管理していても、他のサービスに Office 365 を使用している場合は、2か所ではなく、オンプレミスのリソースと共に、Office 365 のサービスとリソースをダッシュボードから管理することができます。  
  
- ユーザーアカウントと共に Office 365 へのアクセス権をユーザーに与えるオンラインアカウントを管理します。  
  
  -   ユーザー用の Microsoft Online Services アカウントを 1 つの手順で作成し、既存のオンライン アカウント用にサーバー上にユーザー アカウントを作成します。 新規または既存のユーザー アカウントにオンライン アカウントを追加することもできます。  
  
       ダッシュボードからオンラインアカウントを作成すると、ユーザーは、サーバーで使用しているのと同じパスワードを使用して Office 365 にサインインします。 ユーザーがユーザー アカウントのパスワードを変更した場合は、オンラインのパスワードも変わります。 ユーザー アカウントに対して設定したセキュリティ要件をオンライン アカウントのパスワードが常に満たしていることがわかります。  
  
  -   ユーザー アカウントのライフ サイクルを通して、ユーザー アカウントと共にオンライン アカウントを管理します。 ユーザー アカウントを無効にすると、オンライン アカウントも無効になります。 ユーザー アカウントを削除すると、オンライン アカウントも削除されます。  
  
  -   Windows Server Essentials サーバーでは、電子メールの Exchange Online 配布グループも管理します。  
  
- カスタムインターネットドメインを Office 365 サブスクリプションにリンクして、組織のインターネットドメイン (たとえば、contoso.com) から電子メールを送受信します。  
  
- ダッシュボードからサブスクリプションと Office 365 の統合を管理します。  
  
- サブスクリプションに SharePoint Online ライブラリが含まれている場合、Office 365 と Windows Server Essentials サーバーとの統合により、次のことが可能になります。  
  
  - ダッシュボードから SharePoint Online ライブラリを作成し、管理します。  
  
    > [!NOTE]
    >  また、My Server 2012 R2 アプリを使用して、ノート pc、モバイルデバイス、または Windows phone から SharePoint Online ライブラリ内のドキュメントを操作することもできます。 この機能は、Windows Server Essentials でのみ使用できます。 詳細については、「 [My Server アプリを使用する](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)」を参照してください。  
  
  - ダッシュボードから SharePoint Online チームサイトのアクセス許可を変更するか、ダッシュボードからチームサイトを開いて他の変更を行います。  
  
    詳細については、「 [SharePoint Online の管理](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)」を参照してください。  
  
- Exchange Online にサブスクライブする場合、Office 365 と Windows Server Essentials サーバーを統合することで、ユーザーが会社の電子メールサーバーへの接続に使用するモバイルデバイスを管理できるようになります。  
  
  -   モバイル デバイスが会社の電子メール サーバーに接続するときにパスワード保護を必要とします。 最小のパスワード長、サインインの許容失敗回数、およびサインイン試行の必須最小時間間隔を設定します。  
  
  -   デバイス モデルにセキュリティ上の問題があることがわかったら、Exchange Online へのそのモバイル デバイスの接続をブロックします。  
  
  -   モバイル デバイスの紛失または盗難発生の場合は、デバイスの電源が次にオンにされたときに、企業の機密データを削除するようにデバイスをワイプします。  
  
- Office 365 の統合により、Office 365 のサービスとリソースに接続するための新しい方法が提供されます。  
  
  -   Windows Server Essentials スタートパッドから Office 365 サービスを開きます。 詳細については、「 [Microsoft Office 365 を使用するクイックスタートガイド](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)」を参照してください。  
  
  -   My Server 2012 R2 アプリを使用して、ノート pc、モバイルデバイス、または Windows phone から SharePoint Online ライブラリ内のドキュメントを操作します。 詳細については、「 [My Server アプリを使用する](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)」を参照してください。 この機能は、Windows Server Essentials でのみ使用できます。  
  
##  <a name="BKMK_Configure"></a>Office 365 統合のセットアップ  
 サーバーのインストールが完了したら、いつでもサーバーを Office 365 と統合できます。 Office 365 サブスクリプションをお持ちでない場合は、購入するか、無料試用版サブスクリプションにサインアップすることができます。  
  
 次のタスクを行います。  
  
-   [ステップ 1: Office 365 の統合要件を確認する](#BKMK_StepOne_VERIFY)  
  
-   [手順 2:サーバーを Microsoft Office 365 と統合する](#BKMK_StepTwo)  
  
-   [手順 3:組織のインターネットドメイン名を Office 365 にリンクする (省略可能)](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a>手順 1:Office 365 の統合要件を確認する  
 開始する前に、サーバーが次の要件を満たしてされていることを確認します。  
  
-   サーバーは次のオペレーティング システムのいずれかを搭載しています。Windows server essentials、Windows Server Essentials、または windows server 2012 R2 Standard または windows server 2012 R2 Datacenter オペレーティングシステム (Windows Server Essentials Experience 役割がインストールされている場合)。  
  
-   環境で使用できるドメインコントローラーは1つだけであるため、ドメインコントローラーで Office 365 統合を実行する必要があります。  
  
-   サーバーからインターネットに接続できる必要があります。  
  
-   Office 365 統合を開始する前に、サーバーに重要な更新プログラムと重要な更新プログラムをすべてインストールする必要があります。  
  
-   組織のインターネットドメインを電子メールアドレスと SharePoint Online リソースで使用する場合は、統合時にドメインを Office 365 にリンクできるようにドメイン名を登録する必要があります。 詳細については、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。  
  
> [!NOTE]
>  Office 365 を事前にサブスクライブする必要はありません。 Office 365 統合中にサブスクリプションを購入するか、無料試用版にサインアップすることができます。 Office 365 のプランと価格については、「 [office 365 plan for 企業](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)」を参照してください。  
  
###  <a name="BKMK_StepTwo"></a>手順 2:サーバーを Microsoft Office 365 と統合する  
 Windows Server Essentials サーバーと Office 365 を統合するには、ドメインコントローラーで次の手順を実行します。  
  
> [!NOTE]
>  この手順は、Windows Server Essentials または Windows Server Essentials を使用している場合と同じですが、ホームページの別の場所から開始します。 Windows Server Essentials では、 **[サービス]** タブでサーバーと Office 365 およびその他の Microsoft オンラインサービスを統合します。Windows Server Essentials では、Office 365 統合は **[電子メール]** タブで実行されます。  
  
##### <a name="to-integrate-the-server-with-office-365"></a>サーバーと Office 365 を統合するには  
  
1. 管理者としてサーバーにサインインし、Windows Server Essentials ダッシュボードを開きます。  
  
2. **[ホーム]** ページで、 **[サービス]** (Windows Server Essentials の場合は **[電子メール]** ) をクリックし、 **[Microsoft Office 365 との統合]** をクリックして、 **[Microsoft Office 365 統合のセットアップ]** をクリックします。  
  
    Microsoft Office 365 との統合ウィザードが表示されます。  
  
3. **[はじめよう]** ページで、次の操作のいずれかを実行します。  
  
   -   Office 365 のサブスクリプションをお持ちでない場合は、 **[次へ]** をクリックし、指示に従って office 365 に登録するか、試用版サブスクリプションにサインアップしてください。  
  
        ウィザードに戻る前に、Office 365 にサインインする必要があります。 ただし、Office 365 ポータルの **[ここから開始]** セクションでタスクを実行する必要はありません。  
  
   -   サーバーと統合する Office 365 へのサブスクリプションを既に持っている場合は、 **[office 365 のサブスクリプションが既にある]** を選択し、 **[次へ]** をクリックします。  
  
4. 指示に従ってウィザードを完了します。  
  
   ウィザードが正常に完了すると、ダッシュボードに次のような変更が加えられます。  
  
-   新しい**office 365**ページがあります。これは、統合と office 365 サブスクリプションを管理するために使用されます。  
  
-   **[ユーザー]** ページに **[オンラインアカウント]** タブが表示されます。このタブでは、ユーザーが Office 365 にアクセスできるようにする Microsoft online Services アカウントを作成および管理できます。 Exchange Online を使用していて、Windows Server Essentials サーバーを持っている場合は、 **[配布グループ]** タブも表示されます。  
  
-   Windows Server Essentials サーバーの **[ストレージ]** ページには、sharepoint Online ライブラリを管理したり、チームサイトのアクセス許可を変更したりするための **[sharepoint ライブラリ]** タブがあります。 Office 365 のすべてのビジネスプランには、これらの基本的な SharePoint Online 機能が含まれています。  
  
###  <a name="BKMK_StepThree"></a>手順 3:組織のインターネットドメイン名を Office 365 にリンクする (省略可能)  
 組織宛ての電子メールと SharePoint Online リソースの Url で独自のインターネットドメインを使用する場合は、カスタムドメインを Office 365 サブスクリプションにリンクすることができます。 Windows Server Essentials サーバーを Office 365 と統合する場合は、ダッシュボードからこの操作を行うことができます。  
  
 これは、オンラインアカウントを一括作成するときにドメインを使用できるように、ユーザーのオンラインアカウントを作成する前に実行するのが最も簡単です。  
  
 Office 365 にサインアップすると、ドメイン名が取得されます。たとえば、onmicrosoft.com のようになります。 別のドメイン名を使用する場合は、簡単に contoso.com ことができます。 ドメイン名をまだ所有していない場合は購入し、DNS レコードの一部を変更する必要があります。  
  
 Office 365 で使用するカスタムドメインのセットアップには、次の4つのタスクが含まれます。  
  
1. **ドメイン名を購入します。** つまり、ドメイン名をドメイン レジストラーまたは DNS ホスティング プロバイダーに登録します。  
  
   -   Office 365 で動作するドメイン名を選択します。 第2レベルのドメイン名を使用できますか。たとえば、buycontoso.com? ではなく、3番目のレベルのドメイン名は使用できません。たとえば、marketing.contoso.com のように指定します。 Office 365 で使用するドメインの選択の詳細については、「 [Domains](https://technet.microsoft.com/library/office-365-domains.aspx)」を参照してください。  
  
   -   Office 365 で必要なドメインネームサーバー (DNS) レコードを許可するドメインレジストラーから購入します。 どのドメイン レジストラーが、必要な DNS レコードを許可しているかを調べるには、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。 ドメインを別のレジストラーに既に登録している場合は、心配しないでください。ドメインを Office 365 にリンクするときに、ドメインを別のレジストラーに転送できます。  
  
2. **Office 365 サービスにドメイン名の使用を許可する DNS レコードを構成します。** 最も簡単な方法は、手順 3. で Office 365 サブスクリプションにドメインをリンクするときに、ウィザードで DNS レコードを構成することです。 自分で実行する場合は、「 [Office 365 統合の DNS レコードを手動で構成する方法](#BKMK_ManuallyConfigureDNS)」を参照してください。  
  
3. **カスタムインターネットドメインを Office 365 サブスクリプションにリンクします。** 「**ドメインを Office 365 にリンク**する」アクションを使用します。  
  
4. **Office 365 サービスが新しいドメイン名を使用していることを確認します。**  
  
   "**ドメインを office 365 にリンク**する" タスクを使用する前に手順 1. と手順 2. を完了すると、ウィザードによってドメイン名が office 365 にリンクされます。 あるいは、手順 1 および手順 2 の一部または全部をウィザードを使用して実行することもできます。  
  
##### <a name="to-link-your-organizations-internet-domain-to-office-365"></a>組織のインターネットドメインを Office 365 にリンクするには  
  
1.  ダッシュボードで、 **[Office 365]** ページを開き、 **[ドメインを Office 365 にリンクする]** をクリックします。  
  
2.  指示に従ってウィザードを完了します。  
  
     このウィザードでは、Office 365 で使用する新規または既存のインターネットドメイン名を登録、構成、およびリンクする手順の一部またはすべてについて説明します。  
  
     タスクを完了するために必要な情報を取得するには、ウィザード ページで [ヘルプ] リンクをクリックします。 または、プロセスの概要と要件については、「 [Windows Server Essentials でのリモート Web アクセスの管理](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx)」の「ドメイン名のセットアップ」セクションを参照してください。  
  
    > [!NOTE]
    >  ウィザードを使用して新しいドメイン名を登録するには、ウィザードとのシームレスな統合を提供するために Microsoft と提携しているドメイン名サービス プロバイダーのいずれかを使用する必要があります。 ドメイン名レジストラ－を見つけるには、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。  
  
3.  ドメイン名がサーバーで管理されていないことがウィザードによって検出された場合は、構成を完了するために必要な DNS レコードを手動で構成する必要があります。 手順については、後述の「 [Office 365 統合の DNS レコードを手動で構成する方法](#BKMK_ManuallyConfigureDNS)」を参照してください。  
  
4.  ドメインが Office 365 で使用されていることを確認します。  
  
     ウィザードが完了した後、ドメイン名レジストラーによって DNS レコードが検証されるまで、少し待機します。 これは自動的に行われます。何もする必要はありません。 しかし、通常は1時間ほどかかります。 ドメインの検証が完了すると、 **Office 365**ページに組織のドメインが一覧表示されます。  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a>Office 365 統合の DNS レコードを手動で構成する方法  
 ドメイン名がサーバーによって管理されていないことを [ドメインを Office 365 にリンクする] ウィザードが検出した場合に、構成を完了するには、必要なドメイン ネーム サーバー (DNS) レコードを手動で構成する必要があります。 その場合は、 **%username%\NewDNSRecords_ (n) .txt**で構成する必要がある DNS レコードの一覧があります。ここで *(n)* はランダムな数値です。  
  
 次の表は、追加する必要がある DNS レコードを説明します。 入力方法は、ドメイン名レジストラーによって異なります。 不明な点がある場合は、ドメイン名のレジストラーにお問い合わせください。  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>カスタム インターネット ドメイン名を Office 365 にリンクするために必要な DNS レコード  
  
|サービス|必要な DNS レコード|目的|  
|-------------|--------------------------|-------------|  
|(複数のサービス)|MX| Office 365 では、このレコードを使用して、特定のドメイン名を所有していることを確認します。 この MX レコードは、電子メール メッセージのルーティングには影響しません。|  
|Exchange Online|MX|電子メール メッセージのルーティングを実現します。 **重要:** 電子メールを移行する場合は、優先順位ゼロ (**0**) を新しい MX レコードに割り当てないでください。 レコードの値が現在の MX レコードに割り当てられている値より大きいことを確認してください。 電子メールの移行が完了し、電子メールサーバーを Office 365 に変更する準備ができたら、ドメイン名レジストラーに新しい MX レコードの優先順位の値をリセットさせます。|  
|Exchange Online|エイリアス (CNAME)|ユーザーが Exchange Online と Outlook デスクトップ クライアントまたはモバイル電子メール クライアントとの接続を容易にセットアップできるように支援するための自動検出レコード。 **注:** 組織独自のドメイン名 ( http://mail.contoso.com) https://outlook.com/owa/office365.com) など) を使用して Outlook Web アクセスにアクセスする場合は、次のようにエイリアス (CName) レコードを構成できます。**種類 = CNAME、TTL = 01:00:00、HostName = mail、Address = mail. office365. com**|  
|Exchange Online|TXT|Office 365 電子メールサーバーによって使用されるドメイン outlook.com が、ドメインの代わりに電子メールを送信する権限を持っていることを指定します。 このレコードを作成すれば、送信電子メールがスパムとしてフラグ付けされるのを容易に防ぐことができます。|  
|Lync Online|SRV|Windows Live や Yahoo! などのその他のインスタント メッセージング サービスでフェデレーションを有効にするのに役立ちます。|  
|Lync Online|SRV|ユーザーが Lync デスクトップ クライアントと Microsoft Lync Online の間の接続を簡単にセットアップできるように支援するための自動検出レコード。|  
  
> [!IMPORTANT]
>  ドメインの確認が完了したら、Office 365 ポータルから DNS レコードを追加したり、その他の変更を加えたりしないでください。  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a>次のステップ  
  
-   ユーザー用の Microsoft Online Services アカウントを作成します。  
  
     Office 365 サービスを使用するには、ユーザーがネットワークユーザーアカウントに関連付けられている Microsoft Online Services アカウントを持っている必要があります。 ダッシュボードは、これを容易にします。 新しい Office 365 サブスクリプションを使用している場合は、既存のユーザーアカウントのオンラインアカウントを一括作成できます。 既に使用している Office 365 サブスクリプションと新しいサーバーを統合している場合は、既存のオンラインアカウントからユーザーアカウントをインポートできます。 手順については、「[ユーザーのオンラインアカウントを管理する](Manage-Online-Accounts-for-Users.md)」を参照してください。  
  
> [!NOTE]
>  Windows Server Essentials のダッシュボードでは、Microsoft Online Services アカウントは Office 365 アカウントと呼ばれます。 アカウントは同じで、用語だけが変更されています。  
  
##  <a name="BKMK_ManageIntegration"></a>Office 365 統合の管理  
 サーバーを Office 365 と統合すると、ダッシュボードの **[office 365]** ページに office 365 サブスクリプションに関する情報が表示され、これらのタスクが使用できるようになります。  
  
-   [Office 365 サブスクリプションを管理し](#BKMK_ManageO365)ますか?サブスクリプションの管理に使用する管理者アカウントを変更します。 Office 365 管理ダッシュボードを開いて、サブスクリプションを管理します。  
  
-   [組織のインターネットドメインを Office 365 にリンク](#BKMK_StepThree)しますか?自分のドメイン宛ての電子メールを送受信できるようにするには、ドメインを Office 365 にリンクします。 (前述の「 [手順 3:組織のドメインを Office 365](#BKMK_StepThree)にリンクします。)  
  
-   [Office 365 統合を無効に](#BKMK_Disable)しますか?Office 365 サービス、サブスクリプション、およびオンラインアカウントをダッシュボードから管理しない場合は、Office 365 統合を無効にすることができます。 これらのサービスは、Office 365 ポータルで引き続き利用できます。  
  
###  <a name="BKMK_ManageO365"></a>Office 365 サブスクリプションを管理する  
 サーバーでの作業中に Office 365 サブスクリプションに変更を加える必要がある場合は、ダッシュボードの **[office 365]** ページから office 365 のサブスクリプションを開くことができます。 また、サーバーが Office 365 サービスに変更を加えるときに使用する管理者アカウントを変更することもできます。  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 の管理ダッシュボードでサブスクリプションを開くには  
  
1.  Windows Server Essentials ダッシュボードで、 **[Office 365]** ページを開きます。  
  
2.  **[構成タスク]** で、 **[Office 365 を管理する]** をクリックします。  
  
3.  サブスクリプションの管理に使用する Microsoft オンラインアカウントで Office 365 にサインインします。  
  
     Office 365 管理ダッシュボードが開きます。  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 の管理者アカウントを変更するには  
  
1.  ダッシュボードで、 **[Office 365]** をクリックします。  
  
2.  **[構成タスク]** で、 **[Office 365 管理者アカウントを変更する]** をクリックします。 管理者アカウントの変更ウィザードが表示されます (Windows Server Essentials では、ウィザードの名前は Office 365 管理者アカウントに設定されています)。  
  
3.  Office 365 サブスクリプションへの接続に使用するアカウントの資格情報を入力し、 **[次へ]** をクリックします。  
  
4.  **[閉じる]** をクリックします。 ダッシュボードが再起動します。  
  
###  <a name="BKMK_Disable"></a>Office 365 統合を無効にする  
 Office 365 サービスとオンラインアカウントをダッシュボードから管理しない場合は、Office 365 の統合を無効にすることができます。 Office 365 サブスクリプションはアクティブなままで、ダッシュボードから行った構成の変更は引き続き有効です。 たとえば、Office 365 サブスクリプションにリンクしたドメイン名に対応する電子メールを受信します。 すべての電子メールが失われることはなく、モバイルデバイス用に設定したコントロールは引き続き Exchange Online で使用されます。  
  
 今後は、office 365 のサブスクリプション、サービス、およびリソースを Office 365 で管理します。ユーザーは、Office 365 でオンラインアカウントのパスワードを管理する必要があります。 パスワード同期は行われなくなり、ユーザーアカウントを無効にしたり削除したりしても、ユーザーのオンラインアカウントに影響はありません。  
  
 Office 365 統合ソフトウェアはローカルサーバーにインストールされているため、統合サービスが Office 365 に接続できない場合でも、この機能を無効にすることができます。  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>サーバーと Office 365 の統合を無効にするには  
  
1.  ダッシュボードで、 **[Office 365]** をクリックします。  
  
2.  **[Office 365 統合を無効にする]** をクリックします。 [Office 365 を無効にする] ウィザードが表示されます。  
  
3.  指示に従ってウィザードを完了します。  
  
> [!NOTE]
>  Office 365 統合を再び有効にするには、ダッシュボードの**ホーム**ページの **[サービス]** タブにある **[office 365 との統合]** タスクを使用します。 手順について[は、「手順 2:このトピックの前半の「Windows server Essentials](#BKMK_StepTwo)サーバーと Microsoft Office 365 を統合する」を参照してください。  
  
##  <a name="BKMK_Troubleshoot"></a>Office 365 統合のトラブルシューティング  
 このセクションでは、Windows Server Essentials の Office 365 統合機能を使用するときに発生する可能性のある一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
###  <a name="BKMK_AcctsNotCreated"></a>一部の Microsoft Online Services アカウントが作成されませんでした  
 **[説明]**  
  
 ダッシュボードから1つ以上の Microsoft Online Services アカウントを作成できませんでした。  
  
 **ソリューション**  
  
1.  ウィザードの完了ページにあるリンクをクリックして、正常終了しなかった各アカウント作成要求に関する詳細な情報が含まれる結果ファイルを開きます。 たとえば、要求したアカウント名を持つ Microsoft Online Services アカウントが既に存在するという結果が示される場合があります。  
  
2.  推奨される操作に従って、各エラーを解決します。  
  
3.  この問題が解決しない場合は、サーバーを再起動して、オンライン アカウントの作成を再度試みます。  
  
###  <a name="BKMK_ProblemUninstalling"></a>Office 365 統合のアンインストールで問題が発生しました  
 **[説明]**  
  
 Office 365 統合を無効にしようとしたときに不明なエラーが発生しました。  
  
 **ソリューション**  
  
1.  コンピューターがインターネットに接続されていることを確認してから、再試行してください。  
  
2.  エラーが再び発生する場合は、サーバーを再起動し、もう一度試してください。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials のサービス統合の概要-パート1](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials のサービス統合の概要-パート2](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Microsoft Office 365 を使用するクイックスタートガイド](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services の管理](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)
