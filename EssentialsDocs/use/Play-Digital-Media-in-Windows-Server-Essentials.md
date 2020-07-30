---
title: Windows Server Essentials でのデジタル メディアの再生
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 5f570492-ee21-471b-92c1-3fd9bfb84f55
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c8f490f09f9623aa82b42f2103f2fd3e95537d7d
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409512"
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Windows Server Essentials でのデジタル メディアの再生

>適用対象: Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

デジタル メディアとは、デジタル圧縮されているオーディオ、動画、写真コンテンツを指します。  Windows Server Essentials を使用すると、ネットワーク接続されたコンピューターと一部のデジタルメディアデバイスは、サーバーに格納されているデジタルメディアファイルを再生できます。

 次のトピックでは、Windows Server Essentials に格納されているデジタルメディアファイルにアクセスして再生する方法について説明します。


-   [デジタル メディアの概要](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)

-   [デジタル メディアを再生し、共有する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)

-   [離れた場所からデジタル メディア ファイルを再生し、共有する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)

-   [デジタル メディア ファイルをサーバーに追加する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)

-   [ダウンロード形式のオプション](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)

-   [ファイルの簡単アップロードツール](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)

-   [共有デジタル メディアを表示し、閲覧する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)


##  <a name="digital-media-overview"></a><a name="BKMK_1"></a>デジタルメディアの概要
 デジタル メディアとは、コード化されている (デジタル圧縮されている) オーディオ、動画、写真コンテンツを指します。 コンテンツをコード化すると、オーディオや動画の入力が Windows Media ファイルなどのデジタル メディアに変換されます。 コード化したデジタル メディアはコンピューターで簡単に操作、配信、再生できます。コンピューター ネットワークで簡単に転送できます。

 デジタル メディアの種類の例:Windows Media Audio (WMA)、Windows Media Video (WMV)、MP3、JPEG、AVI Windows Media Player でサポートされるデジタル メディアに関する詳細については、「 [Windows Media Player でサポートされるファイルの種類](https://support.microsoft.com/kb/316992)」を参照してください。

### <a name="why-would-i-want-to-stream-my-digital-media"></a>デジタル メディアをストリーム配信する理由とは
 多くの方は、Windows Server Essentials の共有フォルダーに音楽、ビデオ、および画像を保存しています。 次の操作を行う場合があります。

-   **動画を見る**。 サーバーを利用し、動画と録画したテレビ番組の大量のコレクションを保存し、コンピューターやネットワーク上の他の再生機器にストリーム配信できます。 Windows Media Player を利用し、Xbox 360 やコンピューターに動画をストリーム配信できます。

-   **音楽を再生する**。 [**ミュージック**] 共有フォルダーのメディア共有をオンにすると、Windows Media Connect をサポートするデバイスから音楽にアクセスできます。 共有をオンにすると、[**ミュージック**] 共有フォルダーからストリーム配信するためにユーザー アカウントを有効にしたり、設定したりする必要はありません。

-   **写真のスライドショーを行う**。 サーバーの [ **フォト** ] 共有フォルダーにデジタル写真を保存し、自宅または職場で、テレビに接続されているコンピューターまたは Xbox 360 からデジタル写真にアクセスできます。 写真をスライドショーで見ることができます。テレビが写真のための大きな額に変わります。

### <a name="sharing-copy-protected-media"></a>コピー防止機能が付いたメディアを共有する
  Windows Server Essentials では、コピーによって保護されたメディアの共有はサポートされていません。 これにはオンライン ミュージック ストアで購入した音楽が含まれます。

 コピー防止機能が付いたメディアは、その購入に利用したコンピューターまたはデバイスでのみ再生できます。 コピー防止機能は、複数のコンピューターまたはデバイスでメディアを再生する行為を防ぐものです。メディアをサーバーにコピーし、そこから再生する場合も同様です。 ただし、コピーによって保護されたメディアを Windows Server Essentials に保存し、そのメディアの購入に使用したコンピューターまたはデバイスでメディアを再生し続けることができます。

##  <a name="play-and-share-digital-media"></a><a name="BKMK_2"></a>デジタルメディアを再生して共有する
 ネットワークを設定し、コンピューターとメディア デバイスをサーバー ネットワークに接続すると、サーバーに保存し、共有しているデジタル メディア ファイルを検索できます。

> [!NOTE]
>  Windows Server Essentials と互換性のあるデジタルメディアプレーヤー/受信デバイスの最新の一覧については、「 [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)」を参照してください。

 次の方法のいずれかを利用し、サーバーに保存されているデジタル メディア ファイルを検索できます。

-   [ネットワーク上のコンピューターまたはデジタルメディアプレーヤーから Windows Server Essentials 上のメディアファイルを検索して再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)

-   [Windows Server Essentials のメディアファイルを Windows Media Player、Xbox 360、またはネットワーク内のネットワークに接続されたデジタルメディアプレーヤーに送信する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)


###  <a name="search-for-and-play-media-files-on-windows-server-essentials-from-a-computer-or-digital-media-player-on-the-network"></a><a name="BKMK_2.1"></a>ネットワーク上のコンピューターまたはデジタルメディアプレーヤーから Windows Server Essentials 上のメディアファイルを検索して再生する
 デバイスが Windows Server Essentials ネットワークに参加している場合は、次のいずれかの方法でデジタルメディアファイルを検索して再生できます。


-   [Windows Media Center を実行するコンピューターからメディア ファイルを検索し、再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)

-   [Windows Media Player を利用し、Windows を実行しているコンピューターからメディア ファイルを検索し、再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)

-   [Xbox 360 を利用し、メディア ファイルを検索し、再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)

-   [Windows Server Essentials と互換性のある他のデジタルメディアプレーヤーまたはレシーバーを使用して、メディアファイルを検索して再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)

-   [スタート パッドの共有フォルダー機能を利用し、メディア ファイルを検索し、再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)

-   [リモート Web アクセスを利用し、共有メディアを検索し、再生する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)


####  <a name="search-for-and-play-media-files-from-a-computer-that-is-running-windows-media-center"></a><a name="BKMK_WMC"></a>Windows Media Center を実行しているコンピューターからメディアファイルを検索して再生する

1.  [**スタート**] をクリックし、[**すべてのプログラム**] をクリックし、[**Windows Media Center**] をクリックします。

2.  [**Windows Media Center**] ページで、検索するメディアの種類にスクロールし、メディア ライブラリをクリックします。

3.  興味のあるファイルを手動で検索し、[**検索**] をクリックし、探しているファイルの名前を入力します。

4.  ファイルを表示または再生するにはメディア ファイルのイメージをクリックします。

####  <a name="search-for-and-play-media-files-from-a-computer-that-is-running-windows-by-using-windows-media-player"></a><a name="BKMK_MWP"></a>Windows Media Player を使用して Windows を実行しているコンピューターからメディアファイルを検索して再生する

-   コンピューターまたはメディア デバイスから、**Windows Media Player** を開き、メディア ライブラリを検索します。

    > [!NOTE]
    >  検索手順は、使用している Windows Media Player のバージョンによって異なります。 詳細については、お使いのバージョンのヘルプをご覧ください。

####  <a name="search-for-and-play-media-files-by-using-xbox-360"></a><a name="BKMK_Xbox"></a>Xbox 360 を使用してメディアファイルを検索し、再生する

1.  有線または無線接続で、ホーム ネットワークに Xbox 360 コンソールを接続します。

2.  Windows Server Essentials を実行しているコンピューターで、メディア共有をオンにします。 詳細については、「[メディアストリーミングを有効または無効にする](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)」を参照してください。

3.  Xbox 360 コンソールを利用してデジタル メディア ファイルを再生するには

    1.  [**マイ Xbox**] に進み、表示または再生するメディアの種類に応じて [**ビデオ ライブラリ**]、[**ミュージック ライブラリ**]、または [**ピクチャ ライブラリ**] を選択します。

    2.  サーバーの名前を選択します。

        > [!NOTE]
        >  サーバーの名前が一覧にない場合、[**コンピューター**] を選択し、[**テスト接続**] をクリックします。

    3.  ファイル一覧を閲覧し、再生する項目を選択します。

####  <a name="search-for-and-play-media-files-by-using-other-digital-media-players-or-receivers-that-are-compatible-with-windows-server-essentials"></a><a name="BKMK_Other"></a>Windows Server Essentials と互換性のある他のデジタルメディアプレーヤーまたはレシーバーを使用して、メディアファイルを検索して再生する

1.  [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home) にアクセスし、お使いのデジタル メディア プレーヤーまたはレシーバーが互換性のあるデバイスの一覧にあることを確認します。

2.  検索手順はデジタル メディア プレーヤーによって異なるため、詳しい指示についてはお使いのデバイスのヘルプをご覧ください。

####  <a name="search-for-and-play-media-files-by-using-the-shared-folders-feature-of-the-launchpad"></a><a name="BKMK_SharedFolders"></a>スタートパッドの共有フォルダー機能を使用してメディアファイルを検索し、再生する

1.  Windows Server Essentials スタートパッドにサインインします。

2.  スタート パッドから、[**共有フォルダー**] をクリックします。 Windows Explorer ウィンドウが開き、サーバーにある共有フォルダーが表示されます。

3.  [**検索**] ボックスにメディア ファイルの名前を入力します。 検索クエリの結果が表示されます。

    > [!NOTE]
    >  あるいは、共有フォルダーをダブルクリックしてフォルダーの内容を閲覧できます。

####  <a name="search-for-and-play-shared-media-by-using-remote-web-access"></a><a name="BKMK_RWA2"></a>リモート Web アクセスを使用して共有メディアを検索し、再生する

1.  リモート Web アクセスにログオンします。

2.  **[共有フォルダー]** をクリックします。 Web ページの [**共有フォルダー**] セクションに、サーバーにある共有フォルダーの一覧が表示されます。

3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。

###  <a name="send-media-files-on-windows-server-essentials-to-windows-media-player-xbox-360-or-to-a-networked-digital-media-player-in-the-network"></a><a name="BKMK_SendToDevice"></a>Windows Server Essentials のメディアファイルを Windows Media Player、Xbox 360、またはネットワーク内のネットワークに接続されたデジタルメディアプレーヤーに送信する
 **Windows Media Player** を利用し、必要なメディア ファイルを検索します。 メディア ファイルを右クリックし、[**再生するコンピューター**] をクリックし、ネットワークに接続されているメディア デバイスにメディア ファイルを送信します。

##  <a name="play-shared-digital-media-files-from-a-remote-location"></a><a name="BKMK_3"></a>リモートの場所から共有デジタルメディアファイルを再生する
 リモート Web アクセスを使用すると、Windows Server Essentials ネットワークから離れているときに、メディアファイルを再生できます。 携帯電話、リモート コントローラー、デジタル メディア プレーヤーを利用し、サーバーに保存されている共有メディア ファイルを検索し、再生できます。

#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>ネットワークから離れた場所にいるときに共有メディア ファイルを再生するには

1. インターネット ブラウザーを開きます。

2. リモート Web アクセスの Web サイトに進みます。 インターネットブラウザーのアドレスバーに「 **https://<\> ** 」と入力し、enter キーを押します。

   > [!NOTE]
   >  *ドメイン名 \> の<* はプレースホルダーです。 これはサーバーに固有の名前であるため、入力したアドレスはのようになり **https://contoso.com/remote** ます。 ドメインの名前がわからない場合、リモート アクセス機能がサーバーに設定されたときにドメイン名を選択した管理者にお問い合わせください。 詳細については、「[リモート Web アクセス](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)」を参照してください。

3. リモート Web アクセスのサインイン ページで、ユーザー アカウント名とパスワードを入力し、矢印をクリックします。

4. 任意の方法を利用し、再生するメディア ファイルを検索します。

   > [!NOTE]
   >
   >  さまざまな検索方法の詳細については、「[ネットワーク上のコンピューターまたはデジタルメディアプレーヤーから Windows Server Essentials 上のメディアファイルを検索して再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)する」を参照してください。
   >
   >  さまざまな検索方法の詳細については、「[ネットワーク上のコンピューターまたはデジタルメディアプレーヤーから Windows Server Essentials 上のメディアファイルを検索して再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)する」を参照してください。


5. メディア ファイル名が表示されたら、ファイル名をクリックし、メディアを再生します。

##  <a name="add-digital-media-files-to-the-server"></a><a name="BKMK_4"></a>デジタルメディアファイルをサーバーに追加する

 サーバー管理者は、サーバーに直接アクセスするか、リモートの Web アクセスサイトを使用してダッシュボードにサインインすることにより、メディアライブラリの共有フォルダーにデジタルメディアを追加できます。 他のユーザーは、スタートパッドの [**共有フォルダー** ] 接続を使用するか、リモート Web アクセスサイトを使用するか、Windows Phone 用の My server アプリを使用して、サーバーにメディアファイルを追加できます。 メディアを再生する方法に関する詳細については、「[デジタル メディアを再生し、共有する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。

 サーバー管理者は、サーバーに直接アクセスするか、リモートの Web アクセスサイトを使用してダッシュボードにサインインすることにより、メディアライブラリの共有フォルダーにデジタルメディアを追加できます。 他のユーザーは、スタートパッドの [**共有フォルダー** ] 接続を使用するか、リモート Web アクセスサイトを使用するか、Windows Phone 用の My server アプリを使用して、サーバーにメディアファイルを追加できます。 メディアを再生する方法に関する詳細については、「[デジタル メディアを再生し、共有する](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。


> [!NOTE]
>  Windows Phone の My Server アプリを利用し、サーバーにメディア ファイルをアップロードすることもできます。 [Windows Phone ストア](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)から My Server アプリをダウンロードできます。 Windows Phone 用の My Server アプリの詳細については、ブログ記事「 [Windows Server Essentials 用の My server Phone アプリ](https://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)」を参照してください。

#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>サーバー上の共有フォルダーにデジタル メディア ファイルを追加するには

1.  次の方法のいずれかを利用してサーバーにサインインします。


    1.  リモート Web アクセスにログオンする方法の詳細については、「[リモート Web アクセスの使用](Use-Remote-Web-Access-in-Windows-Server-Essentials.md)」を参照してください。

    1.  リモート Web アクセスにログオンする方法の詳細については、「[リモート Web アクセスの使用](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)」を参照してください。


    2.  スタートパッドを使用したサインインの詳細については、「[スタートパッドの概要](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)」を参照してください。

2.  追加するメディアのフォルダーを検索し、クリックします。

3.  追加するメディア ファイルをサーバー上の共有フォルダーにコピーして貼り付けるか、ドラッグアンドドロップします。

##  <a name="download-format-options"></a><a name="BKMK_5"></a>ダウンロード形式のオプション
 ファイルは 2 つの方法でダウンロードできます。 これらのオプションは、Windows ベースのコンピューターに複数のファイルまたはフォルダーをダウンロードする場合にのみ利用できます。

 実行するダウンロードに合わせて次のオプションを選択します。

- **圧縮 ZIP ファイル (.zip)**

   ファイルを圧縮すると、元のファイルより小さい圧縮されたファイルが作成されます。 この圧縮されたファイルには「.zip」というファイル名拡張子が付きます。 圧縮することで最も高い縮小効果が得られるファイルはテキスト指向ファイルとグラフィックス ファイルです。テキスト指向ファイルには「.txt」、「.doc」、「.xls」などがあり、グラフィックス ファイル (非圧縮ファイル タイプを使用) には「.bmp」などがあります。 「.jpg」や「.gif」ファイルのような一部のグラフィックス ファイルでは圧縮技術が既に使用されており、圧縮してもファイル サイズはそれほど小さくなりません。 また、さまざまなグラフィックスを含む Word ドキュメントは、ほとんどがテキストのドキュメントほどには縮小されません。

  > [!NOTE]
  >  このオプションで使用できるインターナショナル ファイル名は限られています。

- **自己解凍実行ファイル (.exe)**

   自己解凍実行ファイルは、解凍 (実行可能) プログラムと圧縮されたファイルを組み合わせたダウンロート可能ファイルです。 実行可能プログラムを実行すると、圧縮されたファイルが自動的に解凍されます。 これは圧縮データを配信する一般的な方法であり、受け取る人に適切な解凍ツールがあるかどうか心配する必要がありません。

  > [!NOTE]
  >  このオプションでは Unicode 文字が使用できます。

  実際のダウンロードが始まる前に、exe または zip ファイルが作成されます。 ダウンロードするファイルの数や合計サイズによっては、数分かかる場合があります。 ダウンロード ファイルが作成されると、バックグラウンドでファイルのダウンロードが始まります。 ダウンロードが完了するまで、作業を続けられます。

##  <a name="easy-file-upload-tool"></a><a name="BKMK_6"></a>ファイルの簡単アップロードツール
 ファイルの簡単アップロードツールを使用すると、Windows Server Essentials サーバーにファイルをアップロードするプロセスを効率化できます。 ファイルの簡単アップロードツールに任意の数のファイルを追加し、それを1つのバッチ内の Windows Server Essentials サーバー上の共有フォルダーにアップロードすることができます。 詳細については、ブログ投稿の「 [リモート Web アクセス ファイル共有に関する理解](https://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx)」を参照してください。

##  <a name="view-and-browse-shared-digital-media"></a><a name="BKMK_7"></a>共有デジタルメディアの表示と参照
 ダッシュボード、スタート パッド、リモート Web アクセスの Web サイト、Windows Phone の My Server のいずれかを利用し、リソースを表示または閲覧できます。

#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>ダッシュボードから共有メディアを表示または閲覧するには

1.  サーバー ダッシュボードを開きます。

2.  メイン ナビゲーション バーで、[**記憶域**] をクリックします。

3.  [**サーバーフォルダー** ] タブをクリックします。サーバーフォルダーの一覧が表示されます。

4.  フォルダーをダブルクリックし、フォルダーの内容を表示します。

#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>ネットワーク コンピューターからスタート パッドを利用し、共有メディアを表示し、閲覧するには

1.  スタート パッドにサインインします。

2.  **[共有フォルダー]** をクリックします。 Windows Explorer が開き、サーバーの共有フォルダーの一覧が表示されます。

3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。

#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>リモート Web アクセスを利用し、共有メディアを表示し、閲覧するには

1.  リモート Web アクセスにログオンします。

2.  **[共有フォルダー]** をクリックします。 Web ページの [**共有フォルダー**] セクションに、サーバーにある共有フォルダーの一覧が表示されます。

3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。

## <a name="additional-references"></a>その他のリファレンス

-   [デジタル メディアの管理](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)

-   [接続の取得](Get-Connected-in-Windows-Server-Essentials.md)

-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)

-   [リモートで作業する](Work-Remotely-in-Windows-Server-Essentials.md)
