---
title: Windows Server Essentials でのリモート Web アクセスの管理
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f3ea40fa-b6ba-4d66-b754-221ca6271387
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 56bfd8d9860ad571265980e859a09914fb4f1b9c
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180938"
---
# <a name="manage-remote-web-access-in-windows-server-essentials"></a>Windows Server Essentials でのリモート Web アクセスの管理

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 Windows Server Essentials のリモート Web アクセス、または Windows server Essentials Experience 役割がインストールされた Windows Server 2012 R2 では、インターネットに接続していればどこからでも、ほとんどすべてのデバイスでアプリケーションやデータにアクセスするための、効率的でタッチ操作に適したブラウザーエクスペリエンスを提供します。 リモート Web アクセス機能を使用するには、まず Anywhere Access のセットアップ ウィザードを使用してこの機能を有効にし、次にルーターとドメインをセットアップする必要があります。

## <a name="in-this-topic"></a>このトピックの内容

-   [リモート Web アクセスの有効化と構成](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)

-   [ルーターのセットアップ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)

-   [ドメイン名のセットアップ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_3)

-   [リモート Web アクセスのカスタマイズ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_4)

-   [リモート Web アクセスのトラブルシューティング](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_5)

##  <a name="turn-on-and-configure-remote-web-access"></a><a name="BKMK_1"></a>リモート Web アクセスをオンにして構成する
 次のトピックでは、リモート Web アクセスを有効にして構成する方法について説明します。

-   [リモート Web アクセスの概要](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)

-   [リモート Web アクセスの有効化](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)

-   [地域の変更](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Region)

-   [リモート Web アクセスのアクセス許可の管理](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManagePerms)

-   [リモート Web アクセスの保護](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SecureRWA)

-   [リモート Web アクセスと VPN ユーザーの管理](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManageRWAVPN)

###  <a name="remote-web-access-overview"></a><a name="BKMK_Overview"></a>リモート Web アクセスの概要
 オフィスから離れているときは、web ブラウザーを開いて、インターネットにアクセスできる任意の場所からリモート Web アクセスにアクセスすることができます。 リモート Web アクセスでは、次のことができます。

- サーバー上の共有ファイルやフォルダーにアクセスします。

- ネットワーク上のサーバーやコンピューターにアクセスします。 つまり、オフィスで作業するのと同じように、ネットワークに接続されたコンピューターのデスクトップにアクセスできます。

  リモート Web アクセスは、既定では有効になっていません。 Anywhere Access のセットアップ ウィザードを実行すると、ルーターおよびインターネットへの接続のセットアップが試行されます。 リモート Web アクセスが有効になったら、サーバーのドメイン名を設定し、リモート Web アクセスをカスタマイズできます。 ルーターを変更した場合は、ルーターを再度セットアップすることもできます。

  リモート Web アクセスにアクセスするためのアクセス許可は、新しいユーザーアカウントを追加するときに自動的には付与されません。 ユーザー アカウントを追加するときに、共有フォルダー、メディア ライブラリ、コンピューター、ホーム ページ リンク、およびサーバー ダッシュボードへのアクセスを許可することができます。 また、リモート Web アクセスを使用することをユーザーに許可しないように指定することもできます。

  [リモート Web アクセス] 設定は、Windows Server Essentials ダッシュボードの [**ユーザー** ] タブで、各ユーザーアカウントに対して表示されます。 リモート Web アクセス設定を変更するには、ユーザーアカウントを右クリックし、[**アカウントのプロパティの表示**] をクリックします。

###  <a name="turn-on-remote-web-access"></a><a name="BKMK_TurnOnRWA"></a>リモート Web アクセスをオンにする
 リモート Web アクセスを有効にするには、サーバー ダッシュボードから Anywhere Access のセットアップ ウィザードを実行します。

##### <a name="to-turn-on-remote-web-access"></a>リモート Web アクセスを有効にするには

1.  ダッシュボードを開きます。

2.  **[設定]** をクリックし、**[Anywhere Access]** タブをクリックします。

3.  **[Configure]\(構成\)** をクリックします。 Anywhere Access のセットアップ ウィザードが表示されます。

4.  **[有効にする Anywhere Access の機能を選択します]** ページで、**[リモート Web アクセス]** チェック ボックスを選択します。

5.  指示に従ってウィザードを完了します。

###  <a name="change-your-region"></a><a name="BKMK_Region"></a>リージョンを変更する
 ネットワーク管理者は、Windows Server Essentials の地域の設定を変更できます。

##### <a name="to-change-the-region-setting"></a>地域の設定を変更するには

1.  Windows Server Essentials に接続されているコンピューターで、ダッシュボードを開きます。

2.  **[設定]** をクリックします。

3.  **[全般]** タブで、**[サーバーの国/地域]** セクションのドロップダウン リストをクリックします。

4.  ドロップダウン リストから、新しい地域を選択し、**[適用]** をクリックして新しい地域の設定を受け入れます。

###  <a name="manage-remote-web-access-permissions"></a><a name="BKMK_ManagePerms"></a>リモート Web アクセスのアクセス許可を管理する
 Windows Server Essentials でユーザー アカウントを追加する場合、既定では、新しいユーザーにはリモート Web アクセスの使用が許可されます。 ユーザーアカウントに対してリモート Web アクセスを許可しないことを選択し、ユーザーがリモート Web アクセスを使用する必要があることを確認した場合は、ユーザーアカウントのプロパティを更新できます。

##### <a name="to-manage-remote-web-access-permissions-for-a-user-account"></a>ユーザー アカウントのリモート Web アクセスへのアクセス許可を管理するには

1. ダッシュボードにログオンし、**[ユーザー]** をクリックします。

2. 管理するユーザー アカウントをクリックし、**[タスク]** ウィンドウの **[アカウント プロパティの表示]** をクリックします。

3. **[プロパティ]** ダイアログ ボックスで、**[Anywhere Access]** タブをクリックします。

4. **[Anywhere Access]** タブで、**[リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする]** チェック ボックスをオンにして、リモート Web アクセスを使用したサーバーへの接続をユーザーに許可します。

5. [**適用**] をクリックし、[**OK**] をクリックします。

   詳細については、「[ユーザーアカウントの管理](Manage-User-Accounts-in-Windows-Server-Essentials.md)」を参照してください。

###  <a name="secure-remote-web-access"></a><a name="BKMK_SecureRWA"></a>リモート Web アクセスをセキュリティで保護する
 Windows Server Essentials は、ソフトウェアと Web ブラウザーの間で交換される情報を保護するためにセキュリティ証明書を使用します。 コンピューターにコネクタ ソフトウェアをインストールするときに、Windows Server Essentials のセキュリティ証明書が、コンピューター上の信頼された証明書の一覧に追加されます。 オフィス以外の場所からリモート Web アクセスに接続する最適な方法は、コネクタ ソフトウェアがインストールされているポータブル コンピューターを使用することです。

> [!WARNING]
>  公共の場所または信頼されていない他のコンピューターからリモート Web アクセスを使用するユーザーは、コンピューターの前から離れる前やセッションを終了したときに、必ず Web サイトからログオフする必要があります。

###  <a name="manage-remote-web-access-and-vpn-users"></a><a name="BKMK_ManageRWAVPN"></a>リモート Web アクセスと VPN ユーザーの管理
 VPN を使用すると、Windows Server Essentials に接続し、サーバーに保存されているすべてのリソースにアクセスすることができます。 これが特に役立つのは、クライアント コンピューターに設定されているネットワーク アカウントを使用して、ホストされている Windows Server Essentials サーバーに VPN 経由で接続できる場合です。 ホストされている Windows Server Essentials サーバーで新しく作成されたユーザー アカウントはすべて、クライアント コンピューターへの初回ログオン時に VPN を使用する必要があります。

##### <a name="to-set-vpn-and-remote-web-access-permissions-for-network-users"></a>ネットワーク ユーザーの VPN とリモート Web アクセスのアクセス許可を設定するには

1.  ダッシュボードを開きます。

2.  ナビゲーション バーで **[ユーザー]** をクリックします。

3.  ユーザー アカウントの一覧から、リモートでデスクトップにアクセスするアクセス許可を付与するユーザー アカウントを選択します。

4.  [**ユーザーアカウント \> タスクの<** ] ウィンドウで、[**プロパティ**] をクリックします。

5.  **<ユーザーアカウントの \> プロパティ**] で、[ **Anywhere Access** ] タブをクリックします。

6.  **[Anywhere Access]** タブで、次の手順を実行します。

    1.  VPN を使用してユーザーがサーバーに接続できるようにするには、[**仮想プライベート ネットワーク (VPN) を許可する**] チェック ボックスをオンにします。

    2.  リモート Web アクセスを使用してユーザーがサーバーに接続できるようにするには、[**リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする**] チェック ボックスをオンにします。

7.  [**適用**] をクリックし、[**OK**] をクリックします。

##  <a name="set-up-your-router"></a><a name="BKMK_2"></a>ルーターをセットアップする
 リモート Web アクセスを使用するようにサーバーを構成するときには、Anywhere Access のセットアップ ウィザードによってルーターのセットアップが行われます。 ルーターを交換したり、ルーターの設定を変更したりした場合は、ルーターのセットアップ ウィザードを再実行する必要があります。 詳細については、次のトピックを参照してください。

-   [ルーターのセットアップ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpRouter)

-   [ルーターの交換](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ReplaceRouter)

-   [定義済みのネットワークの場所](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_NetworkLocation)

-   [リモート デスクトップ サービス ActiveX コントロールの有効化](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ActiveX)

###  <a name="set-up-your-router"></a><a name="BKMK_SetUpRouter"></a>ルーターをセットアップする
 Windows Server Essentials は、この手順の間に UPnP コマンドを使用してルーターを自動的に構成しようと試みます。 このためには、ルーターが UPnP 標準をサポートしていて、ルーターで UPnP 設定が有効になっている必要があります。

> [!NOTE]
> ネットワーク構成は、Windows Server Essentials でサポートされるネットワーク要件に適合している必要があります。 ネットワーク上に存在するルーターは 1 つでなければなりません。

 ルーターがドメイン名のセットアップ ウィザードによってセットアップされない場合は、手動でポート 443 を転送する必要があります。 ルーターでポートフォワーディングを設定する方法については、 [Small Business Server フォーラム](https://docs.microsoft.com/answers/topics/windows-small-business-server.html)を参照してください。

###  <a name="replace-a-router"></a><a name="BKMK_ReplaceRouter"></a>ルーターを交換する
 製造元の指示に従ってルーターを交換し、ルーターのセットアップウィザードを実行して新しいルーターを構成します。

##### <a name="to-set-up-your-new-router"></a>新しいルーターをセットアップするには

1.  Windows Server Essentials ダッシュボードで **[設定]** をクリックします。

2.  **[Anywhere Access]** タブをクリックし、**[ルーター]** セクションで **[セットアップ]** をクリックします。 ルーターのセットアップ ウィザードが起動します。

3.  ウィザードの指示に従って、新しいルーターのセットアップを完了します。

###  <a name="network-location-defined"></a><a name="BKMK_NetworkLocation"></a>定義されたネットワークの場所
 ネットワークの場所は、ネットワークに接続するときに Windows によって適用されるネットワーク設定のコレクションです。 この設定は、使用するネットワークの種類によって異なり、カスタマイズすることができます。 ネットワークの場所の設定によって、特定の機能 (ファイルとプリンターの共有、ネットワーク探索、およびパブリック フォルダーの共有など) が有効または無効になるかどうかが決まります。 ネットワークの場所は、異なるネットワークに接続する必要がある場合に役立ちます。

 たとえば、自宅と職場の両方で使用するラップトップ コンピューターを所有している場合があります。 オフィスでは、オフィス ネットワークに接続します。 帰宅すると、ラップトップを使用し、ホーム サーバーに保存されているビデオや音楽にアクセスして再生します。 新しいネットワークに接続して場所の種類を指定すると、Windows により、その場所の種類に対して事前設定されているネットワーク プロファイルが割り当てられます。 次回にそのネットワークに接続すると、Windows はネットワークを認識し、正しい設定が自動的に割り当てられます。 これにより、コンピューター上の情報を保護するのに役立つセキュリティ層が追加され、その場所に必要なネットワーク機能のみが有効になります。

 ネットワークの場所は、次の 4 種類があります。

-   **ホーム ネットワーク** 自宅のネットワーク、またはネットワーク上のユーザーとデバイスが既知であり信頼できる場合は、このネットワークを選択します。 ホーム ネットワーク上のコンピューターは、ホーム グループに属することができます。 ホーム ネットワークではネットワーク探索が有効になります。これにより、ネットワーク上の他のコンピューターやデバイスを参照することができ、自分のコンピューターも他のネットワーク ユーザーから参照されます。

-   **社内ネットワーク** 小規模なオフィスやその他の職場のネットワークの場合、このネットワークを選択します。 ネットワーク探索を使用すると、ネットワーク上の他のコンピューターやデバイスを参照することができ、自分のコンピューターも他のネットワーク ユーザーから参照されます。この機能は既定で有効になっていますが、ホーム グループを作成したりホーム グループに参加したりすることはできません。

-   **パブリック ネットワーク** 公共の場所 (喫茶店や空港など) では、このネットワークを選択します。 この場所は、自分のコンピューターが他のコンピューター上に表示されないようにして、インターネット上の悪意のあるソフトウェアからコンピューターを保護するように設計されています。 ホーム グループは、パブリック ネットワークでは使用できません。また、ネットワーク探索は無効になります。 ルーターを使用しないでインターネットに直接接続している場合、またはモバイル ブロード バンド接続を使用している場合も、このオプションを選択する必要があります。

-   **ドメイン** 職場などでドメインを使用する場合、このネットワークを選択します。 この種類のネットワークの場所は、ネットワーク管理者によって管理されており、選択または変更することはできません。

###  <a name="enable-remote-desktop-services-activex-controls"></a><a name="BKMK_ActiveX"></a>リモートデスクトップサービス ActiveX コントロールを有効にする
 リモートデスクトップサービス ActiveX コントロールを使用すると、リモート Web アクセスを使用して、別のコンピューターからインターネット経由で自宅または会社のコンピューターにアクセスできます。

##### <a name="to-enable-remote-desktop-services-activex-controls"></a>リモート デスクトップ サービス ActiveX コントロールを有効にするには

1.  Internet Explorer で、**[ツール]** をクリックし、**[インターネット オプション]** をクリックします。

2.  **[セキュリティ]** タブで、**[レベルのカスタマイズ]** をクリックします。

3.  **[ActiveX コントロールとプラグイン]** セクションで、次の操作を実行します。

    1.  **[署名済み ActiveX コントロールのダウンロード]** で、**[ダイアログを表示する]** をクリックします。

    2.  **[ActiveX コントロールとプラグインの実行]** で、**[有効にする]** をクリックします。

4.  **[OK]** を 2 回クリックし、変更を受け入れてダイアログ ボックスを閉じます。

##  <a name="set-up-your-domain-name"></a><a name="BKMK_3"></a>ドメイン名を設定する
 リモート Web アクセスを有効にしたら、Windows Server Essentials が実行されているサーバーのドメイン名をセットアップできます。 この手順は、リモート コンピューターからリモート Web アクセスを使用する予定がある場合に必要です。 詳細については、次のトピックを参照してください。

-   [ドメイン名の概要](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_DNOverview)

-   [Microsoft の個人用ドメイン名の概要](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_PersonalizedNames)

-   [新規または既存のドメイン名の使用](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UseNewName)

-   [ドメイン名のセットアップ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpName)

-   [ドメイン ネーム サービス プロバイダーの選択](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseProvider)

-   [ドメイン名の選択](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseDomainName)

-   [ドメイン名プレフィックスの選択](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Prefixes)

-   [ドメイン名拡張子の選択](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Extension)

-   [ドメイン ネーム サービスの更新またはアップグレード](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UpdateService)

-   [サーバーの証明書のエクスポートまたはインポート](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ExportCert)

-   [手動によるドメイン名のセットアップ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetNameManually)

-   [ドメイン ネーム サービス プロバイダーの確認](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Find)

###  <a name="domain-names-overview"></a><a name="BKMK_DNOverview"></a>ドメイン名の概要
 ドメイン名は、インターネット上のサーバーを一意に識別します。 ドメイン名は少なくとも 2 つの部分から構成されています。トップ レベルのドメイン名 (TLD) と第 2 レベルのドメイン名です。 たとえば、contoso.com では、com は TLD で、contoso は第2レベルのドメイン名です。

 オフィス以外の場所にいても、ドメイン名を使用して、ネットワーク内のサーバーまたはコンピューター上にある共有ファイルにアクセスできます。 離れた場所からサーバーを管理することもできます。 たとえば、サーバーに contoso.com を登録します。 オフィス以外の場所で、ラップトップの Web ブラウザーを開いてアドレス テキスト ボックスに **contoso.com** と入力し、Windows Server Essentials で設定したリモート Web アクセスのインスタンスに接続することができます。

###  <a name="understand-microsoft-personalized-domain-names"></a><a name="BKMK_PersonalizedNames"></a>Microsoft の個人用ドメイン名について
 Microsoft の個人用ドメイン名には、次の機能が含まれます。

- リモート Web アクセスのカスタムドメイン名 (*たとえば、remotewebaccess.com)。* 使用するドメイン名は、パブリック IP アドレスに関連付けられます。

- DNS 動的更新プロトコルサービス。パブリック IP アドレスが変更された場合に、ドメイン名を使用してリモート Web アクセスが中断されることはありません。 通常、組織のブロードバンド接続用のインターネットサービスプロバイダー (Isp) は、変化する可能性のある動的なパブリック IP アドレスを提供します。

- ドメイン名に関連付けられている信頼された証明書。

  Microsoft の個人用ドメイン名をサーバーと統合するには、Microsoft アカウント (旧称: Windows Live ID) が必要です。 Microsoft アカウントを持っていない場合、 [Microsoft Hotmail](https://login.live.com/) Web サイトでサインアップすることができます。

> [!IMPORTANT]
>  Windows Live では、Microsoft アカウントのパスワードにサーバーがサポートしていない特殊文字を使用できます。 Microsoft の個人用ドメインを使用する場合、Microsoft アカウントのパスワードに、サーバーがサポートする文字のみが含まれていることを確認してください。 サーバーでは、$、/、'、および % の使用をサポートしていません。

###  <a name="use-a-new-or-existing-domain-name"></a><a name="BKMK_UseNewName"></a>新規または既存のドメイン名を使用する
 Windows Server Essentials を実行するサーバーでドメイン名を自動的にセットアップするには、ドメイン名のセットアップ ウィザードに一覧表示されているドメイン ネーム サービス プロバイダーを使用する必要があります。 新しいドメイン名を取得するか、または既存のドメイン名を使用することもできます。 次のいずれかの操作を行います。

-   ウィザードに一覧表示されているいずれかのドメイン ネーム サービス プロバイダーから新しいドメイン名を取得する場合は、**[新しいドメイン名をセットアップする]** をクリックします。

-   サポートされているいずれかのドメイン ネーム サービス プロバイダーから購入した既存のドメイン名がある場合は、ドメイン名のセットアップ ウィザードを使用して、サーバーのドメイン名をセットアップできます。 **[既に所有しているドメイン名を使用する]** をクリックし、**[ドメイン名のセットアップ]** テキスト ボックスにドメイン名を入力します。 ドメイン名を購入するために使用したユーザー名とパスワードを指定する必要があります。

-   Windows Server Essentials ではサポートされていないドメイン ネーム サービス プロバイダーから購入した既存のドメイン名があり、ドメイン名のセットアップ ウィザードを使用してサーバーのドメイン名をセットアップする場合は、ウィザードに一覧表示されたドメイン ネーム サービス プロバイダーのいずれかにドメイン名を転送することができます。 [**既に所有しているドメイン名を使用する**] をクリックし、[**ドメイン**名] テキストボックスにドメイン名を入力して、ドメインネームサービスプロバイダーの web サイトの指示に従ってドメイン名を転送します。

###  <a name="set-up-a-domain-name"></a><a name="BKMK_SetUpName"></a>ドメイン名を設定する
 リモート Web アクセスを有効にすると、サーバーのインターネット ドメイン名をセットアップできます。

##### <a name="to-set-up-or-manage-an-internet-domain-name"></a>インターネット ドメイン名をセットアップまたは管理するには

1.  ダッシュボードを開きます。

2.  **[サーバーの設定]** をクリックし、**[Anywhere Access]** タブをクリックします。

3.  **[ドメイン名]** セクションで、**[セットアップ]** をクリックします。

4.  指示に従ってウィザードを完了します。 ドメイン名と証明書を所有していない場合、ウィザードを使用すると、ドメイン名と証明書を購入するドメイン ネーム プロバイダーを見つけるのに役立ちます。または、Microsoft の個人用ドメイン名を取得することもできます。

###  <a name="choose-a-domain-name-service-provider"></a><a name="BKMK_ChooseProvider"></a>ドメインネームサービスプロバイダーの選択
 使用するドメイン名拡張子をサポートしているドメイン ネーム サービス プロバイダーを選択する必要があります。 ドメイン名のセットアップウィザードには、各プロバイダーの web サイトへのリンクと共に使用できる、修飾されたプロバイダーの一覧が含まれています。 プロバイダーによって提供されるサービスと価格に関する情報を取得するには、各プロバイダーの名前の横にある [**詳細情報**] リンクをクリックします。

> [!NOTE]
>  ドメイン ネーム サービス プロバイダーには、世界各国の幅広い地域でサービスを提供しているプロバイダーもあれば、より小さな市場を対象にしているプロバイダーもあります。 このため、一部のプロバイダーでは、ユーザーが使用する言語に翻訳された Web サイトが提供されていない可能性があります。

 ドメイン ネーム サービス プロバイダーからドメイン名を購入するときに、ドメイン ネーム システム (DNS) 動的更新プロトコル サービスの購入も検討することが必要になる場合があります。 DNS 動的更新プロトコルは、ローカル ネットワークの IP アドレスが絶えず変更されている場合でも、任意のユーザーがインターネットからそのネットワーク上のリソースにアクセスできるサービスです。 または、IP アドレスが変更されないように、インターネット サービス プロバイダー (ISP) から静的 IP アドレスを購入することもできます。

###  <a name="choose-a-domain-name"></a><a name="BKMK_ChooseDomainName"></a>ドメイン名を選択してください
 ビジネス サーバーを一意に識別する名前を選択します。 たとえば、会社名が Contoso Ltd の場合、インターネット上のホームまたはビジネス サーバーを一意に識別するために Contoso を選択できます。 このドメイン名を使用できない場合は、この名前の別のバリエーションを試すか、まったく異なる名前を試してみてください。

 名前を入力する際の制限は次のとおりです。

-   最大 63 文字

-   文字 (英語またはユーザーの地域の文字)、数字、またはハイフン (-)。 名前の先頭と末尾は、文字または数字にする必要があります。

    > [!NOTE]
    >  ドメイン名では大文字と小文字が区別されません。

###  <a name="choose-a-domain-name-prefix"></a><a name="BKMK_Prefixes"></a>ドメイン名のプレフィックスを選択してください
 ドメイン名は階層的なラベルで構成されます。

 **トップレベル ドメイン拡張子**は、ドメイン名の一番右側のラベルです。 たとえば、www contoso.com の場合、 \. com はトップレベルのドメイン名拡張子です。

 **第 2 レベル ドメイン名**は、トップレベル ドメイン名拡張子の隣にあるラベルです。 第 2 レベル ドメイン名は多くの場合、会社名、製品、またはサービスに基づいて作成されます。 たとえば、www contoso.com で \. は、contoso は第2レベルのドメイン名であり、会社名 Contoso 製薬用に選択されています。 第 2 レベル ドメインはホスト名と呼ばれることもあり、IP アドレスが関連付けられています。

 **ドメイン名プレフィックス**は、サブドメインを識別します。 サブドメイン名を使用して、サービス、デバイス、または地域を識別することができます。 たとえば、Contoso Pharmaceuticals では、リモート ユーザーにリモート Web アクセスへのログオンを許可しつつ、その Web サイトを一般公開しないようにする必要があります。そのため、適切なアクセス許可を持つユーザーのみが Web サイトにアクセスできるように、サブドメインを作成します。 Contoso Pharmaceuticals は、サブドメインとして remote.contoso.com をセットアップします。remote はドメイン名プレフィックスです。

> [!TIP]
>  ドメイン名のプレフィックスとして、既定値である **[Remote]** を使用することをお勧めします。

###  <a name="choose-a-domain-name-extension"></a><a name="BKMK_Extension"></a>ドメイン名拡張子の選択
 インターネットの Web サイトのドメイン名を選択するときは、使用するドメイン名拡張子も指定する必要があります。 この拡張子は、任意のドメイン名の最後のピリオドの後に続く文字で識別されます。 (拡張機能の正式な用語は、トップレベルドメインまたは TLD です)。

 使用できる主なドメイン拡張子には、汎用と国コードの 2 種類があります。

#### <a name="generic-top-level-domains"></a>汎用トップレベル ドメイン
 汎用ドメイン拡張子は 3 文字以上の長さで、通常、特定の種類の組織によって使用されます。

 **汎用トップレベル ドメインの例**

|ドメイン拡張子|[説明]|
|----------------------|-----------------|
|.com|通常は商業組織によって使用されますが、だれでも使用できます。|
|.net|ネットワーク インフラストラクチャ サービスを提供する企業向けです。|
|.org|本来は、非営利機関や、他の汎用トップレベル ドメインのカテゴリに分類されない企業によって使用されます。 だれでも使用できます。|
|.edu|教育機関のみに使用が制限されています。|

#### <a name="country-code-top-level-domains"></a>国コード トップレベル ドメイン
 これらのドメイン拡張子の長さは 2 文字です。 それぞれのコードに関連付けられている国または地域の組織が対象となります。 一部の国コード トップレベル ドメインは、その国または地域の住民のみが使用できます。 それら以外は、だれでも使用できます。

 **国コード トップレベル ドメインの例**

|ドメイン拡張子|[説明]|
|----------------------|-----------------|
|.ca|カナダの Web サイトで使用されます。|
|.cn|中国の Web サイトで使用されます。|
|.de|ドイツの Web サイトで使用されます。|
|.co.uk|イギリスの Web サイトで使用されます。|

 トップレベル ドメインの完全な一覧を確認するには、 [Internet Assigned Numbers Authority の Web サイト](https://go.microsoft.com/fwlink/?LinkId=117438)を参照してください。

#### <a name="if-a-domain-extension-is-not-available-to-select-in-the-set-up-domain-name-wizard"></a>ドメイン名のセットアップ ウィザードで希望するドメイン拡張子を選択できない場合
 ドメイン名のセットアップ ウィザードを実行すると、ウィザードによりシステム情報が確認され、国または地域が特定されます。 次に、そのエリアの提携プロバイダーがサポートするドメイン拡張子のみが表示されます。 希望するドメイン拡張子が一覧に表示されない場合は、別のドメイン拡張子を選択して続行する必要があります。 ウィザードによって返される一覧から拡張子を選択してください。

###  <a name="update-or-upgrade-your-domain-name-service"></a><a name="BKMK_UpdateService"></a>ドメインネームサービスの更新またはアップグレード
 ドメイン名を購入しても証明書を購入していない場合は、ドメイン ネーム サービスの更新やアップグレードが必要になることがあります。 ドメイン ネーム サービス プロバイダーから提供される、ドメイン名の証明書が必要です。

> [!NOTE]
>  ドメイン ネーム サービス プロバイダーと連携して、必要な証明書の種類を決定してください。 提供されている安価な証明書のいずれかを使用できます。 ただし、高レベルのセキュリティを確保する証明書の場合は、ドキュメントと機能を確認して、ビジネスのニーズを適切に満たすかどうかを判断する必要があります。

###  <a name="export-or-import-your-certificate-on-your-server"></a><a name="BKMK_ExportCert"></a>サーバーでの証明書のエクスポートまたはインポート
 証明書のバックアップ コピーを作成するか、証明書を別のサーバーで使用する場合は、証明書をエクスポートする必要があります。 証明書をエクスポートする方法の詳細については、「 [証明書をエクスポートする](https://go.microsoft.com/fwlink/p/?LinkId=214362)」を参照してください。

###  <a name="set-up-a-domain-name-manually"></a><a name="BKMK_SetNameManually"></a>ドメイン名を手動で設定する
 このオプションを選択すると、サーバーによるドメイン名の監視と管理は行われなくなります。構成の問題があっても警告は表示されません。 次のいずれかに当てはまる場合は、必要に応じてこのオプションを使用することも検討してください。

- お住まいの国または地域に対応するパートナー ドメイン ネーム プロバイダーが表示されない場合。

- 表示されたパートナー ドメイン プロバイダーが、お使いのドメイン名拡張子をサポートしていない場合。

- 現在パートナーではないドメイン ネーム プロバイダーから取得した既存のドメイン名があり、そのドメイン名を Windows Server Essentials でサポートされるドメイン ネーム プロバイダーに移管したくない場合。

- 希望するドメイン名拡張子がウィザードで表示されないが、現在パートナーではないドメイン ネーム プロバイダーがその拡張子に対応している場合。

  ドメイン名を手動で設定する場合は、ドメインネームサービスプロバイダーと協力して、ドメインの A レコードを作成します。

##### <a name="to-create-an-a-record"></a>A レコードを作成するには

1.  リモートなどのホスト名を決定します。 これはドメイン名のプレフィックスです。 ドメイン名のプレフィックスとドメイン名を使用して、リモート Web アクセスログオンページを開くための URL を定義します。たとえば、のように **http://remote.contoso.com** なります。

2.  ドメインネームサービスプロバイダーの構成ダッシュボード (通常は web ページ) で、手順1で決定したホスト名の A レコードを作成します。 A レコードで指定した IP アドレスが、ルーターの WAN 側 (インターネットに接続している側) の IP アドレスであることを確認します。 WAN 側の IP アドレスを確認するには、ルーターの説明書を参照してください。

3.  インターネット サービス プロバイダー (ISP) に問い合わせて、ネットワーク用に静的 IP アドレスを購入することをお勧めします。 これにより、IP アドレスが変更され、DNS エントリが古くなるのを防ぐことができます。

     ISP から静的 IP アドレスを取得することができない場合は、ドメイン ネーム サービス プロバイダーまたは他のサービス プロバイダーから、ドメイン ネーム システム (DNS) 動的更新プロトコル サービスを購入するという選択肢も検討できます。 DNS 動的更新プロトコルは、ネットワークの WAN 側の IP アドレスを最新の状態に保つサービスです。これにより、IP アドレスが変更されても、IP アドレスをドメイン名に解決することができます。

4.  ウィザードの指示に従って、信頼された証明書をインポートします。 信頼された証明書がない場合は、ウィザードに表示されるサポートされているドメイン ネーム プロバイダーから取得するか、任意の信頼できるプロバイダーから購入できます。 信頼された証明書の詳細については、ドメイン ネーム プロバイダーに問い合わせてください。

###  <a name="find-your-domain-name-service-provider"></a><a name="BKMK_Find"></a>ドメインネームサービスプロバイダーの検索

##### <a name="to-find-the-domain-name-service-provider-for-your-domain-name"></a>ドメイン名のドメイン ネーム サービス プロバイダーを確認するには

1. Web ブラウザーを開き、アドレス バーに「<strong>www.internic.com</strong>」と入力して、Internic のホーム ページに移動します。

2. Internic のホーム ページで、**[Whois]** をクリックします。

3. **[Whois]** ボックスに、ドメイン名を入力します (例: contoso.com)。

4. **[Domain]** オプションをクリックし、**[Submit]** をクリックします。

5. 検索結果の **[Registrar]** の欄に、ドメイン ネーム サービス プロバイダーの名前が表示されます。

##  <a name="customize-remote-web-access"></a><a name="BKMK_4"></a>リモート Web アクセスのカスタマイズ
 リモート Web アクセス サイトは、個人用のロゴや背景画像を追加してカスタマイズできます。 また、ホーム ページへのリンクを追加して、すべてのユーザーがこの情報を参照できるようにすることもできます。 詳細については、次のトピックを参照してください。

-   [リモート Web アクセスのカスタマイズ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeRWA)

-   [背景およびロゴの画像のカスタマイズ](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeImages)

-   [リモート Web アクセスの修復](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_RepairRWA)

###  <a name="customize-remote-web-access"></a><a name="BKMK_CustomizeRWA"></a>リモート Web アクセスのカスタマイズ
 リモート Web アクセスのホーム ページに対して、Web サイトのタイトルの変更、背景画像とロゴの変更、他の Web サイトへのリンクの追加を行ってカスタマイズすることができます。

##### <a name="to-customize-remote-web-access"></a>リモート Web アクセスをカスタマイズするには

1.  ダッシュボードを開きます。

2.  **[設定]** をクリックし、**[Anywhere Access]** タブをクリックします。

3.  **[Web サイト設定]** セクションで、**[カスタマイズ]** をクリックします。

4.  リモート Web アクセスのカスタマイズが完了したら、**[OK]** をクリックします。 リモート Web アクセスの変更をテストします。

###  <a name="customize-images-for-backgrounds-and-logos"></a><a name="BKMK_CustomizeImages"></a>背景とロゴ用にイメージをカスタマイズする
 このセクションでは、リモート Web アクセスのカスタマイズに使用できる画像についての情報を提供します。

#### <a name="image-size"></a>イメージ サイズ
 **ロゴ画像**

 サイズが 32x32 ピクセルのロゴ画像を使用することをお勧めします。 これより大きな画像は 32x32 のサイズに縮小され、これより小さな画像は 32x32 のサイズに拡大されます。これらの処理により画像がゆがむことがあります。

 **背景画像**

 背景画像にサイズの制限はありませんが、最適な結果を得るために、およそ 800x500 ピクセルの画像を使用することお勧めします。 背景画像は、ログオン ページの中央 (水平および垂直方向) に配置されます。 ログオン ページのテキストを読みやすくするため、背景画像の中心部分は薄い色にしてください。

#### <a name="image-file-types"></a>画像ファイルの種類
 次の種類の画像ファイルを使用して、既定の背景と Web サイトのロゴを置き換えることができます。

-   ビットマップ (* .bmp、 \* .dib、 \* rle)

-   GIF (*.gif)

-   PNG (*.png)

-   JPG (*.jpg)

###  <a name="repair-remote-web-access"></a><a name="BKMK_RepairRWA"></a>リモート Web アクセスの修復
 修復ウィザードを使用すると、ルーターやドメイン名の問題を検出して解決するのに役立ちます。 リモート Web アクセスの問題を検出するには 2 つの方法があります。

-   ダッシュボードの [サーバーの設定] にある [Anywhere Access] タブに、赤い X マークのアイコンが問題の説明と共に表示されます。

-   アラート ビューアーにアラートが表示されます。

> [!NOTE]
>  リモート Web アクセスを有効にするまで、修復ウィザードは使用できません。 リモート Web アクセスを有効にする方法の詳細については、「[リモート Web アクセスの有効化](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)」を参照してください。

##### <a name="to-repair-remote-web-access"></a>リモート Web アクセスを修復するには

1.  ダッシュボードにログオンします。

2.  **[設定]** をクリックし、**[Anywhere Access]** タブをクリックします。

3.  **[修復]** をクリックします。 **[リモート Web アクセスの修復]** ウィザードが起動します。

4.  **[次へ]** をクリックします。 リモート Web アクセスが分析され、問題が特定され、問題の修復が試行されます。

5.  ウィザードの完了時にアラートが表示される場合は、**[再試行]** をクリックすると、問題の修復が再試行されます。 引き続きアラートが表示される場合は、アラートを確認して、問題に関する追加情報とトラブルシューティングの手順を参照します。

##  <a name="troubleshoot-remote-web-access"></a><a name="BKMK_5"></a>リモート Web アクセスのトラブルシューティング

-   [リモート Web アクセスへの接続のトラブルシューティング](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)

-   [ファイアウォールのトラブルシューティング](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)

-   [Anywhere Access のトラブルシューティング](../support/Troubleshoot-Anywhere-Access-in-Windows-Server-Essentials.md)

## <a name="additional-references"></a>その他のリファレンス

-   [リモート デスクトップのオプション](Remote-desktop-options.md)

-   [リモート Web アクセスの使用](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Anywhere Access の管理](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
