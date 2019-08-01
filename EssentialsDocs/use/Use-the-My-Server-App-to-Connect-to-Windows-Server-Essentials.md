---
title: My Server アプリを利用した Windows Server Essentials への接続
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e40b57f-6917-43ef-92e0-030baa9d2b99
9author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3c7c5114bbd3aa479e2b6afe807fee2ec8d3d5bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435885"
---
# <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a>My Server アプリを利用した Windows Server Essentials への接続

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials の My Server アプリを使用すると、リソースに接続し、ラップトップ、PC、または Surface デバイスから Windows Server Essentials サーバーに簡単な管理タスクを実行できます。 My Server では、ユーザー、デバイス、およびアラートを管理したり、サーバー上の共有ファイルを操作したりできます。 オフラインになっても、My Server から最後にアクセスしたファイルの操作を続行できます。オフラインでの変更は、次回接続したときにサーバーへ自動的に同期されます。  
  
 サーバーで Windows Server Essentials のオペレーティング システムが実行されている場合は、元の My Server アプリを使用します。 サーバーで Windows Server Essentials のオペレーティング システムが実行されている場合、更新された My Server 2012 R2 アプリを使用する必要があります。 どちらのアプリも「 [Windows のアプリ](https://windows.microsoft.com/windows-8/apps)」からインストールできます。  
  
> [!TIP]
> 
>  に、Windows Phone から Windows Server Essentials でのリソースにアクセスするには、(Windows Server Essentials) 用の My Server phone アプリまたは (Windows Server Essentials) 用の My Server 2012 R2 phone アプリを使用します。 My Server phone アプリについては、次を参照してください。 [Windows Phone の My Server アプリを使用して](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)します。 My Server 2012 R2 Phone アプリについては、ブログ エントリの「 [My Server 2012 R2 Windows アプリおよび Windows Phone アプリ](http://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)」を参照してください。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [My Server 2012 R2 の新機能新機能](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_WhatsNew)  
  
-   [オペレーティング システムの要件](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_OS)  
  
-   [My Server をインストールします。](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Install)  
  
-   [My Server を使用します。](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_UseServer)  
  
-   [My Server の機能](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Features)  
  
-   [ローカル ネットワークからサーバーに接続する方法](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_ConnectServer)  

>  に、Windows Phone から Windows Server Essentials でのリソースにアクセスするには、(Windows Server Essentials) 用の My Server phone アプリまたは (Windows Server Essentials) 用の My Server 2012 R2 phone アプリを使用します。 My Server phone アプリについては、次を参照してください。 [Windows Phone の My Server アプリを使用して](../use/Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)します。 My Server 2012 R2 Phone アプリについては、ブログ エントリの「 [My Server 2012 R2 Windows アプリおよび Windows Phone アプリ](http://blogs.technet.com/b/sbs/archive/2013/11/19/my-server-2012-r2-windows-and-windows-phone-apps.aspx)」を参照してください。  
  
## <a name="in-this-topic"></a>このトピックの内容  
  
-   [My Server 2012 R2 の新機能新機能](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_WhatsNew)  
  
-   [オペレーティング システムの要件](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_OS)  
  
-   [My Server をインストールします。](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Install)  
  
-   [My Server を使用します。](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_UseServer)  
  
-   [My Server の機能](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_Features)  
  
-   [ローカル ネットワークからサーバーに接続する方法](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md#BKMK_ConnectServer)  

  
##  <a name="BKMK_WhatsNew"></a> My Server 2012 R2 の新機能新機能  
 My Server で使用できる機能に加えは、My Server 2012 R2 は、お客様向け Windows Server Essentials に次の新機能を提供します。  
  
-   **SharePoint Online チーム サイトとライブラリへのアクセス**-SharePoint Online チーム サイトにアクセスし、My Server 2012 R2 で SharePoint Online ライブラリ内のドキュメントを開いて Windows Server Essentials との統合を活用して Microsoft Office 365 です。  
  
-   **サーバーとクライアント コンピューターに対するリモート デスクトップ接続**-使用**リモート接続**リモート デスクトップを使用して、Windows Server Essentials サーバーとクライアント コンピューターに接続する、My Server 2012 r2。  
  
##  <a name="BKMK_OS"></a> オペレーティング システムの要件  
 My Server または My Server 2012 R2 では、ラップトップ、PC、または Surface デバイスを使用するには、コンピューターは、次のオペレーティング システムのいずれかが必要です。Windows 8.1、Windows RT 8.1、Windows 8、または Windows RT.  
  
##  <a name="BKMK_Install"></a> My Server をインストールします。  
 適切な My Server アプリを [Windows のアプリ](https://windows.microsoft.com/windows-8/apps) ストアからダウンロードすることができます。 コンピューターに Windows 8 または Windows RT オペレーティング システムで、サーバー名を使用して、イントラネット上のサーバーに接続する場合は、サーバーから証明書をインストールする必要があります。  
  
#### <a name="to-install-my-server-or-my-server-2012-r2-on-your-windows-based-laptop-pc-or-surface-device"></a>My Server または My Server 2012 R2 を Windows ベースのノート PC、PC、または Surface デバイスにインストールするには  
  
1.  適切な My Server アプリを [Windows のアプリ](https://windows.microsoft.com/windows-8/apps) から Windows ベースのノート PC、PC、または Surface デバイスにインストールします。  
  
    |サーバーのオペレーティング システム|ダウンロード|  
    |-----------------------------|--------------|  
    | Windows Server Essentials|[私のサーバー](https://apps.microsoft.com/webpdp/app/19d94f81-db21-4234-8b49-806694dbbaea)|  
    | Windows Server Essentials|[My Server 2012 R2](https://apps.microsoft.com/webpdp/app/67e86695-bda3-4f32-96c4-2e20e56f1cf3)|  
  
2.  サーバー名を使用して、イントラネット経由で Windows Server Essentials サーバーに接続することができるようにして、デバイスが、Windows 8 または Windows RT オペレーティング システムには、既定 CAROOT.cer 証明書をインストール コンピューターに次 p を実行することによってrocedure します。 証明書の手動インストールは、Windows 8.1 と Windows RT 8.1 では必要ありません。  
  
###  <a name="BKMK_InstallCert"></a> Windows 8、Windows 8.1、または Windows RT デバイスで My Server の証明書をインストールするには  
  
1.  コンピューターで Web ブラウザーを開き、既定の証明書 CAROOT.cer をサーバーからダウンロードします。 これを行うには、次のように入力します。その際、<*サーバー名*> をご使用のサーバーの名前で置き換えます (たとえば、**marketing.contoso.com**)。  
  
     **http://<servername\>/connect/default.aspx?get=caroot.cer**  
  
2.  証明書をインストールします。  
  
    1.  **[スタート]** ページで **[エクスプローラー]** を開きます。  
  
    2.  非表示の項目とファイル名の拡張子が表示されるようにします。 **[表示]** タブの **[表示/非表示]** グループで、 **[隠しファイル]** チェック ボックスと **[ファイル名拡張子]** チェック ボックスをオンにします。  
  
    3.  ダウンロードした CAROOT.cer ファイルが含まれているフォルダーに移動します。  
  
    4.  CAROOT.cer ファイルを右クリックして、 **[開く]** をクリックします。  
  
    5.  **[証明書]** ダイアログ ボックスで、 **[証明書のインストール]** をクリックします。  
  
    6.  **[ローカル コンピューター]** をインストール場所として選択し、 **[次へ]** をクリックします。  
  
    7.  **[証明書ストア]** ウィザード ページで、 **[証明書をすべて次のストアに配置する**] を選択し、 **[参照]** を使用して **[信頼されたルート証明機関]** ストアを選択します。 次に、 **[完了]** をクリックします。  
  
##  <a name="BKMK_UseServer"></a> My Server を使用します。  
 My Server または My Server 2012 R2 アプリの使用を開始するには、アプリを開き、その機能のクイック ツアーを実行します。  
  
#### <a name="to-open-my-server-or-my-server-2012-r2"></a>My Server または My Server 2012 R2 を開くには  
  
1.  (Windows Server Essentials) 用の My Server または (Windows Server Essentials) 用の My Server 2012 R2 を開く、**開始**Windows デバイスのページ。  
  
2.  サーバーで、アカウントを使用して Windows Server Essentials サーバーにサインインします。 サーバーを識別するには、次のようにします。  
  
    -   たとえば、オフプレミス環境では、使用、サーバーのドメイン名 - **marketing.contoso.com**します。  
  
    -   前の例では、サーバー名を使用して、イントラネット経由でオンプレミスを接続する場合は、サーバー名が**マーケティング**します。 (場合は、オンプレミスの接続に Windows 8 または Windows RT のコンピューターを使用しているし、このメソッドを使用する、する必要があります CAROOT.cer 証明書サーバーからインストールします。 詳細については、次を参照してください[My Server の Windows 8、Windows 8.1、または Windows RT デバイスで証明書をインストールする](#BKMK_InstallCert)。)。  
  
###  <a name="BKMK_Features"></a> My Server の機能  
 My Server アプリと My Server 2012 R2 アプリの機能を次の表で説明します。 表示できる項目と実行できる操作は、サーバーのアカウントの種類によって決まります。 すべてのユーザーが、共有リソースを操作し、 **[最近使ったもの]** 画面をカスタマイズし、最近使用したファイルをオフライン アクセスのためにキャッシュに入れておく期間を決定し、有料の接続を介したダウンロードをオンまたはオフにすることができます。 Windows Server Essentials サーバーの管理者は、アラート、デバイス、およびユーザー使用管理できますも。 標準ユーザー アカウントには、アラートを表示したりデバイスに接続するためのより制限された機能があります。これは、ユーザー アカウントのプロパティによって決定されます。個々の機能の要件は、次の表に記載されています。  
  
### <a name="features-of-the-my-server-and-my-server-2012-r2-apps-for-windows-server-essentials"></a>Windows Server Essentials の My Server アプリと My Server 2012 R2 アプリの機能  
  
|機能セット|説明|  
|-----------------|-----------------|  
|アラートの管理|-(管理者のみ) の解決は、サーバー上のアラートまたはアクションを必要としないアラートを無視します。 通知を有効または無効にします ( **[アクセス許可]** 設定、 **[通知]** オプション)<br />-ネットワーク正常性アラートの表示 (標準ユーザー アカウント)。<br />     **注:** ユーザーが My Server でのアラートを表示するため、**ユーザーがネットワーク正常性アラートを表示できます**で設定を選択する必要があります**全般**ユーザー アカウントの設定。 詳細については、「 [Manage user accounts using the Dashboard](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)」を参照してください。|  
|デバイスの管理|(管理者のみ)<br /><br /> -Windows Server Essentials サーバーに接続しているときに接続されている各コンピュータに関する詳細を表示します。**デバイス**ビュー。 オフライン デバイスは網掛けされます。<br />-開始し、接続されているコンピューターのバックアップを停止します。<br />-My Server では、オンまたはオフに通知を有効にします。 ( **[アクセス許可]** 設定、 **[通知]** オプション)<br /><br /> すべてのユーザー:<br /><br /> -ユーザー アカウントがアクセスできるクライアント コンピューターを表示します。 ( **[デバイス]** 画面)<br />-これらのコンピューターのアラートを監視します。 ( **[アラート]** 画面)<br />-(My Server 2012 R2 のみ) でリモート Web アクセスを使用してこれらのコンピューターに接続します。 ( **[デバイス]** 画面、 **[リモート接続]** ボタン)|  
|リモート デスクトップを使用してコンピューターに接続する|(My Server 2012 R2 のみ)Windows Server Essentials サーバーまたはクライアント コンピューターでリモート デスクトップ セッションを開きます。 ( **[デバイス]** 画面、 **[リモート接続]** ボタン)<br /><br /> **注:** この機能を有効にするのには、ダウンロードしてインストール、[リモート デスクトップ アプリ](https://apps.microsoft.com/webpdp/app/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)からアプリを Windows コンピューターにします。 標準ユーザーのアカウントは、サインオンする権限のあるデバイスに接続できます。 ユーザーがコンピューターにサインオンできるようにするには、ユーザー アカウントの **[コンピューターへのアクセス]** タブにコンピューターを追加します。 詳細については、次を参照してください。[ユーザー アカウントに特定のネットワーク コンピューターにログオンする権限を割り当てる](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)します。|  
|ユーザーを管理する|(管理者のみ) ユーザー アカウントのパスワードを変更します。 サーバー上のユーザーのセッションを終了します。 ( **[ユーザー]** 設定)|  
|共有ファイルに対する作業|<ul><li>アップロードとダウンロード ファイルの共有ファイル (共有フォルダー に、サーバーへのアクセスがある) からプライベート共有、または Windows 8.1 デバイス、SkyDrive あるいはネットワーク ストレージから。 フォルダーを作成します。 サーバーにファイルを追加 (アップロード) したり、そのファイルを編集したり、サーバーからファイルを削除したりします。</li><li>ファイルをアップロードまたはダウンロードする間、転送状況を表示します。 転送をキャンセルします。 ファイルの競合を解決します。</li><li>ローカル コンピューター、サーバー、SkyDrive、またはネットワーク ストレージ上のファイルやフォルダーに対してシームレスに作業します。 ファイルの一覧には、コンピューター、SkyDrive、またはネットワーク ストレージで最近使用したフォルダーやサーバー上のフォルダー、およびサーバーにある共有フォルダーが表示され、それらの場所にあるフォルダーを参照することができます。</li><li>サーバー上のフォルダーおよびファイルを検索します。ファイルをクリックしてダウンロードし、既定のアプリで開きます。 オフライン モードでは、オフライン ファイルのみを検索します。</li><li>画像、音楽、およびビデオを共有します。 Windows 8 の画像、音楽、またはビデオ プレーヤーで開くファイルをクリックします。 または、 **[開く]** あるいは **[別のアプリで開く]** を使用して別のアプリで開きます。 通常どおり、選択したアプリをそのメディアの種類の既定のアプリとして設定することができます。<br /><br />     **注:** 既定では、メディア ストリーミング機能がない Windows Server Essentials と Windows Server 2012 R2、Windows Server Essentials エクスペリエンス役割がインストールされました。 詳細については、次を参照してください。 [Manage Digital Media](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)します。<br /><br /> <ul><li>**画像** - **[画像]** ビューで、画像をタップして開きます。 My Server のサムネイル表示に戻るには、もう一度画像をタップします。</li><li>**音楽**-**音楽**ビューに、アルバムや曲、サーバー上の共有を表示します。 項目をタップして、ミュージック プレーヤーで開きます。</li><li>**ビデオ**-サムネイルをクリックして**ビデオ**ビュー、ビデオ プレーヤーを開きます。</li></ul></li></ul>|  
|SharePoint Online ライブラリの管理|(My Server 2012 R2 のみ)チームの SharePoint Online ライブラリ内のファイルを使用します。 チームのサイトを開きます。 (SharePoint Online セクション: チーム サイトを開き、開きたいドキュメント ライブラリまたはファイルにドリルダウンします。 ファイルを開くときにする必要がありますにサインインする Office 365、ネットワーク アカウントに関連付けられている Microsoft オンライン アカウントを使用します。)<br /><br /> **注:** この機能を使用するサーバーは、Office 365 と統合する必要があります、Office 365 サブスクリプションは、SharePoint Online、含める必要があります、およびサーバーで、ユーザー アカウントは Microsoft Online Services アカウントが関連付けられている必要があります。 Windows Server Essentials と Office 365 と SharePoint Online を統合する方法の詳細については、次を参照してください[サービス統合 Windows Server Essentials の概要 - パート 1](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)と[のサービス統合の概要。Windows Server Essentials - パート 2](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)します。|  
|**[最近使ったもの]** 画面のカスタマイズ|**[最近使ったもの]** の一覧から、作業中のファイルに簡単に即時にアクセスすることができます。 次のような変更を行うことができます。<br /><br /> -最近のファイル履歴を表示する日数を設定します。 ( **[最近使ったもの]** 設定: **[最近使ったものに保持する日数]** ; 既定 = 7 日)<br />-オフ、**最近**作業で作業しているファイルが不要になった場合、表示します。 これは、キャッシュには影響しません。ファイルは引き続きオフラインで利用できます。 ( **[最近使ったもの]** 設定: **[クリア]** ボタン)<br />     **クォータを調整する**ファイルへのオフライン アクセスを必要としない場合は、使用**すべてクリア**で**オフライン**キャッシュからファイルを削除する設定。|  
|オフラインで作業する|既定では、過去 7 日間にアクセスしていたファイルをオフラインで利用できます。 オフラインでの変更は、サーバーに接続するたびにサーバーと同期されます。<br /><br /> オフラインの構成には、次のような変更を行うことができます。<br /><br /> -作業の日数をキャッシュに変更します。 (**オフライン**My Server で設定**ファイル**My Server 2012 R2 での設定。**キャッシュ期間**; 既定 = 7 日)<br />-有料ネットワーク経由でファイル転送を許可またはその機能をオフにします。 既定では、有料ネットワークを経由したコストのかかるファイル転送が行われないようにするためにオフになっています。 ( **[オフライン]** 設定または **[ファイル]** 設定: **[有料ネットワーク経由の自動ファイル転送をオンまたはオフにする]** ; 既定 = **[オフ]** )<br />-場合によっては、キャッシュをクリアする場合がありますこと。 **[最近使ったもの]** 設定または **[ファイル]** 設定でキャッシュのサイズを確認します。その後、 **[クリア]** または **[すべてクリア]** を使用してキャッシュをクリアします。<br /><br /> **クォータを調整する**任意の共有フォルダーでオフラインで利用可能なファイルを見つけるには、 **[すべて]** の代わりに [オフライン キャッシュ] フィルターを使用します。<br /><br /> **注:** 既定では、キャッシュには、 **[最近使ったもの]** リストに表示されるものと同じファイル履歴が保管されます。 キャッシュをクリアするか、キャッシュの設定と **[最近使ったもの]** 画面が一致しない場合、 **[最近使ったもの]** の一覧の一部のファイルをオフラインで利用できない可能性があります。|  
|バック グラウンドの同期|ファイルは My Server にログオンするたびに、またサーバーとの接続中に変更が加えられると、サーバーと同期されます。 パフォーマンスを維持するために、リソースを消費するバックグラウンドの同期はほとんどのフォルダーで自動的には実行されません。 コストのかかる転送を回避するために、3 ギガバイトのネットワークではバックグラウンドの同期は実行されません。<br /><br /> -に表示されるファイルの競合を解決する、**競合している**の領域、**転送の状態**ページ。 ファイル転送が実行される際、メイン画面に **[転送の状態]** チャームと **[アラート]** チャームが表示されます。|  
  
##  <a name="BKMK_ConnectServer"></a> ローカル ネットワークからサーバーに接続する方法  
 Windows Phone、Windows 8、および Windows 8.1 の My Server アプリを Windows Server Essentials 環境で正常に使用するには、最初にサーバー証明書をデバイスにインストールする必要があります。 これにより、ローカル ネットワークで Windows Server Essentials を実行しているサーバーにデバイスが接続されます。 次の手順を使用して、ローカル ネットワーク内のサーバーに接続し、Windows 8 あるいは Windows 8.1 を実行している Windows Phone またはコンピューターにサーバー証明書をインストールします。  
  
#### <a name="to-connect-to-your-server-from-your-windows-phone"></a>Windows Phone からサーバーに接続するには  
  
1.  Windows 8 または Windows 8.1 を実行している Windows Phone で、Internet Explorer を開きます。  
  
2.  アドレス バーに「 **http://<yourservername\>/connect/default.aspx?get=caroot.cer**、し、Enter キーを押します。  
  
3.  caroot.cer 証明書をインストールするメッセージが表示されたら、 **[インストール]** をクリックします。  
  
4.  証明書のインストールが完了するのを待ちます。  
  
    > [!NOTE]
    >  証明書のインストールが完了したら、サーバー名とネットワーク資格情報を使用して Windows Phone 用の My Server アプリにサインインできるようになります。  
  
#### <a name="to-connect-to-your-server-in-your-local-network-from-a-computer-running-windows-8-or-windows-81"></a>Windows 8 または Windows 8.1 を実行するコンピューターからローカル ネットワーク内のサーバーに接続するには  
  
1.  Windows 8 または Windows 8.1 を実行しているコンピューターで、Internet Explorer を開きます。  
  
2.  アドレス バーに「 **http://<yourservername\>/connect/default.aspx?get=caroot.cer**、し、Enter キーを押します。  
  
3.  caroot.cer 証明書をインストールするメッセージが表示されたら、 **[開く]** をクリックします。  
  
4.  **[証明書]** ダイアログ ボックスで、 **[証明書のインストール]** をクリックします。  
  
5.  証明書のインポート ウィザードで、保管場所として **[ローカル コンピューター]** を選択します。  
  
6.  **[証明書をすべて次のストアに配置する]** を選択し、 **[信頼されたルート証明機関]** の場所を参照します。  
  
7.  指示に従ってウィザードを完了します。  
  
    > [!NOTE]
    >  証明書のインストールが完了したら、サーバー名とネットワーク資格情報を使用して Windows 8 または Windows 8.1 用の My Server アプリにサインインできるようになります。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials - 第 1 部のサービスの統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials - パート 2 のサービスの統合の概要](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Anywhere Access を管理します。](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [リモートで作業します。](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の使用](Use-Windows-Server-Essentials.md)

-   [リモートで作業します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の使用](../use/Use-Windows-Server-Essentials.md)

