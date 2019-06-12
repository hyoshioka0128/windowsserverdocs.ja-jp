---
title: Windows Server Essentials での Office 365 の管理
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
0author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d897c9186ff74a80d531cf84961709de54459f82
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433280"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials での Office 365 の管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Microsoft Office 365 と Windows Server Essentials サーバーを統合する場合に、Windows Server Essentials ダッシュ ボードから、オンプレミスのリソースと一緒に、Office 365 サービスおよびオンライン アカウントを管理できます。 このトピックでは、できる、サーバーに Office 365 を統合することで、これを行う方法、および管理し、Office 365 統合のトラブルシューティングを行う方法を見つかります。  
  
  
  
> [!IMPORTANT]
>   Office 365 統合は、1 つのドメイン コント ローラー環境でのみサポートされます。 さらに、Office 365 の統合ウィザードは、ドメイン コント ローラーで実行する必要があります。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [Office 365 をマイ サーバーと統合する必要があります。](#BKMK_IntegrationOverview)  
  
-   [Office 365 統合をセットアップします。](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 統合を管理します。](#BKMK_ManageIntegration)  
  
-   [Office 365 統合をトラブルシューティングします。](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a> Office 365 をマイ サーバーと統合する必要があります。  
 Office 365、Windows Server Essentials サーバーと統合する理由はたくさんあります。 一部は社内リソースの管理、Office 365 を使用して、その他のサービスの場合は、ダッシュ ボードで、2 つの場所での作業ではなく、オンプレミスのリソースと一緒に、Office 365 サービスとリソースを管理することができます。  
  
- ユーザー アカウントと共に、Office 365 へのユーザー アクセス権を付与するオンライン アカウントを管理します。  
  
  -   ユーザー用の Microsoft Online Services アカウントを 1 つの手順で作成し、既存のオンライン アカウント用にサーバー上にユーザー アカウントを作成します。 新規または既存のユーザー アカウントにオンライン アカウントを追加することもできます。  
  
       ダッシュ ボードからオンライン アカウントを作成するときにユーザーにサインインする Office 365、サーバーで使用される同じパスワードを使用します。 ユーザーがユーザー アカウントのパスワードを変更した場合は、オンラインのパスワードも変わります。 ユーザー アカウントに対して設定したセキュリティ要件をオンライン アカウントのパスワードが常に満たしていることがわかります。  
  
  -   ユーザー アカウントのライフ サイクルを通して、ユーザー アカウントと共にオンライン アカウントを管理します。 ユーザー アカウントを無効にすると、オンライン アカウントも無効になります。 ユーザー アカウントを削除すると、オンライン アカウントも削除されます。  
  
  -   Windows Server Essentials サーバーにも電子メールの Exchange Online 配布グループを管理します。  
  
- カスタム インターネット ドメインを Office 365 サブスクリプションにリンクすることによって、組織のインターネット ドメイン (contoso.com など) から電子メールを送受信します。  
  
- ダッシュ ボードから、お客様のサブスクリプションと Office 365 統合を管理します。  
  
- サブスクリプションには、SharePoint Online ライブラリが含まれている場合、Windows Server Essentials サーバーと Office 365 の統合では、することができます。  
  
  - 作成し、ダッシュ ボードから、SharePoint Online ライブラリを管理します。  
  
    > [!NOTE]
    >  My Server 2012 R2 アプリを使用して、ラップトップ、モバイル デバイス、または Windows Phone から SharePoint Online ライブラリ内のドキュメントを操作することがあります。 この機能では、Windows Server Essentials の使用のみです。 詳細については、次を参照してください。 [My Server アプリを使用して、](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)します。  
  
  - ダッシュ ボードで、SharePoint Online チーム サイトのアクセス許可を変更するか、変更を加える他のダッシュ ボードから、チーム サイトを開きます。  
  
    詳細については、次を参照してください。 [SharePoint Online の管理](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)します。  
  
- Exchange Online にサブスクライブする場合、Windows Server Essentials サーバーと Office 365 の統合では、ユーザーが会社の電子メール サーバーへの接続に使用するモバイル デバイスを管理することができます。  
  
  -   モバイル デバイスが会社の電子メール サーバーに接続するときにパスワード保護を必要とします。 最小のパスワード長、サインインの許容失敗回数、およびサインイン試行の必須最小時間間隔を設定します。  
  
  -   デバイス モデルにセキュリティ上の問題があることがわかったら、Exchange Online へのそのモバイル デバイスの接続をブロックします。  
  
  -   モバイル デバイスの紛失または盗難発生の場合は、デバイスの電源が次にオンにされたときに、企業の機密データを削除するようにデバイスをワイプします。  
  
- Office 365 統合では、Office 365 サービスおよびリソースに接続する新しい方法を示します。  
  
  -   Windows Server Essentials スタート パッドから Office 365 サービスを開きます。 詳しくは、次を参照してください。 [Quick Start Guide to Using Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)します。  
  
  -   My Server 2012 R2 アプリを使用して、ラップトップ、モバイル デバイス、または Windows Phone から SharePoint Online ライブラリ内のドキュメントを操作します。 詳しくは、次を参照してください。 [My Server アプリを使用して、](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)します。 この機能は、Windows Server Essentials で使用可能なだけです。  
  
##  <a name="BKMK_Configure"></a> Office 365 統合をセットアップします。  
 サーバーは、サーバーのインストールの完了後、いつでも Office 365 と統合できます。 Office 365 サブスクリプションがまだしていない場合は、いずれかを購入または無料試用版サブスクリプションにサインアップできます。  
  
 次のタスクを行います。  
  
-   [ステップ 1: Office 365 統合要件を確認します。](#BKMK_StepOne_VERIFY)  
  
-   [手順 2:Microsoft Office 365 とサーバーを統合します。](#BKMK_StepTwo)  
  
-   [手順 3:組織のインターネット ドメイン名を Office 365 (省略可能) にリンクします。](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a> 手順 1:Office 365 統合要件を確認します。  
 開始する前に、サーバーが次の要件を満たしてされていることを確認します。  
  
-   サーバーは次のオペレーティング システムのいずれかを搭載しています。Windows Server Essentials、Windows Server Essentials、または Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter オペレーティング システム。  
  
-   環境は 1 つのドメイン コント ローラー、しかし、ドメイン コント ローラーで Office 365 統合を実行する必要があります。  
  
-   サーバーからインターネットに接続できる必要があります。  
  
-   Office 365 統合を開始する前に、すべての重大かつ重要な更新プログラムをサーバーにインストールする必要があります。  
  
-   組織のインターネット ドメイン、SharePoint Online のリソースを使用して電子メール アドレスで使用する場合は、統合時に、ドメインを Office 365 にリンクできるようにドメイン名を登録する必要があります。 詳細については、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。  
  
> [!NOTE]
>  Office 365 を事前にサブスクライブする必要はありません。 サブスクリプションの購入または Office 365 統合中に無料試用版にサインアップすることができます。 プランと、Office 365 の価格について見てしたい場合[企業向け Office 365 プランの比較](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)します。  
  
###  <a name="BKMK_StepTwo"></a> 手順 2:Microsoft Office 365 とサーバーを統合します。  
 Office 365 と Windows Server Essentials サーバーを統合するドメイン コント ローラーで、次の手順を実行します。  
  
> [!NOTE]
>  プロシージャは Windows Server Essentials または Windows Server Essentials があるが、ホーム ページで別の場所から開始するかどうかと同じです。 Windows Server Essentials で Office 365 やその他の Microsoft Online Services でサーバーを統合する、**サービス**タブ。Windows Server Essentials で Office 365 統合を実行、**電子メール**タブ。  
  
##### <a name="to-integrate-the-server-with-office-365"></a>サーバーと Office 365 を統合するには  
  
1. 管理者は、サーバーにサインインし、Windows Server Essentials ダッシュ ボードを開きます。  
  
2. **ホーム**] ページで [**サービス**(in Windows Server Essentials では、次のようにクリックします**電子メール**)、[] をクリック**Microsoft Office 365 との統合**、。クリックして**Microsoft Office 365 統合のセットアップ**します。  
  
    Microsoft Office 365 との統合ウィザードが表示されます。  
  
3. **[はじめよう]** ページで、次の操作のいずれかを実行します。  
  
   -   Office 365 のサブスクリプションを持っていない場合はクリックして**次**、試用版サブスクリプションを Office 365 または記号をサブスクライブする指示に従います。  
  
        ウィザードに戻る前に、Office 365 にサインインする必要があります。 内のタスクを実行する必要はありませんが、**ここから始めて**Office 365 ポータルのセクション。  
  
   -   サーバーと統合する Office 365 のサブスクリプションが既にある場合**for Office 365 サブスクリプションが既にあるは**、順にクリックします**次**します。  
  
4. 指示に従ってウィザードを完了します。  
  
   ウィザードが正常に完了した後、ダッシュ ボードには、次の変更がわかります。  
  
-   新しい**Office 365**  ページで、統合、および Office 365 サブスクリプションを管理するために使用します。  
  
-   **ユーザー**ページの表示、**オンライン アカウント** タブを作成し、ユーザーに Office 365 へのアクセスを提供する Microsoft Online Services アカウントを管理します。 Exchange Online を使用して Windows Server Essentials サーバーが存在していてもわかります、**配布グループ**タブ。  
  
-   **ストレージ**Windows Server Essentials サーバー上のページが、 **SharePoint ライブラリ**SharePoint Online ライブラリを管理すると、チーム サイトのアクセス許可の変更 タブ。 Office 365 のすべてのビジネス プランには、これらの基本的な SharePoint Online 機能が含まれています。  
  
###  <a name="BKMK_StepThree"></a> 手順 3:組織のインターネット ドメイン名を Office 365 (省略可能) にリンクします。  
 独自のインターネット ドメイン、組織と、SharePoint Online のリソースの Url 宛ての電子メールを使用する場合は、Office 365 サブスクリプションにカスタム ドメインをリンクできます。 Office 365、Windows Server Essentials サーバーを統合する場合は、ダッシュ ボードからこれを実行できます。  
  
 作成するときに一括でオンライン アカウントにドメインを使用できるように、ユーザーのオンライン アカウントを作成する前に行う最も簡単になります。  
  
 Office 365 にサインアップするときに、ドメイン名を取得するでしょうか。 たとえば、 *contoso*。 onmicrosoft.com です。 別のドメイン名が使用する場合はでしょうか。 たとえば、単に contoso.com でしょうか。 ことができます。 既に 1 つは、自分が所有し、DNS レコードの一部を変更しない場合は、ドメイン名を購入する必要があります。  
  
 Office 365 で使用するカスタム ドメインの設定には、4 つのタスクが含まれます。  
  
1. **ドメイン名を購入します。** つまり、ドメイン名をドメイン レジストラーまたは DNS ホスティング プロバイダーに登録します。  
  
   -   Office 365 と連携するドメイン名を選択します。 第 2 レベル ドメイン名を使用することができますか? たとえば、buycontoso.com でしょうか。 第 3 レベル ドメイン名ではありませんが、でしょうか。 たとえば、marketing.contoso.com。 Office 365 で使用するドメインの選択方法の詳細については、次を参照してください。[ドメイン](https://technet.microsoft.com/library/office-365-domains.aspx)します。  
  
   -   Office 365 で必要なドメイン ネーム サーバー (DNS) レコードを許可するドメイン レジストラーからドメインを購入します。 どのドメイン レジストラーが、必要な DNS レコードを許可しているかを調べるには、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。 異なるレジストラーに既に自分のドメインが登録されている場合は心配しないでください。ドメインを Office 365 にリンクする場合は、異なるレジストラーにドメインを転送できます。  
  
2. **Office 365 サービスにドメイン名の使用を許可する DNS レコードを構成します。** 最も簡単な方法では、手順 3. での Office 365 サブスクリプションにドメインをリンクするの DNS レコードを構成するウィザードを使用します。 場合ではなく行うのと自分を参照してください。 [Office 365 統合のレコードを手動で DNS を構成する方法](#BKMK_ManuallyConfigureDNS)します。  
  
3. **カスタム インターネット ドメインを Office 365 サブスクリプションにリンクします。** 使用して、**ドメイン Office 365 にリンクする**アクション。  
  
4. **Office 365 サービスが新しいドメイン名を使用していることを確認します。**  
  
   使用する前に、手順 1. および 2. を完了するかどうか、**ドメイン Office 365 にリンクする**タスクでは、ウィザードが、ドメイン名を Office 365 にリンクできます。 あるいは、手順 1 および手順 2 の一部または全部をウィザードを使用して実行することもできます。  
  
##### <a name="to-link-your-organizations-internet-domain-to-office-365"></a>Office 365 に組織のインターネット ドメインをリンクするには  
  
1.  ダッシュボードで、 **[Office 365]** ページを開き、 **[ドメインを Office 365 にリンクする]** をクリックします。  
  
2.  指示に従ってウィザードを完了します。  
  
     ウィザードは、登録、構成、および Office 365 で使用する新規または既存インターネット ドメイン名をリンクする手順の一部またはすべてのヘルプします。  
  
     タスクを完了するために必要な情報を取得するには、ウィザード ページで [ヘルプ] リンクをクリックします。 セットアップのドメイン名のセクションを参照してください。 または[Windows Server Essentials でのリモート Web アクセスの管理](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx)、プロセスの概要と要件。  
  
    > [!NOTE]
    >  ウィザードを使用して新しいドメイン名を登録するには、ウィザードとのシームレスな統合を提供するために Microsoft と提携しているドメイン名サービス プロバイダーのいずれかを使用する必要があります。 ドメイン名レジストラ－を見つけるには、「 [ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)」を参照してください。  
  
3.  ウィザードが、ドメイン名がサーバーによって管理されていないことを検出した場合は、構成を完了に必要な DNS レコードを手動で構成する必要があります。 手順については、後述の「 [Office 365 統合の DNS レコードを手動で構成する方法](#BKMK_ManuallyConfigureDNS)」を参照してください。  
  
4.  ドメインを Office 365 で使用されていることを確認します。  
  
     少し待機しているドメイン名レジストラーで DNS レコードを検証中に、ウィザードの完了後します。 自動的に。何もする必要はありません。 通常約 1 時間かかることが、ですか? とやや長い時間場合があります。 ドメインの確認が完了すると、 **Office 365**ページは、組織のドメインを一覧表示されます。  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a> Office 365 統合の DNS レコードを手動で構成する方法  
 ドメイン名がサーバーによって管理されていないことを [ドメインを Office 365 にリンクする] ウィザードが検出した場合に、構成を完了するには、必要なドメイン ネーム サーバー (DNS) レコードを手動で構成する必要があります。 その場合で構成する必要がある DNS レコードの一覧を検索します **%username%\NewDNSRecords_ (n) .txt**ここで、 *(n)* はランダムな番号です。  
  
 次の表は、追加する必要がある DNS レコードを説明します。 入力方法は、ドメイン名レジストラーによって異なります。 不明な点がある場合は、ドメイン名のレジストラーにお問い合わせください。  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>カスタム インターネット ドメイン名を Office 365 にリンクするために必要な DNS レコード  
  
|サービス|必要な DNS レコード|目的|  
|-------------|--------------------------|-------------|  
|(複数のサービス)|MX| Office 365 では、このレコードを使用して、特定のドメイン名を所有していることを確認します。 この MX レコードは、電子メール メッセージのルーティングには影響しません。|  
|Exchange Online|MX|電子メール メッセージのルーティングを実現します。 **重要:** 電子メールを移行する場合は、優先順位ゼロ (**0**) を新しい MX レコードに割り当てないでください。 レコードの値が現在の MX レコードに割り当てられている値より大きいことを確認してください。 電子メールの移行が完了し、Office 365 にメール サーバーを変更する準備が完了したら、新しい MX レコードの優先順位の値をリセット、ドメイン名レジストラーがあります。|  
|Exchange Online|エイリアス (CNAME)|ユーザーが Exchange Online と Outlook デスクトップ クライアントまたはモバイル電子メール クライアントとの接続を容易にセットアップできるように支援するための自動検出レコード。 **注:** 組織のドメイン名を使用して Outlook Web Access にアクセスする場合 (たとえば、 http://mail.contoso.com)標準的な URL ではなく (https://outlook.com/owa/office365.com)エイリアス (CName) レコードを次のように構成することができます。**型 CNAME、TTL を = = 01: 00:00、ホスト名 = メール、Address=mail.office365.com**|  
|Exchange Online|TXT|その outlook.com、Office 365 の電子メール サーバーによって使用されるドメインは、ドメインの代わりに電子メールを送信する権限を指定します。 このレコードを作成すれば、送信電子メールがスパムとしてフラグ付けされるのを容易に防ぐことができます。|  
|Lync Online|SRV|Windows Live や Yahoo! などのその他のインスタント メッセージング サービスでフェデレーションを有効にするのに役立ちます。|  
|Lync Online|SRV|ユーザーが Lync デスクトップ クライアントと Microsoft Lync Online の間の接続を簡単にセットアップできるように支援するための自動検出レコード。|  
  
> [!IMPORTANT]
>  ドメインの後に検証が完了したら、追加、または Office 365 ポータルから、DNS レコードにさらに変更を加えるしないでください。  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a> 次の手順  
  
-   ユーザー用の Microsoft Online Services アカウントを作成します。  
  
     Office 365 サービスを使用するには、ユーザーは、ネットワーク ユーザー アカウントに関連付けられている Microsoft Online Services アカウントをいる必要があります。 ダッシュボードは、これを容易にします。 新しい Office 365 サブスクリプションを使用している場合は一括作成できますオンライン アカウントの既存のユーザー アカウント。 新しいサーバーを使用している Office 365 サブスクリプションに統合する場合は、既存のオンライン アカウントからユーザー アカウントをインポートできます。 手順については、次を参照してください。[ユーザーのオンライン アカウントの管理](Manage-Online-Accounts-for-Users.md)します。  
  
> [!NOTE]
>  Windows Server essentials ダッシュ ボードでは、Microsoft Online Services アカウントを Office 365 アカウントと呼びます。 アカウントは同じで、用語だけが変更されています。  
  
##  <a name="BKMK_ManageIntegration"></a> Office 365 統合を管理します。  
 Office 365 とサーバーを統合すると、 **Office 365**ダッシュ ボードのページは、Office 365 サブスクリプションの情報が表示され、これらのタスクを使用できるようになります。  
  
-   [Office 365 サブスクリプションの管理](#BKMK_ManageO365)でしょうか。サブスクリプションの管理に使用する管理者アカウントを変更します。 サブスクリプションの管理に Office 365 管理者ダッシュ ボードを開きます。  
  
-   [Office 365 に組織のインターネット ドメインをリンク](#BKMK_StepThree)でしょうか。独自のドメイン宛ての電子メールの送受信を行うことができる場合は、Office 365 にドメインをリンクできます。 (以前で説明した[手順 3。Office 365 組織のドメインをリンク](#BKMK_StepThree))。  
  
-   [Office 365 統合を無効にする](#BKMK_Disable)でしょうか。ダッシュ ボードから、Office 365 サービス、サブスクリプション、およびオンライン アカウントを管理しない場合は、Office 365 統合を無効にすることができます。 サービスは、Office 365 ポータルで引き続き使用できます。  
  
###  <a name="BKMK_ManageO365"></a> Office 365 サブスクリプションを管理します。  
 サーバー上の作業中に、Office 365 サブスクリプションに変更を加える必要がありますから Office 365 でサブスクリプションを開くことができます、 **Office 365**ダッシュ ボードのページ。 Office 365 サービスを変更するサーバーが使用する管理者アカウントを変更することもできます。  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 の管理ダッシュボードでサブスクリプションを開くには  
  
1.  Windows Server Essentials ダッシュ ボードで、開く、 **Office 365**ページ。  
  
2.  **[構成タスク]** で、 **[Office 365 を管理する]** をクリックします。  
  
3.  使用して、サブスクリプションを管理する Microsoft オンライン アカウントで Office 365 にサインインします。  
  
     Office 365 の管理ダッシュ ボードを開きます。  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 の管理者アカウントを変更するには  
  
1.  ダッシュボードで、 **[Office 365]** をクリックします。  
  
2.  **[構成タスク]** で、 **[Office 365 管理者アカウントを変更する]** をクリックします。 管理者アカウントの変更ウィザードが表示されます (Windows Server essentials では、ウィザードの名前は Office 365 管理者アカウントの設定です。)  
  
3.  クリックして、Office 365 サブスクリプションに接続を使用するアカウントの資格情報を入力**次**します。  
  
4.  **[閉じる]** をクリックします。 ダッシュボードが再起動します。  
  
###  <a name="BKMK_Disable"></a> Office 365 統合を無効にします。  
 ダッシュ ボードから、Office 365 サービスおよびオンライン アカウントを管理しない場合は、Office 365 統合を無効にすることができます。 Office 365 サブスクリプションがアクティブなと、ダッシュ ボードから加えた構成変更有効のままにします。 たとえば、電子メール アドレス、Office 365 サブスクリプションにリンクしたドメイン名を受け取ります。 任意の電子メールを失うことと、モバイル デバイス用に設定したコントロールは引き続き Exchange Online を使用します。  
  
 今後は、Office 365 サブスクリプション、サービス、および Office 365 でのリソースを管理して、ユーザーが Office 365 でのオンライン アカウントのパスワードを管理する必要があります。 パスワード同期が不要になったが発生し、無効にするか、ユーザー アカウントを削除する効果はありません、ユーザーのオンライン アカウントでします。  
  
 Office 365 統合ソフトウェアは、ローカル サーバーにインストールされている、ため、統合サービスは、Office 365 に接続できない場合でも、機能を無効にできます。  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>サーバーと Office 365 の統合を無効にするには  
  
1.  ダッシュボードで、 **[Office 365]** をクリックします。  
  
2.  **[Office 365 統合を無効にする]** をクリックします。 [Office 365 を無効にする] ウィザードが表示されます。  
  
3.  指示に従ってウィザードを完了します。  
  
> [!NOTE]
>  Office 365 統合を再度有効にする、使用、 **Office 365 との統合**タスクで、**サービス**、ダッシュ ボードのタブ**ホーム**ページ。 手順については、次を参照してください。[手順 2。Windows Server Essentials サーバーと Microsoft Office 365 を統合](#BKMK_StepTwo)、このトピックの「以前のバージョン。  
  
##  <a name="BKMK_Troubleshoot"></a> Office 365 統合をトラブルシューティングします。  
 このセクションでは、Windows Server Essentials で、Office 365 統合機能を使用する場合に発生する可能性がある一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
###  <a name="BKMK_AcctsNotCreated"></a> 一部の Microsoft Online Services アカウントは作成されませんでした。  
 **説明**  
  
 成功したとしたときに、ダッシュ ボードから 1 つまたは複数の Microsoft Online Services アカウントを作成しようがありませんでした。  
  
 **ソリューション**  
  
1.  ウィザードの完了ページにあるリンクをクリックして、正常終了しなかった各アカウント作成要求に関する詳細な情報が含まれる結果ファイルを開きます。 たとえば、要求したアカウント名を持つ Microsoft Online Services アカウントが既に存在するという結果が示される場合があります。  
  
2.  推奨される操作に従って、各エラーを解決します。  
  
3.  この問題が解決しない場合は、サーバーを再起動して、オンライン アカウントの作成を再度試みます。  
  
###  <a name="BKMK_ProblemUninstalling"></a> Office 365 統合のアンインストールの問題が発生しました  
 **説明**  
  
 Office 365 統合を無効にしようとしたときに、不明なエラーが発生しました。  
  
 **ソリューション**  
  
1.  コンピューターがインターネットに接続されていることを確認してから、再試行してください。  
  
2.  エラーが再び発生する場合は、サーバーを再起動し、もう一度試してください。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials - 第 1 部のサービスの統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials - パート 2 のサービスの統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Microsoft Office 365 を使用するクイック スタート ガイド](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services を管理します。](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)
