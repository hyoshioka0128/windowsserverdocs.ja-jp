---
title: Windows Server Essentials ユーザーのオンライン アカウントの管理
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c09f4cf6-4d12-49fe-9ae4-e6cb14027b9d
8author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 95f401bbec9bb503d19e2d9918a05851c04f7ef4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824093"
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Windows Server Essentials ユーザーのオンライン アカウントの管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Microsoft Office 365 と Windows Server Essentials サーバーを統合する場合は、ダッシュ ボードから、オンライン アカウントとユーザー アカウントを管理できます。 このトピックで読んだ後を検索できる、ダッシュ ボードから、ユーザーの Microsoft Online Services アカウントを管理することで、作成し、ダッシュ ボードからオンライン アカウントを管理する方法、および Exchange Online の電子メール アドレスと配布グループを管理する方法ダッシュ ボード。  

  
> [!NOTE]
>  Windows Server Essentials での Microsoft Online Services アカウントを管理するには、サーバーを Office 365 と統合する必要があります。 手順については、次を参照してください。 [Office 365 の管理](Manage-Office-365-in-Windows-Server-Essentials.md)します。  
  
> [!IMPORTANT]
>  かどうかは Windows Server Essentials でのオンライン アカウントを管理することに慣れていると呼ばれる Microsoft Online Services アカウントが表示されます*Office 365 アカウント*します。 In Windows Server Essentials ダッシュ ボードでは、ラベルに変更されました*Microsoft Online Services アカウント*、または*Microsoft オンライン アカウント*省略形。 アカウントと手順は同じです。ラベルだけが変更されています。 このトピックのほとんどの手順では、用語*オンライン アカウント*を使用します。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [自分のオンライン アカウントをダッシュ ボードから管理する必要があります。](#BKMK_WhyManageOnlineAccounts)  
  
-   [オンライン アカウントを作成します。](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [オンライン アカウントを管理します。](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Exchange Online の電子メール アドレスを管理します。](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Exchange online 配布グループを管理します。](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a> 自分のオンライン アカウントをダッシュ ボードから管理する必要があります。  
 ユーザー アカウントに Microsoft Online Services アカウントを割り当てる、ダッシュ ボードを使用してアカウントのパスワードは自動的に同期すると、ユーザー アカウントのライフ サイクル全体で同時に 2 つのアカウントを維持することができます。  
  
 S、サーバーと Office 365 では、リソースにアクセスするのと同じパスワードを使用できるユーザーと、ユーザーにとって便利です。 社内のリソースを必要とする Office 365 内のリソースにアクセスするために同じパスワード要件を適用することができます。  
  
### <a name="how-does-password-synchronization-work"></a>パスワード同期化のしくみ  
 ダッシュ ボードを使用すると、ユーザー アカウントに Microsoft Online Services アカウントの割り当て、ユーザーのオンライン アカウントとユーザー アカウントのパスワードが自動的に同期します。 これは、ユーザーにのみ、サーバーと Office 365 で、両方のリソースにアクセスする 1 つのパスワードが必要なことを意味します。 さらに、同じユーザー アカウントとユーザーのオンライン ID の名前を使用することができます。  
  
 パスワードの同期は、ドメインに参加しているコンピューターまたはリモート Web アクセスを使用してユーザー アカウントのパスワードを変更した直後に自動で行われます。  
  
> [!IMPORTANT]
>  Windows Server Essentials と Office 365 を統合すると場合、ユーザーでは、Office 365 ポータルからの Microsoft オンライン アカウントのパスワードは変更されません。 それを行うと、パスワードの同期化は中断されます。  
  
### <a name="simplified-account-creation"></a>簡素化されたアカウントの作成  
 S、ダッシュ ボードから初期オンライン アカウントを作成するときに、もう 1 つの利点です。 単一の操作で、すべてのユーザーのオンライン アカウントを作成できます。 その一方で、従業員は Office 365 に既にを使用して、新しい Windows Server Essentials サーバーを設定する、作成できますすべてのユーザー アカウント 1 つのアクションでオンライン アカウントから。 詳細については、「[オンライン アカウントの作成](#BKMK_SECTION_CreateOnlineAccounts)」を参照してください。  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>ダッシュボードから電子メール アドレスと配布グループを管理する  
 Exchange Online の電子メール アドレスと配布グループは、ダッシュボードから管理することができます。 電子メール アドレスでは、組織のインターネット ドメインを使用することができます。 すべての設定は、Office 365 にサインインしなくてもダッシュ ボードで、行うことができます。 (読んだ後は、ダッシュ ボードから配布グループを管理する Windows Server Essentials を使用する必要があります。 この機能はサポートされていません in Windows Server Essentials。)詳細については、「[Exchange Online の電子メール アドレスの管理](#BKMK_SECTION_ManageEmailAddresses)」と「[Exchange Online の配布グループの管理](#BKMK_SECTION_ManageDistributionGroups)」を参照してください。  
  
### <a name="manage-the-user-account-and-online-account-together"></a>ユーザー アカウントとオンライン アカウントを一緒に管理する  
 また、アカウントのライフ サイクル全体でユーザー アカウントと共にオンライン アカウントを管理できます。 ユーザー アカウントを非アクティブにすると、Microsoft Online Services でオンライン アカウントも非アクティブにされます。 ユーザー アカウントを削除すると、オンライン アカウントも削除されます。 詳細については、「 [オンライン アカウントの管理](#BKMK_SECTION_ManageOnlineAccounts)」を参照してください。  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a> オンライン アカウントを作成します。  
 Office 365 とサーバーを統合すると、Microsoft Online Services を作成する方が得策 s が、ダッシュ ボードからユーザーのアカウントします。 読んだ後に、多くのオンライン アカウントの作成の柔軟性があります。 新しい Office 365 サブスクリプションがあれば、一括作成できますオンライン アカウントのすべてのユーザー。 Office 365 でのオンライン アカウントを既に作成している場合、心配はありません。 新しいサーバーを設定するを作成できる場合、ユーザー アカウント、サーバーでオンライン アカウントをインポートすることで。 個々 のユーザー アカウントを作成するときに、または既存のユーザー アカウントにオンライン アカウントを追加すると、新規または既存のオンライン アカウントを割り当てることができます。  
  
 **ライセンスの要件**を作成するオンライン アカウントごとのユーザー ライセンスは必要があります。 チェック、 **Office 365**ユーザー ライセンスの数は、Office 365 サブスクリプションを利用してダッシュ ボードのページ。 複数のユーザー ライセンスを追加する必要がある場合は、そのために Office 365 での Office 365 サブスクリプションを開くに読んだ後ができます。  
  
 **ユーザーのフォロー アップ**ユーザーが次回サインインしたユーザー アカウントのパスワードを変更するために必要なユーザー アカウントに対してオンライン アカウントを追加した後。 新しいパスワードは、オンライン アカウントにすぐに同期します。 その後、そのオンライン ID を持つ Office 365 にサインインするパスワードを使用したことができます。  
  
> [!IMPORTANT]
>  決して変更しないように Office 365 でオンライン アカウントのパスワードをユーザーに強調します。 パスワードは、ユーザーが自分のユーザー アカウントのパスワードを変更したときに必ず自動的に変更されます。 Office 365 でオンライン パスワードを変更した場合、パスワード同期は切断されます。  
  
 このセクションに示す手順に従って、次のことを行います。  
  
-   [既存のユーザー アカウントのオンライン アカウントを一括作成します。](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Microsoft Online Services アカウントからのユーザー アカウントのインポート](#BKMK_ToImportUserAccounts)  
  
-   [オンライン アカウントが割り当てられた新しいユーザー アカウントを作成します。](#BKMK_ToCreateaNewUserAccount)  
  
-   [ユーザー アカウントにオンライン アカウントを割り当てる](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  表示は Windows Server Essentials を使用する場合は*Office 365 アカウント*の代わりに*Microsoft Online Services アカウント*これらの手順全体にわたっています。 プロセスは、同じですが、Windows Server Essentials での用語が変更されました。  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a> 既存のユーザー アカウントのオンライン アカウントを一括作成するには  
  
1.  管理者は、サーバーにサインインし、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ダッシュボードで、**[ユーザー]** ページを開きます。  
  
3.  **[ユーザー タスク]** で、**[Microsoft Online アカウントの追加]** をクリックします。  
  
     ウィザードの **[Microsoft Online Services アカウントの追加]** ページには、Microsoft オンライン アカウントを持っていないすべてのユーザー アカウントが表示されます。 既定ではすべてのアカウントが選択されており、Microsoft オンライン ID に対してユーザー名が提案されます。 カスタム インターネット ドメインを Office 365 サブスクリプションにリンクした場合、そのドメインは既定で使用されます。  
  
4.  **[Microsoft Online Services アカウントの追加]** ページで、作成されるアカウントを確認します。 たとえば、オンライン ID が異なるオンライン アカウントを既に持っているユーザーがいるかどうかを確認し、電子メール アドレスで使用するドメインが選択されていることを確認します。 必要な変更作業が終了したら、 **[次へ]** をクリックします。  
  
5.  **割り当てる Microsoft Online Services ライセンス**ページで、選択した Office 365 サービス、ユーザーが使用されます。 **[次へ]** をクリックすると、アカウントの作成が開始されます。  
  
    > [!NOTE]
    >  オンライン アカウントごとに、サービスのライセンスを Office 365 が必要です。 利用可能なライセンスを確認し、必要に応じてサブスクリプションを開いて、ダッシュボードの **[Office 365]** ページからライセンスを追加します。  
  
6.  Microsoft オンライン アカウントを使用できるようになったことをユーザーに通知します。 Office 365 にサインインすることができます前に、ネットワーク ユーザー アカウントのパスワードを変更する必要があります。 手順については、「[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)」を参照してください。  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a> 新しい Microsoft オンライン アカウントの使用を開始するには  
  
1.  ネットワーク ユーザー アカウントを使用してコンピューターにサインインします。  
  
2.  ユーザー アカウントのパスワードを変更します。 まず、Ctrl + Alt + Del キーを押し、次に **[パスワードの変更]** をクリックします。  
  
     パスワードを変更すると、そのパスワードは新しいオンライン アカウントに同期されます。 Office 365 にサインインするのと同じパスワードを使えるようになりました。  
  
3.  新しいオンライン ID とユーザー アカウントのパスワードを使用して、[Office 365 にサインイン](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) します。  
  
    > [!IMPORTANT]
    >  Office 365 で、オンライン アカウントのパスワードも変わりません。 それを行うと、パスワード同期化が無効になります。 ネットワーク ユーザー アカウントのパスワードを変更するたびに、オンライン パスワードが更新されます。  
  
###  <a name="BKMK_ToImportUserAccounts"></a> 既存のオンライン アカウントからユーザー アカウントをインポートするには  
  
1.  ダッシュボードで、**[ユーザー]** ページを開きます。  
  
2.  **[ユーザー タスク]** で、**[Office 365 からのアカウントのインポート]** をクリックします。  
  
     次のページには、サーバー上のユーザー アカウントがない、Office 365 サブスクリプションのすべてのオンライン アカウントが表示されます。 既定ではすべてのアカウントが選択されており、ユーザー名に対してオンライン ID が提案されます。  
  
3.  ユーザー アカウントを作成するには  
  
    1.  提案されたユーザー アカウントに必要な変更を加えます。  
  
    2.  必要に応じて、ユーザー アカウントに割り当てられる一時的なパスワードを表示するリンクをクリックします。 新しいアカウント名と一緒に一時パスワードをユーザーに付与する必要があります  
  
         (読んだ後でこれらのパスワードがこのファイルの一覧を検索、アカウントを作成した後。*SystemDrive*\Users\\*Office365admin*\\*NewServerUser*.txt、 *Office365admin*ネットワーク アカウントは、サーバーでの Office 365 の管理に使用して*NewServerUser*は新しいユーザー アカウントの名前です)。  
  
    3.  **[次へ]** をクリックして、ユーザー アカウントを作成します。  
  
4.  ユーザーは、新しいユーザー アカウントと最初の時間 œ 用のサーバーにサインインを使用して、サインインした後にパスワードを変更する必要があります、一時パスワードを把握できます。 ユーザー向けの手順については、「 [新しい Microsoft オンライン アカウントの使用を開始するには](#BKMK_ToBeginUsingAnOnlineAccount)」を参照してください。  
  
     今後、そのユーザー アカウントを使用して、オンライン アカウントのパスワードを同期して、Office 365 でオンライン パスワードを変更しないでくださいことがわかっていることを確認します。  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a> オンライン アカウントが割り当てられた新しいユーザー アカウントを作成するには  
  
1.  ダッシュボードで、**[ユーザー]** をクリックします。  
  
2.  **[ユーザー タスク]** で、**[ユーザー アカウントの追加]** をクリックします。 ユーザー アカウントの追加ウィザードが表示されます。  
  
3.  指示に従って、ユーザー アカウントを作成します。  
  
4.  **[Microsoft Online Services アカウントの割り当て]** ページで、ユーザー用に新しいオンライン アカウントを作成するか、または既存のオンライン アカウントを割り当てます。  
  
    -   新しいオンライン アカウントを作成するには、**[新しい Microsoft Online Services アカウントを作成し、それをこのユーザー アカウントに割り当てる]** をクリックし、Microsoft Online Services アカウントの名前を入力します (既定では、ユーザー名はオンライン ID に使用されます)。 **[次へ]** をクリックします。  
  
    -   既存の Microsoft オンライン アカウントを割り当てるには、**[既存の Microsoft Online Services アカウントをこのユーザー アカウントに割り当てる]** をクリックし、ドロップダウン リストから既存のアカウントを選択します。 **[次へ]** をクリックします。  
  
    > [!NOTE]
    >  Windows Server Essentials では、Microsoft Online Services アカウントをウィザードとダッシュ ボード ラベルにおいて Office 365 アカウントと呼びます。  
  
5.  指示に従ってウィザードを完了します。  
  
6.  新しいオンライン アカウントで Office 365 にサインインするには事前にユーザー アカウントのパスワードを変更しておく必要があることを、ユーザーに通知します。 手順については、「[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)」を参照してください。  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>ユーザー アカウントにオンライン アカウントを割り当てる  
  
1.  ダッシュボードで、**[ユーザー]** をクリックします。  
  
2.  一覧でユーザー アカウントを右クリックし、**[Microsoft のオンライン アカウントの割り当て]** をクリックします。 Microsoft Online Services アカウントの割り当てウィザードが表示されます。  
  
3.  既存のオンライン アカウントを割り当てるか、ユーザー用に新しいオンライン アカウントを作成します。 新しいアカウントの既定のオンライン ID は、ユーザー名です。 **[次へ]** をクリックし、オンライン アカウントをユーザー アカウントに追加します。  
  
4.  ウィザードの最後のページにある情報を確認し、**[閉じる]** をクリックします。  
  
5.  新しいオンライン アカウントで Office 365 にサインインするには事前にユーザー アカウントのパスワードを変更しておく必要があることを、ユーザーに通知します。 手順については、「[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)」を参照してください。  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a> オンライン アカウントを管理します。  
 Windows Server Essentials でのユーザー アカウントにオンライン アカウントを追加するときにアカウントのライフ サイクル全体で両方のアカウントを一緒に管理できます。  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a> オンライン アカウントの状態を理解します。  
 Microsoft Online Services アカウントをユーザー アカウントに割り当てると、ダッシュボードの **[ユーザー]** ページの **[Microsoft オンライン アカウント]** 列にアカウントの電子メール アドレスが表示されます (Windows Server Essentials では、列ラベルは**Office 365 アカウント**)。  
  
-   電子メール アドレスの横にある青いアイコンは、オンライン アカウントがアクティブであることを示します。 つまり、アカウントが現在の Office 365 ライセンスと、ユーザーは、オンライン ID を使用して Office 365 にサインインすることができます。  
  
-   電子メール アドレスの横にある灰色のアイコンは、オンライン アカウントを示すライセンスがアクティブでなくなったため、非アクティブな œ はか、またはオンライン アカウントの割り当てが解除されました。 ユーザーのオンライン アカウントの割り当てを解除して、ライセンスが削除されると、アカウントを使用して Office 365 へのサインインからユーザーがブロックされます。 ただし、サーバーは、ユーザー アカウント名と Office 365 のメール アドレスの間のマッピングを維持します。  
  
###  <a name="BKMK_UnassignOnlineAccount"></a> オンライン アカウントへのアクセスを制限します。  
 ユーザーが自分の組織を離れるか、Office 365 サービスへのユーザーのアクセスを制限する場合はどうすればでしょうか。 場合、ユーザーのオンライン アカウントと Windows Server Essentials でユーザー アカウントを管理する 3 つのオプション。  
  
-   **オンライン アカウントの割り当て解除**でしょうか。サーバー上のリソースへのアクセスを阻止することがなく Office 365 を使用してユーザーを保持するには、オンライン アカウントの割り当てを解除する必要があります。 Office 365 のライセンスがリリースされ、ユーザーが Office 365 へのサインインからブロックされています。 ただし、サーバーは、ユーザー アカウント名と Office 365 のメール アドレスの間のマッピングを維持します。 手順については、次を参照してください。[ユーザー アカウントからオンライン アカウントの割り当てを解除する](#BKMK_ToUnassignAnOnlineAccount)します。  
  
-   **ユーザー アカウントを非アクティブ化**でしょうか。一時的または永続的に、従業員が退職したため、ユーザー アカウントを無効化する場合、ユーザーのオンライン アカウントもが非アクティブ化します。 オンライン アカウントは使用できませんが、ユーザーのデータ (電子メールなど) は、Microsoft Online Services に保持されます。 手順については、次を参照してください。[ユーザー アカウントを非アクティブ化](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6)で[Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
-   **ユーザー アカウントを削除**でしょうか。ユーザー アカウントを削除する場合、オンライン アカウントが Microsoft Online Services からも削除します。 手順については、次を参照してください。[ユーザー アカウントを削除](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove)で[Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
    > [!WARNING]
    >  オンライン アカウントが削除されると、ユーザー データは Microsoft Online Services のデータ保持ポリシーの影響下に置かれるので注意してください。 従業員が退職した後も、人のユーザーのデータを保持する必要がある場合は、削除することではなく、ユーザー アカウントを非アクティブ化します。  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a> ユーザー アカウントからオンライン アカウントの割り当てを解除するには  
  
1.  ダッシュボードで、**[ユーザー]** をクリックします。  
  
2.  一覧で、ユーザー アカウントを右クリックし、をクリックし、 **Microsoft オンライン アカウントの割り当て解除**(in Windows Server Essentials では、次のようにクリックします。 **、Office 365 アカウントの割り当て解除**)。  
  
3.  確認のプロンプトで、**[はい]** をクリックします。  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a> Exchange Online の電子メール アドレスを管理します。  
 Windows Server Essentials でユーザーのオンライン アカウントに電子メール アドレスを追加することでは、オンライン Exchange で複数の電子メール アドレスに電子メールを受信するユーザーを許可できます。  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a> ユーザーの Microsoft オンライン アカウントに追加の電子メール アドレスを追加するには  
  
1.  Windows Server Essentials ダッシュ ボードで、次のようにクリックします。**ユーザー**します。  
  
2.  一覧でユーザー アカウントを右クリックし、**[アカウント プロパティを表示]** をクリックします。  
  
3.  **Microsoft online**のアカウントのプロパティ タブ (または**Office 365** Windows Server Essentials でのタブ)、をクリックして**追加**します。  
  
4.  新しい電子メールのエイリアスを入力し、電子メール ドメインを選択します。  
  
5.  **[OK]** を 2 回クリックします。  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a> Exchange Online (Windows Server Essentials のみ) の配布グループを管理します。  
 Office 365、Windows Server Essentials サーバーを統合した後は、作成し、Windows Server Essentials ダッシュ ボードから Exchange online 配布グループの管理します。 読んだ後でこれを行う、**配布グループ** タブに追加される、**ユーザー**ページ。 Exchange Online サブスクリプションを持っている場合は、このタブのみ表示されます。 この機能は、Windows Server Essentials でご利用いただけません。  
  
 以下の手順を使用して次のことを行います。  
  
-   [配布グループを追加します。](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [配布グループのメンバーを変更します。](#BKMK_ChangeGroupMembers)  
  
-   [ユーザーの配布グループのメンバーシップを変更します。](#BKMK_EditUserMemberships)  
  
-   [配布グループを削除します。](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a> 配布グループを追加するには  
  
1.  Windows Server essentials ダッシュ ボードで、次のようにクリックします。**ユーザー**、順にクリックします、**配布グループ**タブ。  
  
2.  **[配布グループ タスク]** で、**[配布グループの追加]** をクリックします。  
  
     [新しい配布グループの追加] ウィザードが表示されます。  
  
3.  **[新しい配布グループの追加]** ページで、次の情報を入力し、**[次へ]** をクリックします。  
  
    -   新しい配布グループのグループ名、オプションの説明、および電子メールのエイリアスを入力します。  
  
    -   既定では、配布グループは、組織の外部の人からの電子メールを受信できます。 これを許可しないようにする場合は、該当するオプションをオフにします。  
  
4.  **[グループ メンバーの追加]** ページの **[追加]** ボタンを使用して、オンライン アカウントが割り当てられているアクティブなユーザー アカウント、およびその他の配布グループを、新しい配布グループに追加します。 **[次へ]** をクリックします。  
  
     Exchange Online で新しい配布グループが作成されます。  
  
###  <a name="BKMK_ChangeGroupMembers"></a> 配布グループのメンバーを変更するには  
  
1.  ダッシュボードで、**[ユーザー]** をクリックし、**[配布グループ]** タブをクリックします。  
  
2.  一覧で配布グループを右クリックし、**[グループ メンバーシップの変更]** をクリックします。  
  
3.  **[追加]** ボタンと **[削除]** ボタンを使用し、配布グループに対してアクティブなオンライン アカウントの追加または削除を行います。 **[次へ]** をクリックし、Exchange Online で配布グループ メンバーシップを更新します。  
  
###  <a name="BKMK_EditUserMemberships"></a> ユーザーの配布グループ メンバーシップを変更するには  
  
1.  ダッシュボードで、**[ユーザー]** をクリックします。  
  
2.  一覧でユーザー アカウントを右クリックし、**[アカウント プロパティを表示]** をクリックします。  
  
3.  ユーザー アカウント プロパティで、**[配布グループ]** タブをクリックし、**[編集]** をクリックします。  
  
4.  **[グループ メンバーシップの編集]** ボックスの **[追加]** ボタンと **[削除]** ボタンを使用し、ユーザー アカウントに対して配布グループの追加または削除を行い、**[閉じる]** をクリックします。  
  
5.  **[OK]** をクリックして、更新済のユーザー アカウント プロパティを保存します。  
  
###  <a name="BKMK_RemoveDistributionGroup"></a> 配布グループを削除するには  
  
1.  ダッシュボードで、**[ユーザー]** をクリックし、**[配布グループ]** タブをクリックします。  
  
2.  一覧で配布グループを右クリックし、**[グループの削除]** をクリックします。  
  
3.  確認のプロンプトで、**[グループの削除]** をクリックします。  
  
     配布グループが Exchange Online から削除されます。  
  
## <a name="see-also"></a>関連項目  
  
-   [ユーザー アカウントを管理します。](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Office 365 を管理します。](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services を管理します。](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
