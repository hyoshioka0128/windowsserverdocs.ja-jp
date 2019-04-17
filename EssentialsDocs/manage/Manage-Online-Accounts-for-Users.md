---
title: "Windows Server Essentials ユーザーのオンライン アカウントを管理します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Windows Server Essentials ユーザーのオンライン アカウントを管理します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Microsoft Office 365 と Windows Server Essentials サーバーを統合する際は、ダッシュ ボードからユーザー アカウントと共にオンライン アカウントを管理できます。 このトピックでは、した後は、ダッシュ ボードから、ユーザーの Microsoft Online Services アカウントを管理することによって得られる利点、作成し、ダッシュ ボードからオンライン アカウントを管理する方法と、ダッシュ ボードから Exchange Online の電子メール アドレスと配布グループを管理する方法をご覧ください。  

  
> [!NOTE]
>  Windows Server Essentials での Microsoft Online Services アカウントを管理するには、サーバーを Office 365 と統合する必要があります。 手順については、次を参照してください。[Office 365 の管理](Manage-Office-365-in-Windows-Server-Essentials.md)します。  
  
> [!IMPORTANT]
>  かどうか、Windows Server Essentials でのオンライン アカウントを管理するしたに慣れていると呼ばれる Microsoft Online Services アカウントが表示*Office 365 アカウント*します。 Windows Server Essentials のダッシュ ボードで、ラベルが変更された*Microsoft Online Services アカウント*、または*Microsoft オンライン アカウント*短いのです。 アカウントと手順は同じです。ラベルだけを変更します。 ほとんどの手順では、このトピックの「という用語を使用して*オンライン アカウント*します。  
  
## <a name="in-this-topic"></a>このトピックの「  
  
-   [オンライン アカウントをダッシュ ボードから管理する必要があります。](#BKMK_WhyManageOnlineAccounts)  
  
-   [オンライン アカウントを作成します。](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [オンライン アカウントを管理します。](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Exchange Online の電子メール アドレスを管理します。](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Exchange Online の配布グループを管理します。](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a>オンライン アカウントをダッシュ ボードから管理する必要があります。  
 ユーザー アカウントに、Microsoft Online Services アカウントを割り当てる、ダッシュ ボードを使用してアカウントのパスワードが自動的に同期は、ユーザー アカウントのライフ サイクル全体で一緒に 2 つのアカウントを保持しておくことができます。  
  
 サーバーと Office 365 では、リソースにアクセスするための同じパスワードを使用できるユーザーと、ユーザーにとって便利です。 社内のリソースが必要な Office 365 のリソースにアクセスするために同じパスワード要件を適用することができます。  
  
### <a name="how-does-password-synchronization-work"></a>パスワード同期のしくみ  
 ダッシュ ボードを使用すると、ユーザー アカウントに Microsoft Online Services アカウントの割り当て、ユーザー アカウントのパスワードはユーザーのオンライン アカウントに自動的に同期します。 これは、ユーザーに、サーバーと Office 365 で、両方のリソースにアクセスする 1 つのパスワードのみ必要があることを意味します。 さらに、ユーザー アカウントとユーザーのオンライン ID に同じ名前を使用することができます。  
  
 パスワード同期は、すぐにし、自動的に、ドメインに参加しているコンピューターから、またはリモート Web アクセスを使用して、ユーザーが自分のユーザー アカウントのパスワードを変更するときに発生します。  
  
> [!IMPORTANT]
>  Windows Server Essentials と Office 365 を統合すると場合、ユーザーが、Office 365 ポータルから自分の Microsoft オンライン アカウントのパスワードを変更する必要がありますされません。 これを行うと、パスワード同期は中断されます。  
  
### <a name="simplified-account-creation"></a>簡素化されたアカウントの作成  
 その他の利点がある、ダッシュ ボードから初期オンライン アカウントを作成する場合。 すべての単一の操作でユーザーのオンライン アカウントを作成できます。 一方、従業員が Office 365 を既に使われている場合、新しい Windows Server Essentials サーバーを設定することができますから作成するすべてのユーザー アカウント、単一の操作でオンライン アカウント。 詳細については、次を参照してください。[オンライン アカウントを作成](#BKMK_SECTION_CreateOnlineAccounts)します。  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>ダッシュ ボードからの電子メール アドレスと配布グループを管理します。  
 ダッシュ ボードから Exchange Online の電子メール アドレスと配布グループを管理することができます。 および電子メール アドレスでは、組織のインターネット ドメインを使用することができます。 すべての操作は、Office 365 へのログインしなくても、ダッシュ ボードから行うことができます。 (Windows Server Essentials ダッシュ ボードから配布グループの管理に使用する必要がありますします。 この機能は Windows Server Essentials でします。)詳細については、次を参照してください。[Exchange Online の電子メール アドレスの管理](#BKMK_SECTION_ManageEmailAddresses)と[Exchange Online の配布グループを管理](#BKMK_SECTION_ManageDistributionGroups)します。  
  
### <a name="manage-the-user-account-and-online-account-together"></a>ユーザー アカウントとオンライン アカウントを一緒に管理します。  
 アカウントのライフ サイクルを通して、ユーザー アカウントと共にオンライン アカウントを管理することができます。 ユーザー アカウントを無効にすると、オンライン アカウントも非アクティブに Microsoft Online Services でします。 ユーザー アカウントを削除する場合、オンライン アカウントも削除されます。 詳細については、次を参照してください。[オンライン アカウントの管理](#BKMK_SECTION_ManageOnlineAccounts)します。  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a>オンライン アカウントを作成します。  
 Office 365 とサーバーを統合した後、有利ダッシュ ボードからユーザー用の Microsoft Online Services アカウントを作成するのにです。 Ll するには、多くのオンライン アカウントの作成の柔軟性があります。 新しい Office 365 サブスクリプションがあれば、一括作成できますオンライン アカウントのすべてのユーザー。 Office 365 で、オンライン アカウントを作成済み、心配いりません。 新しいサーバーを設定すると、作成できる場合、ユーザー アカウント、サーバー上でオンライン アカウントをインポートすることによってします。 個々 のユーザー アカウントを作成するときに、または既存のユーザー アカウントにオンライン アカウントを追加する場合は、新規または既存のオンライン アカウントを割り当てることができます。  
  
 **ライセンスの要件**作成するオンライン アカウントごとにユーザー ライセンスは必要があります。 確認、**Office 365**ページで、ダッシュ ボード、Office 365 のサブスクリプションで利用可能なユーザー ライセンスの数を確認してください。 複数のユーザー ライセンスを追加する必要が場合は、そのためには、Office 365 で Office 365 サブスクリプションを開くにはすることができます。  
  
 **ユーザーのフォロー アップ**、ユーザーが自分のユーザー アカウントのパスワードを変更するには、次回のログイン時に必要なユーザー アカウントに対してオンライン アカウントを追加した後です。 新しいパスワードは、オンライン アカウントにすぐに同期します。 その後、そのオンライン ID を持つ Office 365 へのログインにパスワードを使用したことができます。  
  
> [!IMPORTANT]
>  決して変更しないように Office 365 でオンライン アカウントのパスワードをユーザーに強調します。 パスワードは、自分のユーザー アカウントのパスワードを変更した場合は、常に自動的に変更されます。 Office 365 でオンライン パスワードを変更した場合、パスワード同期は切断されます。  
  
 このセクションの手順を使用します。  
  
-   [既存のユーザー アカウントのオンライン アカウントを一括作成します。](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Microsoft Online Services アカウントからユーザー アカウントをインポートします。](#BKMK_ToImportUserAccounts)  
  
-   [それに割り当てられているオンライン アカウントを使用して、新しいユーザー アカウントを作成します。](#BKMK_ToCreateaNewUserAccount)  
  
-   [ユーザー アカウントにオンライン アカウントを割り当てる](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  表示は Windows Server Essentials を使用する場合は*Office 365 アカウント*の代わりに*Microsoft Online Services アカウント*これらの手順全体にわたってします。 プロセスは、同じですが、Windows Server Essentials での用語が変更されています。  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a>既存のユーザー アカウントのオンライン アカウントを一括作成するには  
  
1.  管理者は、サーバー ログオンし、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ダッシュ ボードを開く、**ユーザー**ページ。  
  
3.  **ユーザー タスク**、] をクリックして**追加の Microsoft オンライン アカウント**します。  
  
     **Microsoft Online Services アカウントの追加**ウィザードのページには、Microsoft オンライン アカウントを持っていないすべてのユーザー アカウントが表示されます。 既定では、すべてのアカウントが選択されており、Microsoft オンライン ID に対してユーザー名が提案 カスタム インターネット ドメインを Office 365 サブスクリプションにリンクしている場合、そのドメインは既定で使用されます。  
  
4.  **Microsoft Online Services アカウントの追加**] ページで、作成されるアカウントを確認します。 たとえば、既にオンライン ID が異なるオンライン アカウントを持っていることを確認の電子メール アドレスで使用するドメインが選択されているユーザーを確認します。 必要な変更のいずれかの作業が終了したら、クリックして**次**します。  
  
5.  **Microsoft Online Services ライセンスの割り当て**ページで、[Office 365 サービスが、ユーザーが使用されます。 クリックすると**次**、アカウントの作成が開始されます。  
  
    > [!NOTE]
    >  Office 365 でオンライン アカウントごとにサービス ライセンスが必要です。 確認、利用可能なライセンスし、必要な場合からライセンスを追加するサブスクリプションを開いて、**Office 365**ダッシュ ボードのページです。  
  
6.  今すぐであること、Microsoft オンライン アカウントをユーザーに通知します。 Office 365 にログインすることができます前に、ネットワーク ユーザー アカウントのパスワードを変更する必要があります。 手順については、次を参照してください。[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)します。  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a>新しい Microsoft オンライン アカウントの使用を開始するには  
  
1.  ネットワーク ユーザー アカウントを使用してコンピューターにログインします。  
  
2.  ユーザー アカウントのパスワードを変更します。 まず、Ctrl + Alt + Del キーを押し、**パスワードを変更する**します。  
  
     パスワードを変更するときに、パスワードは新しいオンライン アカウントに同期します。 Office 365 へのログインに同じパスワードを使えるようになりました。  
  
3.  [Office 365 へのログイン](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out)新しいオンライン ID とユーザー アカウントのパスワードを使用します。  
  
    > [!IMPORTANT]
    >  Office 365 でオンライン アカウントのパスワードは変更されません。 パスワード同期を無効になります。 ネットワーク ユーザー アカウントのパスワードを変更するたびに、オンライン パスワードが更新されます。  
  
###  <a name="BKMK_ToImportUserAccounts"></a>既存のオンライン アカウントからユーザー アカウントをインポートするには  
  
1.  ダッシュ ボードを開く、**ユーザー**ページ。  
  
2.  **ユーザー タスク**、] をクリックして**から Office 365 アカウントをインポート**します。  
  
     次のページには、サーバー上のユーザー アカウントがない、Office 365 サブスクリプション用のすべてのオンライン アカウントが表示されます。 既定では、すべてのアカウントが選択されており、ユーザー名に対してオンライン ID をお勧めします。  
  
3.  ユーザー アカウントを作成します。  
  
    1.  提案されたユーザー アカウントに必要な変更を加えます。  
  
    2.  必要に応じて、ユーザー アカウントに割り当てられる一時的なパスワードを表示するリンクをクリックします。 新しいアカウント名と一緒に一時パスワードをユーザーに提供する必要があります。  
  
         (アカウントを作成した後、わかりますこれらのパスワードがこのファイルの一覧: *SystemDrive*\Users\\*Office365admin*\\*NewServerUser*.txt 場所*Office365admin*は、サーバー上の Office 365 を管理するために使用するネットワーク アカウントと*NewServerUser*は新しいユーザー アカウント名です)。  
  
    3.  をクリックして**次**ユーザー アカウントを作成します。  
  
4.  新しいユーザー アカウントと一時パスワードに最初の時間 œ 用のサーバーにログインに使用してにログインした後、パスワードを変更する必要があるユーザーに知らせます。 手順については、ユーザーを参照してください。[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)します。  
  
     必ずが認識する、オンライン アカウントのパスワードは今後は、自分のユーザー アカウントと同期して、Office 365 でオンライン パスワードを変更しないでください。  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a>それに割り当てられているオンライン アカウントを使用して、新しいユーザー アカウントを作成するには  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**します。  
  
2.  **ユーザー タスク**、] をクリックして**ユーザー アカウントを追加**します。 追加するユーザー アカウントのウィザードが表示されます。  
  
3.  ユーザー アカウントを作成するための手順に従います。  
  
4.  **Microsoft Online Services アカウントの割り当て**] ページで、作成するか、新しいオンライン ユーザーのアカウントまたは既存のオンライン アカウントを割り当てます。  
  
    -   新しいオンライン アカウントを作成する] をクリックして**新しい Microsoft Online Services アカウントを作成し、このユーザー アカウントに割り当てる**、Microsoft Online Services アカウントの名前を入力し、(既定では、ユーザー名は使用はオンライン ID)。 をクリックして**次**します。  
  
    -   既存の Microsoft オンライン アカウントを割り当てるにはクリックして**既存の Microsoft Online Services アカウントをこのユーザー アカウントに割り当てる**、ドロップダウン リストから既存のアカウントを選択します。 をクリックして**次**します。  
  
    > [!NOTE]
    >  Windows Server Essentials では、Microsoft Online Services アカウントを Office 365 アカウント ウィザードとダッシュ ボード ラベルにおいてと呼びます。  
  
5.  ウィザードを完了するための手順に従います。  
  
6.  ログインできる Office 365 に、新しいオンライン アカウントにする前に、ユーザー アカウントのパスワードを変更する必要がありますユーザーに通知します。 手順については、次を参照してください。[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)します。  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>ユーザー アカウントにオンライン アカウントを割り当てる  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**します。  
  
2.  一覧で、ユーザー アカウントを右クリックし、をクリックして**Microsoft オンライン アカウントの割り当て**します。 割り当てる Microsoft Online Services アカウント ウィザードが表示されます。  
  
3.  既存のオンライン アカウントを割り当てるか、新しいユーザーを作成します。 新しいアカウントの既定のオンライン ID は、ユーザー名です。 をクリックして**次**ユーザー アカウントにオンライン アカウントを追加します。  
  
4.  ウィザードの最後のページで情報を確認し、をクリックして**閉じる**します。  
  
5.  ログインできる Office 365 に、新しいオンライン アカウントにする前に、ユーザー アカウントのパスワードを変更する必要がありますユーザーに通知します。 手順については、次を参照してください。[新しい Microsoft オンライン アカウントの使用を開始する](#BKMK_ToBeginUsingAnOnlineAccount)します。  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a>オンライン アカウントを管理します。  
 Windows Server Essentials でのユーザー アカウントにオンライン アカウントを追加する場合、アカウントのライフ サイクル全体で一緒に両方のアカウントを管理できます。  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a>オンライン アカウントの状態をについてください。  
 ユーザー アカウントに、Microsoft Online Services アカウントを割り当てると、アカウントの電子メール アドレスが表示されます、**Microsoft オンライン アカウント**の列に、**ユーザー**ダッシュ ボードのページです。 (Windows Server Essentials では、列のラベルは**Office 365 アカウント**.)  
  
-   電子メール アドレスの横にある青いアイコンは、オンライン アカウントがアクティブなを示します。 つまり、アカウントが現在の Office 365 ライセンスと、ユーザーは Office 365 へのログインにオンライン ID を使用することができます。  
  
-   示して、オンライン アカウントのメール アドレスの横にある灰色のアイコンは非アクティブな œ ライセンスがアクティブになるため、または、オンライン アカウントが割り当てられたになっています。 ユーザーのオンライン アカウントの割り当てを解除して、ライセンスが削除されると、アカウントを使用して Office 365 へのログインからユーザーをブロックします。 ただし、サーバーは、ユーザー アカウント名と Office 365 のメール アドレスの間のマッピングを維持します。  
  
###  <a name="BKMK_UnassignOnlineAccount"></a>オンライン アカウントへのアクセスを制限します。  
 ユーザーが退職する、または Office 365 サービスにユーザーのアクセスを制限する場合はどうすればですか。 なら、ユーザーのオンライン アカウントと Windows Server Essentials でユーザー アカウントを管理する 3 つのオプション。  
  
-   **オンライン アカウントの割り当てを解除**ですか?Office 365 を使用して、サーバー上のリソースへのアクセスを妨げることがなく、ユーザーが引き続きする場合は、オンライン アカウントの割り当てを解除する必要があります。 Office 365 ライセンスが解除されてし、Office 365 へのログインからユーザーをブロックします。 ただし、サーバーは、ユーザー アカウント名と Office 365 のメール アドレスの間のマッピングを維持します。 手順については、次を参照してください。[ユーザー アカウントからオンライン アカウントの割り当てを解除する](#BKMK_ToUnassignAnOnlineAccount)します。  
  
-   **ユーザー アカウントを非アクティブ化**ですか?一時的または永続的に、従業員が退職したため、ユーザー アカウントを無効化する場合、ユーザーのオンライン アカウントも非アクティブにします。 オンライン アカウントを使用することはできませんが、メールも含めて、ユーザー データは Microsoft Online Services に保持されます。 手順については、次を参照してください。[ユーザー アカウントを非アクティブ化](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6)で[ユーザー アカウントの管理](Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
-   **ユーザー アカウントを削除する**ですか?ユーザー アカウントを削除する場合、オンライン アカウントが Microsoft Online Services からも削除します。 手順については、次を参照してください。[ユーザー アカウントの削除](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove)で[ユーザー アカウントの管理](Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
    > [!WARNING]
    >  オンライン アカウントが削除されると、ユーザー データが対象のデータ保持ポリシーの Microsoft Online Services に注意してください。 を従業員が退職した後、ユーザーのユーザー データを保持する必要がある場合は、削除することではなく、ユーザー アカウントを非アクティブ化します。  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a>ユーザー アカウントからオンライン アカウントの割り当てを解除するには  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**します。  
  
2.  一覧で、ユーザー アカウントを右クリックし、をクリックして**Microsoft オンライン アカウントの割り当てを解除**(Windows Server Essentials では、をクリックして**Office 365 アカウントの割り当てを解除**)。  
  
3.  確認のプロンプトで次のようにクリックします。**はい**します。  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a>Exchange Online の電子メール アドレスを管理します。  
 電子メール アドレスを Windows Server Essentials でのユーザーのオンライン アカウントを追加するには、オンライン Exchange に複数の電子メール アドレスに電子メールを受信するユーザーを許可できます。  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a>その他のメール アドレス、ユーザーの Microsoft オンライン アカウントを追加するには  
  
1.  Windows Server Essentials ダッシュ ボード] をクリックして**ユーザー**します。  
  
2.  一覧で、ユーザー アカウントを右クリックし、をクリックして**アカウント プロパティの表示**します。  
  
3.  **Microsoft online**アカウント プロパティのタブ (または**Office 365** ] タブの [Windows Server Essentials で)、] をクリックして**追加**します。  
  
4.  新しい電子メールのエイリアスを入力し、電子メール ドメインを選択します。  
  
5.  をクリックして**OK** 2 回クリックします。  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a>配布グループ Exchange Online の管理 (Windows Server Essentials のみ)  
 Office 365 と Windows Server Essentials サーバーを統合した後は、作成し、Windows Server Essentials ダッシュ ボードから Exchange Online の配布グループを管理します。 紹介する実行、**配布グループ**] タブに追加されている、**ユーザー**ページ。 このタブは、Exchange Online サブスクリプションがある場合のみ表示されます。 この機能では、Windows Server Essentials で使用できません。  
  
 次の手順に従います。  
  
-   [配布グループを追加します。](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [配布グループのメンバーを変更します。](#BKMK_ChangeGroupMembers)  
  
-   [ユーザーの配布グループのメンバーシップを変更します。](#BKMK_EditUserMemberships)  
  
-   [配布グループを削除します。](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a>配布グループを追加するには  
  
1.  Windows Server essentials ダッシュ ボードで、をクリックして**ユーザー**、クリックして、**配布グループ**] タブ。  
  
2.  **配布グループ タスク**、] をクリックして**配布グループを追加**します。  
  
     追加の配布グループの新規作成ウィザードが表示されます。  
  
3.  **新しい配布グループの追加**] ページで、次の情報を入力してをクリックして**次**:  
  
    -   新しい配布グループのグループ名、説明 (オプション)、および電子メールのエイリアスを入力します。  
  
    -   既定では、配布グループは、組織の外部の人から電子メールを受信できます。 これを許可する場合は、そのオプションをオフにします。  
  
4.  **グループ メンバー追加**] ページで、使用、**追加**に割り当てられている、オンライン アカウントを持っているアクティブなユーザー アカウントを追加するボタンをクリックし、その他の配布グループを新しい配布グループ。 をクリックして**次**します。  
  
     新しい配布グループは、Exchange Online で作成されます。  
  
###  <a name="BKMK_ChangeGroupMembers"></a>配布グループのメンバーを変更するには  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**、クリックして、**配布グループ**] タブ。  
  
2.  一覧で、配布グループを右クリックし、をクリックして**グループ メンバーシップの変更**します。  
  
3.  使用して、**追加**と**削除**ボタンを追加または配布グループからのアクティブなオンライン アカウントを削除します。 をクリックして**次**Exchange online 配布グループのメンバーシップを更新します。  
  
###  <a name="BKMK_EditUserMemberships"></a>ユーザーの配布グループ メンバーシップを変更するには  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**します。  
  
2.  一覧で、ユーザー アカウントを右クリックし、をクリックして**アカウント プロパティの表示**します。  
  
3.  ユーザー アカウントのプロパティ] をクリックして、**配布グループ**タブをクリックし、をクリックして**編集**します。  
  
4.  **グループ メンバーシップの編集**ボックスで使用して、**追加**と**削除**ボタンを追加または配布グループをユーザー アカウントから削除し、クリックして**閉じる**します。  
  
5.  をクリックして**OK**更新されたユーザー アカウントのプロパティを保存します。  
  
###  <a name="BKMK_RemoveDistributionGroup"></a>配布グループを削除するには  
  
1.  ダッシュ ボードで、をクリックして**ユーザー**、クリックして、**配布グループ**] タブ。  
  
2.  一覧で、配布グループを右クリックし、をクリックして**グループを削除**します。  
  
3.  確認のプロンプトで次のようにクリックします。**グループの削除**します。  
  
     配布グループは、Exchange Online から削除されます。  
  
## <a name="see-also"></a>参照してください。  
  
-   [ユーザー アカウントを管理します。](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Office 365 を管理します。](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services を管理します。](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
