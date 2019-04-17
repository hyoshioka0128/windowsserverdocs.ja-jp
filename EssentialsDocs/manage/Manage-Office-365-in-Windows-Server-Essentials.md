---
title: "Windows Server Essentials での Office 365 を管理します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: b45bddb657b96c7cc5f9291a6c887b9d0801974b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials での Office 365 を管理します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Microsoft Office 365 と Windows Server Essentials サーバーを統合する際、Windows Server Essentials ダッシュ ボードから社内リソースと一緒に、Office 365 サービスとオンライン アカウントを管理できます。 このトピックでは、紹介するは、Office 365 とサーバーを統合することにより得られる利点、方法、およびを管理し、Office 365 統合のトラブルシューティングを行う方法をご覧ください。  
  
  
  
> [!IMPORTANT]
>   Office 365 統合は 1 つのドメイン コントローラー環境でのみサポートされます。 さらに、Office 365 の統合ウィザードは、ドメイン コントローラーで実行する必要があります。  
  
## <a name="in-this-topic"></a>このトピックの「  
  
-   [Office 365 をマイ サーバーと統合する必要があります。](#BKMK_IntegrationOverview)  
  
-   [Office 365 統合をセットアップします。](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 統合を管理します。](#BKMK_ManageIntegration)  
  
-   [Office 365 統合をトラブルシューティングします。](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a>Office 365 をマイ サーバーと統合する必要があります。  
 多くの Windows Server Essentials サーバーと Office 365 を統合する理由があります。 社内リソースの一部の管理が、その他のサービスの Office 365 を利用すると場合、は、ダッシュ ボードで、次の 2 つの場所で操作ではなく、内部設置型のリソースと一緒に、Office 365 サービスとリソースを管理することができます。  
  
-   ユーザー アカウントと共に、Office 365 に、ユーザーのアクセス権を与えるオンライン アカウントを管理するには。  
  
    -   1 つの手順では、ユーザー用の Microsoft Online Services アカウントを作成するか、既存のオンライン アカウント用のサーバーにユーザー アカウントを作成します。 新規または既存のユーザー アカウントにオンライン アカウントを追加することもできます。  
  
         ダッシュ ボードからオンライン アカウントを作成するときにユーザーにログイン Office 365、サーバーで使用される同じパスワードを使用します。 自分のユーザー アカウントのパスワードを変更した場合も、オンライン パスワードを変更します。 オンライン アカウントのパスワードが常にユーザー アカウントに対して設定したセキュリティ要件を満たすことがわかっています。  
  
    -   ユーザー アカウントのライフ サイクル全体を通じて、ユーザー アカウントと共にオンライン アカウントを管理します。 ユーザー アカウントを無効にすると、オンライン アカウントも無効にします。 ユーザー アカウントを削除する場合、オンライン アカウントも削除されます。  
  
    -   Windows Server Essentials サーバーで電子メールの Exchange Online 配布グループも管理します。  
  
-   カスタム インターネット ドメインを Office 365 サブスクリプションにリンクして、組織のインターネット ドメイン (たとえば、contoso.com) から電子メールを送受信します。  
  
-   ダッシュ ボードからサブスクリプションと Office 365 統合を管理します。  
  
-   お客様のサブスクリプションに SharePoint Online ライブラリが含まれている場合、Windows Server Essentials サーバーと Office 365 統合できます。  
  
    -   作成し、ダッシュ ボードから SharePoint Online ライブラリを管理します。  
  
        > [!NOTE]
        >  こともできる My Server 2012 R2 アプリを使用して、ラップトップ、モバイル デバイス、または Windows phone から SharePoint Online ライブラリ内のドキュメントを操作します。 この機能は Windows Server Essentials の利用可能なだけです。 詳細については、次を参照してください。[My Server アプリを使用して](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)します。  
  
    -   、ダッシュ ボードから SharePoint Online チーム サイトのアクセス許可を変更するか、その他の変更を行うダッシュ ボードからチーム サイトを開きます。  
  
     詳細については、次を参照してください。[SharePoint Online の管理](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)します。  
  
-   Exchange Online にサブスクライブする場合、Windows Server Essentials サーバーと Office 365 の統合によって、ユーザーが会社の電子メール サーバーへの接続に使用するモバイル デバイスを管理できます。  
  
    -   モバイル デバイスが会社の電子メール サーバーに接続時にパスワード保護が必要です。 最小パスワード長、サインイン試行失敗を許可して、必須最小時間間隔サインイン試行の数を設定します。  
  
    -   デバイス モデルのセキュリティの問題がわかっている場合、Exchange Online に接続するモバイル デバイスをブロックします。  
  
    -   モバイル デバイスが紛失または盗難にあった場合は、次回のデバイスの電源がオンの企業の機密データを削除するデバイスをワイプします。  
  
-    Office 365 統合では、Office 365 サービスとリソースに接続する新しい方法を示します。  
  
    -   Windows Server Essentials スタート パッドから Office 365 サービスを開きます。 詳細については、次を参照してください。[を使用して Microsoft Office 365 へのクイック スタート ガイド](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)します。  
  
    -   My Server 2012 R2 アプリを使用して、ラップトップ、モバイル デバイス、または Windows phone から SharePoint Online ライブラリ内のドキュメントを操作します。 詳細については、次を参照してください。[My Server アプリを使用して](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)します。 この機能は Windows Server Essentials で利用可能なだけです。  
  
##  <a name="BKMK_Configure"></a>Office 365 統合をセットアップします。  
 Office 365 とサーバーのインストールの完了後いつでも、サーバーを統合できます。 T がない場合は、Office 365 サブスクリプションを既にお持ち、いずれかを購入するか、または、無料試用版サブスクリプションにサインアップします。  
  
 次のタスクには。  
  
-   [手順 1: Office 365 統合要件を確認します。](#BKMK_StepOne_VERIFY)  
  
-   [手順 2: サーバーを Microsoft Office 365 を統合します。](#BKMK_StepTwo)  
  
-   [手順 3: 組織のインターネット ドメイン名を Office 365 (省略可能) にリンクします。](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a>手順 1: Office 365 統合要件を確認します。  
 開始する前に、サーバーがこれらの要件を満たしていることを確認します。  
  
-   サーバーは、これらのオペレーティング システムのいずれかを持つことができます。Windows Server Essentials、Windows Server Essentials、または、Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter オペレーティング システム、Windows Server Essentials エクスペリエンス役割がインストールされているとします。  
  
-   環境では、1 つのドメイン コントローラーを持つことができますのみとドメイン コントローラーで Office 365 統合を実行する必要があります。  
  
-   サーバーからインターネットに接続できる必要があります。  
  
-   Office 365 統合を開始する前に、サーバー上ですべての重大かつ重要な更新プログラムをインストールしてください。  
  
-   場合は、組織のインターネット ドメイン、SharePoint Online のリソースを使用して、電子メール アドレスでを使用するには、ドメインを Office 365 にリンクするには統合中にできるようにドメイン名を登録する ll する必要があります。 詳細については、次を参照してください。[ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)します。  
  
> [!NOTE]
>  Office 365 を事前にサブスクライブする必要はありません。 サブスクリプションを購入または Office 365 統合中に無料試用版にサインアップすることができます。 プランと Office 365 の価格設定を確認する場合は、d[ビジネス向け Office 365 プランの比較](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)します。  
  
###  <a name="BKMK_StepTwo"></a>手順 2: サーバーを Microsoft Office 365 を統合します。  
 ドメイン コントローラーで Windows Server Essentials サーバーと Office 365 を統合するには、次の手順を実行します。  
  
> [!NOTE]
>  S 手順と同じかどうかがある Windows Server Essentials または Windows Server Essentials を紹介するが、ホーム ページで異なる場所から開始します。 Windows Server Essentials での Office 365 やその他の Microsoft Online Services で、サーバーを統合する、**サービス**] タブ。Windows Server essentials では、Office 365 統合がで実行、**電子メール**] タブ。  
  
##### <a name="to-integrate-the-server-with-office-365"></a>Office 365 とサーバーを統合するには  
  
1.  管理者は、サーバー ログオンし、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  **ホーム**] ページで [**サービス**(Windows Server Essentials では、をクリックして**電子メール**)、] をクリックして**Microsoft Office 365 との統合**、] をクリックし、**Microsoft Office 365 統合のセットアップ**します。  
  
     Microsoft Office 365 のウィザードとの統合が表示されます。  
  
3.  **始める**] ページで、次の操作のいずれかを実行します。  
  
    -   T don の Office 365 へのサブスクリプションであれば、] をクリックして**次**、試用版サブスクリプションをサインインまたは Office 365 をサブスクライブする指示に従います。  
  
         ウィザードに戻る前に、Office 365 へのログインを紹介する必要があります。 タスクでは、いずれかを実行する必要はありませんが、**ここから開始**Office 365 ポータルのセクションです。  
  
    -   サーバーと統合する Office 365 へのサブスクリプションが既に**Office 365 のサブスクリプションが既にあるは**、] をクリックし、**[次へ]**します。  
  
4.  ウィザードを完了するための手順に従います。  
  
 ウィザードが正常に完了した後、ダッシュ ボードには、次の変更をすることがわかります。  
  
-   新しいそこ s **Office 365** ] ページで、統合と Office 365 サブスクリプションを管理するために使用されます。  
  
-   **ユーザー** ] ページで、説明を参照してください、**オンライン アカウント**] タブを作成および Office 365 へのアクセスをユーザーに与える Microsoft Online Services アカウントを管理できます。 オンラインで交換するを使用している場合、Windows Server Essentials サーバーがあるとしてもわかります、**配布グループ**] タブの [します。  
  
-   **記憶域**Windows Server Essentials サーバー上のページには、**SharePoint ライブラリ**] タブの [SharePoint Online ライブラリを管理すると、チーム サイトのアクセス許可を変更します。 すべての Office 365 ビジネス プランには、これらの基本的な機能 SharePoint Online にはが含まれています。  
  
###  <a name="BKMK_StepThree"></a>手順 3: 組織のインターネット ドメイン名を Office 365 (省略可能) にリンクします。  
 独自のインターネット ドメイン、組織と SharePoint Online リソースの Url 宛ての電子メールを使用する場合は、カスタム ドメインを Office 365 サブスクリプションにリンクできます。 Office 365 を Windows Server Essentials サーバーを統合する場合は、ダッシュ ボードからこれを実行できます。  
  
 オンラインで作成する前に行う最も簡単な s、ユーザーのアカウントを作成するときに一括でオンライン アカウントにドメインを使用できるようにします。  
  
 Office 365 にサインアップするときに、ドメイン名を取得するか。たとえば、*contoso*。onmicrosoft.com します。はなく別のドメイン名を使用する d 場合ですか?」と言います contoso.com だけですか? することができます。 ドメイン名の購入 t がない場合、独自に既に 1 つと DNS レコードの一部を変更する必要がありますします。  
  
 Office 365 を使用するカスタム ドメインの設定には、4 つのタスクが含まれます。  
  
1.  **ドメイン名の購入します。** つまり、ドメイン レジストラーまたは DNS ホスティング プロバイダーに登録します。  
  
    -   Office 365 と連携するドメイン名を選択します。 第 2 レベル ドメイン名を使用することができますか? buycontoso.com などですか? 第 3 レベル ドメイン名ではありませんが、ですか? marketing.contoso.com などです。Office 365 で使用するドメインの選択の詳細については、次を参照してください。[ドメイン](https://technet.microsoft.com/library/office-365-domains.aspx)します。  
  
    -   Office 365 で必要なドメイン ネーム サーバー (DNS) レコードを許可するドメイン レジストラーからドメインを購入します。 どのドメイン レジストラーが、必要な DNS レコードを許可するを参照してください[ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)します。 異なるレジストラーに既にドメインが登録されている場合は、心配はありません。Office 365 をドメインにリンクするときに、異なるレジストラーにドメインを転送できます。  
  
2.  **Office 365 サービスがドメイン名を使用するように DNS レコードを構成します。** 最も簡単な方法は、ウィザードの手順 3 で Office 365 サブスクリプションにドメインをリンクするときの DNS レコードを構成します。 この場合 d ではなく、自分を参照してください。[Office 365 統合の DNS に手動で構成する方法を記録](#BKMK_ManuallyConfigureDNS)します。  
  
3.  **カスタム インターネット ドメインを Office 365 サブスクリプションにリンクします。** 今回の使用、**ドメインを Office 365 にリンク**操作します。  
  
4.  **Office 365 サービスが、新しいドメイン名を使用していることを確認します。**  
  
 使用する前に、手順 1 と 2 を完了するかどうか、**ドメインを Office 365 にリンク**タスク、ウィザードが、ドメイン名を Office 365 にリンクできます。 代わりに、手順 1 と 2 の一部またはすべてを手伝ってウィザードことができます。  
  
##### <a name="to-link-your-organization-s-internet-domain-to-office-365"></a>組織のインターネット ドメインを Office 365 にリンクするには  
  
1.  ダッシュ ボードを開く、**Office 365**ページ、およびクリックして**ドメインを Office 365 にリンク**します。  
  
2.  ウィザードを完了するための手順に従います。  
  
     ウィザードでは、登録、構成、および Office 365 で使用する新規または既存インターネット ドメイン名をリンクする手順の一部またはすべてに役立ちます。  
  
     タスクを完了する必要がある情報を取得するウィザード ページで [ヘルプ] リンクをクリックします。 セットアップのドメイン名のセクションを参照してください。または[Windows Server Essentials でのリモート Web アクセスの管理](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx)プロセスの概要と要件です。  
  
    > [!NOTE]
    >  新しいドメイン名を登録するウィザードを使用して、ウィザードでのシームレスな統合を提供する Microsoft と提携しているドメイン ネーム サービス プロバイダーのいずれかを使用する必要があります。 ドメイン名レジストラーを見つけるを参照してください。[ドメイン名の購入方法](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)します。  
  
3.  場合は、ドメイン名ではありません t がサーバーによって管理されている検出されるとウィザード、構成の完了に必要な DNS レコードを手動で構成する説明する必要があります。 手順については、次を参照してください。[Office 365 統合の DNS に手動で構成する方法を記録](#BKMK_ManuallyConfigureDNS)、このトピックで後述します。  
  
4.  ドメインを Office 365 で使用されていることを確認します。  
  
     ウィザードが完了したら、ドメイン名レジストラーが DNS レコードを確認中にほとんどの待機秒ですね。 これは。t don は、何もする必要です。 一般に約 1 時間がかかりません。と少し長くなる場合があります。 ドメインの確認が完了すると、**Office 365** ] ページで、組織のドメインが一覧表示します。  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a>Office 365 統合の DNS レコードを手動で構成する方法  
 Office 365 ウィザードへのリンク、ドメイン、ドメイン名がサーバーによって管理されていない検出されると場合、構成を完了する必要があります手動で構成する必要なドメイン ネーム サーバー (DNS) レコードです。 その場合は、するわかりますで構成する必要がある DNS レコードの一覧**%username%\NewDNSRecords_ (n) .txt**ここで、*(n)*はランダムな番号です。  
  
 次の表では、追加する必要がある DNS レコードについて説明します。 入力方法は、別のドメイン名レジストラーによって異なります。 ご質問がある場合は、ヘルプのドメイン名レジストラーを依頼します。  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>カスタム インターネット ドメイン名を Office 365 にリンクするための必要な DNS レコード  
  
|サービス|必要な DNS レコード|目的|  
|-------------|--------------------------|-------------|  
|(複数のサービス)|MX| Office 365 では、このレコードを使用して、特定のドメイン名を所有していることを確認します。 この MX レコードは、電子メール メッセージのルーティングは影響しません。|  
|Exchange Online|MX|電子メール メッセージのルーティングを提供します。 **重要:**電子メールを移行する場合を割り当てないでください、優先順位ゼロ (**0**)、新しい MX レコードにします。 レコードの値が、現在の MX レコードに割り当てられている値より大きいことを確認します。 電子メールの移行が完了すると、Office 365 への電子メール サーバーを変更する準備ができたらがある、ドメイン名レジストラーに、新しい MX レコードの優先順位の値をリセットします。|  
|Exchange Online|エイリアス (CNAME)|ユーザーを簡単に行うための自動検出レコードは、Exchange Online と Outlook デスクトップ クライアントまたはモバイル電子メール クライアントの間の接続を設定します。 **注:**標準的な URL (https://outlook.com/owa/office365.com) ではなく、組織の独自のドメイン名 (たとえば、http://mail.contoso.com) を使用して Outlook Web Access にアクセスする場合は、エイリアス (CName) レコードを次のように構成できます:**種類 CNAME、TTL を = = 01: 00:00、ホスト名、メール アドレスを = = mail.office365.com**|  
|Exchange Online|TXT|ドメインの代わりに電子メールを送信する outlook.com、Office 365 の電子メール サーバーによって使用されるドメインが承認されていることを指定します。 送信電子メールがスパムとしてフラグ付けされることを防ぐために、このレコードを作成します。|  
|Lync Online|SRV|Windows Live や yahoo! など他のインスタント メッセージング サービスとフェデレーションを有効にするのに役立ちます。|  
|Lync Online|SRV|ユーザーを簡単に行うための自動検出レコードは、デスクトップの Lync クライアントと Microsoft Lync Online 間の接続を設定します。|  
  
> [!IMPORTANT]
>  ドメインの後に検証が完了したらを追加または DNS レコードに Office 365 ポータルからさらに変更を加えるしないでください。  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a>次の手順  
  
-   ユーザー用の Microsoft Online Services アカウントを作成します。  
  
     Office 365 サービスを使用するには、ユーザーは、ネットワーク ユーザー アカウントに関連付けられた Microsoft Online Services アカウントが必要です。 ダッシュ ボードを使用するこの簡単にできます。 かどうかする新しい Office 365 サブスクリプションを使用している、一括作成できますオンライン アカウントの既存のユーザー アカウント。 場合、Office 365 サブスクリプションを既に使用している、するアカウントをインポートできますユーザーから、既存のオンラインで新しいサーバーを統合するアカウント。 手順については、次を参照してください。[ユーザーのオンライン アカウントの管理](Manage-Online-Accounts-for-Users.md)します。  
  
> [!NOTE]
>  Windows Server essentials ダッシュ ボードでは、Microsoft Online Services アカウントを Office 365 アカウントと呼びます。 アカウントは同じです。用語だけを変更します。  
  
##  <a name="BKMK_ManageIntegration"></a>Office 365 統合を管理します。  
 サーバーと、Office 365 を統合した後、**Office 365**ダッシュ ボードのページが Office 365 サブスクリプションに関する情報を表示およびはこれらのタスクを利用できるようにします。  
  
-   [Office 365 サブスクリプションの管理](#BKMK_ManageO365)ですか?サブスクリプションの管理に使用する管理者アカウントを変更します。 サブスクリプションの管理に Office 365 管理ダッシュ ボードを開きます。  
  
-   [組織のインターネット ドメインを Office 365 にリンク](#BKMK_StepThree)ですか?独自のドメイン宛ての電子メールの送受信を行うことができる場合は、ドメインを Office 365 にリンクできます。 (前で説明した[手順 3: 組織のドメインを Office 365 にリンク](#BKMK_StepThree).)  
  
-   [Office 365 統合を無効にする](#BKMK_Disable)ですか?表示されないが、ダッシュ ボードから、Office 365 サービス、サブスクリプション、およびオンライン アカウントを管理する場合は、Office 365 統合を無効にすることができます。 サービスは、Office 365 ポータルから利用できます。  
  
###  <a name="BKMK_ManageO365"></a>Office 365 サブスクリプションを管理します。  
 を運用しているサーバー上の中に、Office 365 サブスクリプションに変更を加える必要がある場合は、から Office 365 のサブスクリプションを開くことができます、**Office 365**ダッシュ ボードのページです。 Office 365 サービスに変更を加えるサーバーが使用する管理者アカウントを変更することもできます。  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 管理ダッシュ ボードにお客様のサブスクリプションを開く  
  
1.  Windows Server Essentials ダッシュ ボードを開く、**Office 365**ページ。  
  
2.  **構成タスク**、] をクリックして**Office 365 の管理**します。  
  
3.  サブスクリプションの管理に使用する、Microsoft オンライン アカウントを Office 365 にログインします。  
  
     Office 365 管理ダッシュ ボードを開きます。  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 管理者アカウントを変更するには  
  
1.  ダッシュ ボードで、をクリックして**Office 365**します。  
  
2.  **構成タスク**、] をクリックして**Office 365 管理者アカウントを変更**します。 管理者アカウントの変更ウィザードが表示されます。 (Windows Server Essentials で、ウィザードは [Office 365 管理者アカウントの設定。)  
  
3.  クリックして、Office 365 サブスクリプションへの接続に使用するアカウントの資格情報を入力**次**します。  
  
4.  をクリックして**閉じる**します。 ダッシュ ボードを再起動します。  
  
###  <a name="BKMK_Disable"></a>Office 365 統合を無効にします。  
 T がないことを決定する場合は、Office 365 サービスおよびオンライン アカウントをダッシュ ボードから管理する、Office 365 統合を無効にすることができます。 Office 365 のサブスクリプションはアクティブなし、ダッシュ ボードから行われた構成変更が有効にします。 たとえば、ll するは、Office 365 のサブスクリプションにリンクしたドメイン名宛ての電子メールを受信します。 獲得した t 任意のメールが失われ、モバイル デバイス用に設定したコントロールは引き続き Exchange Online を使用します。  
  
 今後は、Office 365 サブスクリプション、サービス、および Office 365 でリソースを管理して、ユーザーが Office 365 で、オンライン アカウントのパスワードを管理する必要があります。 パスワード同期は不要になった場合、無効にすると、ユーザー アカウントを削除または影響はありません、ユーザーのオンライン アカウントにします。  
  
 ローカル サーバーに Office 365 統合ソフトウェアがインストールされている、ため、統合サービスは、Office 365 に接続できない場合でも、機能を無効にできます。  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>サーバーと Office 365 の統合を無効にするには  
  
1.  ダッシュ ボードで、をクリックして**Office 365**します。  
  
2.  をクリックして**Office 365 統合を無効にする**します。 Office 365 を無効にするウィザードが表示されます。  
  
3.  ウィザードを完了するための手順に従います。  
  
> [!NOTE]
>  もう一度 Office 365 の統合を有効にするには使用、**Office 365 との統合**タスクで、**サービス**s ダッシュ ボードのタブ**ホーム**ページ。 手順については、次を参照してください。[手順 2: Windows Server Essentials サーバーと Microsoft Office 365 を統合](#BKMK_StepTwo)、このトピックの「以前のバージョン。  
  
##  <a name="BKMK_Troubleshoot"></a>Office 365 統合をトラブルシューティングします。  
 ここでは、Windows Server Essentials での Office 365 統合機能を使用する場合に発生する可能性のある一般的な問題のトラブルシューティングに役立つ情報を説明します。  
  
###  <a name="BKMK_AcctsNotCreated"></a>一部の Microsoft Online Services アカウントは作成されませんでした。  
 **説明**  
  
 成功したダッシュ ボードされなかった t から 1 つまたは複数の Microsoft Online Services アカウントを作成しようとしました。  
  
 **解決策**  
  
1.  正常に完了しなかった各アカウント作成要求に関する詳細な情報が含まれる結果ファイルを開くウィザードの完了ページ上のリンクをクリックします。 たとえば、という結果が示さを要求したアカウントの名前の Microsoft Online Services アカウントが既に存在することです。  
  
2.  各エラーを解決するのには推奨される操作を実行します。  
  
3.  この問題が解決しない場合、サーバーを再起動し、再度オンライン アカウントを作成します。  
  
###  <a name="BKMK_ProblemUninstalling"></a>Office 365 統合のアンインストールの問題が発生しました  
 **説明**  
  
 Office 365 統合を無効にしようとしたとき、不明なエラーが発生しました。  
  
 **解決策**  
  
1.  コンピューターが、インターネットに接続されていることを確認して、もう一度やり直してください。  
  
2.  エラーが再び発生する場合、サーバーを再起動し、もう一度やり直してください。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials の第 1 部のサービス統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials - パート 2 のサービス統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [クイック スタート ガイド: Microsoft Office 365 を使用するには](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services を管理します。](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](../manage/Manage-Windows-Server-Essentials.md)
