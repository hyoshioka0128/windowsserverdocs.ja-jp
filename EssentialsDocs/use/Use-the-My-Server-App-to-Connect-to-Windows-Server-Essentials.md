---
title: My Server アプリを利用した Windows Server Essentials への接続
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 4e40b57f-6917-43ef-92e0-030baa9d2b99
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: 3fbe3824792432f5631729110fb0e9a548f6e05d
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217552"
---
# <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a>My Server アプリを利用した Windows Server Essentials への接続

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials 用の My Server アプリを使用すると、ノート pc、PC、または Surface デバイスから、リソースに接続し、Windows Server Essentials サーバー上で簡単な管理タスクを実行できます。 My Server では、ユーザー、デバイス、およびアラートを管理したり、サーバー上の共有ファイルを操作したりできます。 オフラインになっても、My Server から最後にアクセスしたファイルの操作を続行できます。オフラインでの変更は、次回接続したときにサーバーへ自動的に同期されます。  
  
 サーバーで Windows Server Essentials オペレーティングシステムが実行されている場合は、元の My Server アプリを使用します。 サーバーで Windows Server Essentials オペレーティングシステムが実行されている場合は、更新された My Server 2012 R2 アプリを使用する必要があります。 どちらのアプリも「 [Windows のアプリ](https://windows.microsoft.com/windows-8/apps)」からインストールできます。  
  
> [!TIP]
> 
>  Windows Phone から Windows Server Essentials のリソースにアクセスするには、My Server phone アプリ (Windows Server Essentials の場合) または My Server 2012 R2 Phone アプリ (Windows Server Essentials の場合) を使用します。 My Server phone アプリの詳細については、「 [Windows Phone 用の My server アプリの使用](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。 My Server 2012 R2 Phone アプリについては、ブログ エントリの「 [My Server 2012 R2 Windows アプリおよび Windows Phone アプリ](https://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)」を参照してください。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [My Server 2012 R2 の新機能](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_WhatsNew)  
  
-   [オペレーティング システムの要件](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_OS)  
  
-   [My Server のインストール](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Install)  
  
-   [My Server の使用](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_UseServer)  
  
-   [My Server の機能](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Features)  
  
-   [ローカル ネットワークからサーバーに接続する方法](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_ConnectServer)  

>  Windows Phone から Windows Server Essentials のリソースにアクセスするには、My Server phone アプリ (Windows Server Essentials の場合) または My Server 2012 R2 Phone アプリ (Windows Server Essentials の場合) を使用します。 My Server phone アプリの詳細については、「 [Windows Phone 用の My server アプリの使用](../use/Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。 My Server 2012 R2 Phone アプリについては、ブログ エントリの「 [My Server 2012 R2 Windows アプリおよび Windows Phone アプリ](https://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)」を参照してください。

  
##  <a name="whats-new-in-my-server-2012-r2"></a><a name="BKMK_WhatsNew"></a>My Server 2012 R2 の新機能  
 My Server で使用できる機能に加えて、My Server 2012 R2 では、Windows Server Essentials を使用するお客様向けに次の新機能が提供されています。  
  
-   **Sharepoint online チームサイトとライブラリへのアクセス**-Microsoft Office 365 と Windows Server Essentials の統合を活用して、sharepoint online チームサイトにアクセスし、My Server 2012 R2 で sharepoint online ライブラリのドキュメントを開きます。  
  
-   **サーバーとクライアントコンピューターへのリモートデスクトップ接続**-My Server 2012 R2 の**remote connect**を使用して、リモートデスクトップを使用して Windows server Essentials サーバーとクライアントコンピューターに接続します。  
  
##  <a name="operating-system-requirements"></a><a name="BKMK_OS"></a>オペレーティングシステムの要件  
 マイサーバーまたは My Server 2012 R2 をノート pc、PC、または Surface デバイスで使用するには、コンピューターに次のオペレーティングシステムのいずれかが搭載されている必要があります: Windows 8.1、Windows RT 8.1、Windows 8、または Windows RT。  
  
##  <a name="install-my-server"></a><a name="BKMK_Install"></a>マイサーバーのインストール  
 適切な My Server アプリを [Windows のアプリ](https://windows.microsoft.com/windows-8/apps) ストアからダウンロードすることができます。 コンピューターに Windows 8 または Windows RT オペレーティングシステムがインストールされていて、サーバー名を使用してイントラネット上のサーバーに接続する場合は、サーバーから証明書をインストールする必要もあります。  
  
#### <a name="to-install-my-server-or-my-server-2012-r2-on-your-windows-based-laptop-pc-or-surface-device"></a>My Server または My Server 2012 R2 を Windows ベースのノート PC、PC、または Surface デバイスにインストールするには  
  
1.  適切な My Server アプリを [Windows のアプリ](https://windows.microsoft.com/windows-8/apps) から Windows ベースのノート PC、PC、または Surface デバイスにインストールします。  
  
    |サーバー オペレーティング システム|ダウンロード|  
    |-----------------------------|--------------|  
    | Windows Server Essentials|[My Server](https://apps.microsoft.com/webpdp/app/19d94f81-db21-4234-8b49-806694dbbaea)|  
    | Windows Server Essentials|[My Server 2012 R2](https://apps.microsoft.com/webpdp/app/67e86695-bda3-4f32-96c4-2e20e56f1cf3)|  
  
2.  サーバー名を使用してイントラネット経由で Windows Server Essentials サーバーに接続できるようにし、デバイスに Windows 8 または Windows RT オペレーティングシステムがインストールされている場合は、次の手順を実行して、既定の CAROOT .cer 証明書をコンピューターにインストールします。 Windows 8.1 および Windows RT 8.1 では、証明書の手動インストールは不要です。  
  
###  <a name="to-install-a-certificate-for-my-server-on-your-windows-8-windows-81-or-windows-rt-device"></a><a name="BKMK_InstallCert"></a>Windows 8、Windows 8.1、または Windows RT デバイスに My Server の証明書をインストールするには  
  
1.  コンピューターで Web ブラウザーを開き、既定の証明書 CAROOT.cer をサーバーからダウンロードします。 これを行うには、次のように入力します。その際、<*サーバー名*> をご使用のサーバーの名前で置き換えます (たとえば、**marketing.contoso.com**)。  
  
     **http://<servername \> /connect/default.aspx? get = caroot .cer**  
  
2.  証明書をインストールします。  
  
    1.  **[スタート]** ページで **[エクスプローラー]** を開きます。  
  
    2.  非表示の項目とファイル名の拡張子が表示されるようにします。 **[表示]** タブの **[表示/非表示]** グループで、 **[隠しファイル]** チェック ボックスと **[ファイル名拡張子]** チェック ボックスをオンにします。  
  
    3.  ダウンロードした CAROOT.cer ファイルが含まれているフォルダーに移動します。  
  
    4.  CAROOT.cer ファイルを右クリックして、**[開く]** をクリックします。  
  
    5.  **[証明書]** ダイアログ ボックスで、**[証明書のインストール]** をクリックします。  
  
    6.  **[ローカル コンピューター]** をインストール場所として選択し、**[次へ]** をクリックします。  
  
    7.  **[証明書ストア]** ウィザード ページで、**[証明書をすべて次のストアに配置する**] を選択し、**[参照]** を使用して **[信頼されたルート証明機関]** ストアを選択します。 **[完了]** をクリックします。  
  
##  <a name="use-my-server"></a><a name="BKMK_UseServer"></a>マイサーバーを使用する  
 My Server または My Server 2012 R2 アプリの使用を開始するには、アプリを開き、その機能のクイック ツアーを実行します。  
  
#### <a name="to-open-my-server-or-my-server-2012-r2"></a>My Server または My Server 2012 R2 を開くには  
  
1.  Windows デバイスの**スタート**ページから my Server (Windows server essentials の場合) または my Server 2012 R2 (Windows server essentials の場合) を開きます。  
  
2.  サーバー上のアカウントを使用して、Windows Server Essentials サーバーにサインインします。 サーバーを識別するには、次のようにします。  
  
    -   オフプレミス環境では、サーバーのドメイン名 (たとえば、 **marketing.contoso.com**) を使用します。  
  
    -   イントラネット経由でオンプレミスで接続している場合は、サーバー名を使用します。前の例では、サーバー名は**marketing**です。 (Windows 8 または Windows RT コンピューターを使用してオンプレミスに接続し、この方法を使用する場合は、サーバーから CAROOT .cer 証明書をインストールする必要があります。 詳細については、「 [windows 8、Windows 8.1、または WINDOWS RT デバイスに My Server の証明書をインストールするには](#BKMK_InstallCert)」を参照してください。)  
  
###  <a name="features-of-my-server"></a><a name="BKMK_Features"></a>My Server の機能  
 My Server アプリと My Server 2012 R2 アプリの機能を次の表で説明します。 表示できる項目と実行できる操作は、サーバーのアカウントの種類によって決まります。 すべてのユーザーが、共有リソースを操作し、**[最近使ったもの]** 画面をカスタマイズし、最近使用したファイルをオフライン アクセスのためにキャッシュに入れておく期間を決定し、有料の接続を介したダウンロードをオンまたはオフにすることができます。 Windows Server Essentials サーバーの管理者は、アラート、デバイス、およびユーザーを管理することもできます。 標準ユーザー アカウントには、アラートを表示したりデバイスに接続するためのより制限された機能があります。これは、ユーザー アカウントのプロパティによって決定されます。個々の機能の要件は、次の表に記載されています。  
  
### <a name="features-of-the-my-server-and-my-server-2012-r2-apps-for-windows-server-essentials"></a>Windows Server Essentials の My Server アプリと My Server 2012 R2 アプリの機能  
  
|機能セット|説明|  
|-----------------|-----------------|  
|アラートの管理|-(管理者のみ) サーバー上のアラートを解決するか、アクションを必要としないアラートを無視します。 通知を有効または無効にします (**[アクセス許可]** 設定、**[通知]** オプション)<br />-(標準ユーザーアカウント) ネットワークの正常性アラートを表示します。<br />     **注:** ユーザーが My Server でアラートを表示できるようにするには、ユーザーアカウントの **[全般**設定] で [**ユーザーがネットワークの正常性アラートを表示できる**ようにする] 設定を選択する必要があります。 詳細については、「 [Manage user accounts using the Dashboard](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)」を参照してください。|  
|デバイスの管理|(管理者のみ)。<br /><br /> -Windows Server Essentials サーバーに接続している場合は、接続されている各コンピューターの詳細が [**デバイス**] ビューに表示されます。 オフライン デバイスは網掛けされます。<br />-接続されているコンピューターのバックアップを開始および停止します。<br />-[マイサーバー] で通知をオンまたはオフにします。 (**[アクセス許可]** 設定、**[通知]** オプション)<br /><br /> すべてのユーザー:<br /><br /> -ユーザーアカウントがアクセスできるクライアントコンピューターを表示します。 (**[デバイス]** 画面)<br />-これらのコンピューターのアラートを監視します。 (**[アラート]** 画面)<br />-(My Server 2012 R2 のみ) リモート Web アクセスを使用してこれらのコンピューターに接続します。 (**[デバイス]** 画面、**[リモート接続]** ボタン)|  
|リモート デスクトップを使用してコンピューターに接続する|(My Server 2012 R2 のみ)Windows Server Essentials サーバーまたはクライアントコンピューターでリモートデスクトップセッションを開きます。 (**[デバイス]** 画面、**[リモート接続]** ボタン)<br /><br /> **注:** この機能を有効にするには、コンピューターの Windows アプリから[リモートデスクトップアプリ](https://apps.microsoft.com/webpdp/app/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)をダウンロードしてインストールします。 標準ユーザーのアカウントは、サインオンする権限のあるデバイスに接続できます。 ユーザーがコンピューターにサインオンできるようにするには、ユーザー アカウントの **[コンピューターへのアクセス]** タブにコンピューターを追加します。 詳細については、「 [Assign user accounts permission to log on to specific network computers](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。|  
|ユーザーの管理|(管理者のみ) ユーザー アカウントのパスワードを変更します。 サーバー上のユーザーのセッションを終了します。 (**[ユーザー]** 設定)|  
|共有ファイルに対する作業|<ul><li>共有ファイル (サーバー上のアクセス権を持つ共有フォルダー)、プライベート共有、または Windows 8.1 デバイス、SkyDrive、またはネットワークストレージからファイルをアップロードおよびダウンロードします。 フォルダーを作成します。 サーバーにファイルを追加 (アップロード) したり、そのファイルを編集したり、サーバーからファイルを削除したりします。</li><li>ファイルをアップロードまたはダウンロードする間、転送状況を表示します。 転送をキャンセルします。 ファイルの競合を解決します。</li><li>ローカル コンピューター、サーバー、SkyDrive、またはネットワーク ストレージ上のファイルやフォルダーに対してシームレスに作業します。 ファイルの一覧には、コンピューター、SkyDrive、またはネットワーク ストレージで最近使用したフォルダーやサーバー上のフォルダー、およびサーバーにある共有フォルダーが表示され、それらの場所にあるフォルダーを参照することができます。</li><li>サーバー上のフォルダーおよびファイルを検索します。ファイルをクリックしてダウンロードし、既定のアプリで開きます。 オフライン モードでは、オフライン ファイルのみを検索します。</li><li>画像、音楽、およびビデオを共有します。 ファイルをクリックして、Windows 8 の画像、音楽、またはビデオプレーヤーで開きます。 または、**[開く]** あるいは **[別のアプリで開く]** を使用して別のアプリで開きます。 通常どおり、選択したアプリをそのメディアの種類の既定のアプリとして設定することができます。<br /><br />     **注:** 既定では、windows server essentials エクスペリエンスの役割がインストールされている windows server Essentials および Windows Server 2012 R2 では、メディアストリーミング機能は使用できません。 詳細については、「[デジタルメディアの管理](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)」を参照してください。<br /><br /> <ul><li>**画像** - **[画像]** ビューで、画像をタップして開きます。 My Server のサムネイル表示に戻るには、もう一度画像をタップします。</li><li>**音楽**-**ミュージック**ビューで、サーバー上で共有されているアルバムや楽曲を表示します。 項目をタップして、ミュージック プレーヤーで開きます。</li><li>**ビデオ-[** **ビデオ] ビューの**サムネイルをクリックして、ビデオプレーヤーを開きます。</li></ul></li></ul>|  
|SharePoint Online ライブラリの管理|(My Server 2012 R2 のみ)チームの SharePoint Online ライブラリ内のファイルを操作します。 チームのサイトを開きます。 (SharePoint Online セクション: チーム サイトを開き、開きたいドキュメント ライブラリまたはファイルにドリルダウンします。 ファイルを開くときに、ネットワーク アカウントに関連付けられている Microsoft オンライン アカウントで Office 365 にサインインする必要があります。<br /><br /> **注:** この機能を使用するには、サーバーを Office 365 と統合し、Office 365 サブスクリプションに SharePoint Online を含める必要があります。また、サーバー上のユーザーアカウントには、Microsoft Online Services アカウントが関連付けられている必要があります。 Office 365 と SharePoint Online を Windows Server Essentials と統合する方法の詳細については、「Windows server essentials[のサービス統合の概要-パート 1](https://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx) 」および「 [windows Server Essentials のサービス統合の概要-パート 2](https://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)」を参照してください。|  
|**[最近使ったもの]** 画面のカスタマイズ|**[最近使ったもの]** の一覧から、作業中のファイルに簡単に即時にアクセスすることができます。 次のような変更を行うことができます。<br /><br /> -最近使ったファイルの履歴を表示する日数を設定します。 (**[最近使ったもの]** 設定: **[最近使ったものに保持する日数]**; 既定 = 7 日)<br />-作業中のファイルを操作する必要がなくなった場合は、[**最近**] 表示をクリアします。 これは、キャッシュには影響しません。ファイルは引き続きオフラインで利用できます。 (**最近**の設定:**クリア**ボタン)<br />     **ヒント:** ファイルへのオフラインアクセスが不要な場合は、**オフライン**設定の [**すべてクリア**] を使用して、キャッシュからファイルを削除します。|  
|オフライン作業|既定では、過去 7 日間にアクセスしていたファイルをオフラインで利用できます。 オフラインでの変更は、サーバーに接続するたびにサーバーと同期されます。<br /><br /> オフラインの構成には、次のような変更を行うことができます。<br /><br /> -キャッシュする作業の日数を変更します。 (My Server の **[オフライン]** 設定、My Server 2012 R2 の **[ファイル]** 設定: **キャッシュ期間**; 既定 = 7 日)<br />-有料ネットワークでのファイル転送を許可するか、またはその機能を無効にします。 既定では、有料ネットワークを経由したコストのかかるファイル転送が行われないようにするためにオフになっています。 (**[オフライン]** 設定または **[ファイル]** 設定: **[有料ネットワーク経由の自動ファイル転送をオンまたはオフにする]**; 既定 = **[オフ]**)<br />-キャッシュをクリアすることが必要になる場合があります。 **[最近使ったもの]** 設定または **[ファイル]** 設定でキャッシュのサイズを確認します。その後、**[クリア]** または **[すべてクリア]** を使用してキャッシュをクリアします。<br /><br /> **ヒント:** オフラインで使用できるファイルを確認するには、任意の共有フォルダーで、[**すべて**] ではなく、**オフラインキャッシュ**されたフィルターを選択します。<br /><br /> **注:** 既定では、キャッシュには、**最近使用**した一覧に表示されるのと同じファイル履歴が格納されます。 キャッシュをクリアするか、キャッシュの設定と **[最近使ったもの]** 画面が一致しない場合、**[最近使ったもの]** の一覧の一部のファイルをオフラインで利用できない可能性があります。|  
|バック グラウンドの同期|ファイルは My Server にログオンするたびに、またサーバーとの接続中に変更が加えられると、サーバーと同期されます。 パフォーマンスを維持するために、リソースを消費するバックグラウンドの同期はほとんどのフォルダーで自動的には実行されません。 コストのかかる転送を回避するために、3 ギガバイトのネットワークではバックグラウンドの同期は実行されません。<br /><br /> -ファイルの競合を解決します。 [転送の**状態**] ページの [**競合**] 領域に表示されます。 ファイル転送が実行される際、メイン画面に **[転送の状態]** チャームと **[アラート]** チャームが表示されます。|  
  
##  <a name="how-to-connect-to-your-server-from-your-local-network"></a><a name="BKMK_ConnectServer"></a>ローカルネットワークからサーバーに接続する方法  
 Windows Phone、Windows 8、および Windows 8.1 の My Server アプリを Windows Server Essentials 環境で正常に使用するには、最初にサーバー証明書をデバイスにインストールする必要があります。 これにより、ローカル ネットワークで Windows Server Essentials を実行しているサーバーにデバイスが接続されます。 次の手順を使用して、ローカル ネットワーク内のサーバーに接続し、Windows 8 あるいは Windows 8.1 を実行している Windows Phone またはコンピューターにサーバー証明書をインストールします。  
  
#### <a name="to-connect-to-your-server-from-your-windows-phone"></a>Windows Phone からサーバーに接続するには  
  
1.  Windows 8 または Windows 8.1 を実行している Windows Phone で、Internet Explorer を開きます。  
  
2.  アドレスバーに「http://<入力します。この場合は、「」と入力し、enter キーを押します。 ** \> **  
  
3.  caroot.cer 証明書をインストールするメッセージが表示されたら、**[インストール]** をクリックします。  
  
4.  証明書のインストールが完了するのを待ちます。  
  
    > [!NOTE]
    >  証明書のインストールが完了したら、サーバー名とネットワーク資格情報を使用して Windows Phone 用の My Server アプリにサインインできるようになります。  
  
#### <a name="to-connect-to-your-server-in-your-local-network-from-a-computer-running-windows-8-or-windows-81"></a>Windows 8 または Windows 8.1 を実行するコンピューターからローカル ネットワーク内のサーバーに接続するには  
  
1.  Windows 8 または Windows 8.1 を実行しているコンピューターで、Internet Explorer を開きます。  
  
2.  アドレスバーに「http://<入力します。この場合は、「」と入力し、enter キーを押します。 ** \> **  
  
3.  caroot.cer 証明書をインストールするメッセージが表示されたら、**[開く]** をクリックします。  
  
4.  **[証明書]** ダイアログ ボックスで、**[証明書のインストール]** をクリックします。  
  
5.  証明書のインポート ウィザードで、保管場所として **[ローカル コンピューター]** を選択します。  
  
6.  **[証明書をすべて次のストアに配置する]** を選択し、**[信頼されたルート証明機関]** の場所を参照します。  
  
7.  指示に従ってウィザードを完了します。  
  
    > [!NOTE]
    >  証明書のインストールが完了したら、サーバー名とネットワーク資格情報を使用して Windows 8 または Windows 8.1 用の My Server アプリにサインインできるようになります。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials のサービス統合の概要-パート1](https://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials のサービス統合の概要-パート2](https://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Anywhere Access の管理](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)    

-   [リモートで作業する](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の使用](Use-Windows-Server-Essentials.md)

