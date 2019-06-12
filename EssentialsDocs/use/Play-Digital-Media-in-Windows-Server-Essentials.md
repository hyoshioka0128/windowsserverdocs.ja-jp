---
title: Windows Server Essentials でのデジタル メディアの再生
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f570492-ee21-471b-92c1-3fd9bfb84f55
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f38d234768d40903615145954f1215546119344a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435940"
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Windows Server Essentials でのデジタル メディアの再生

>適用先:Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

デジタル メディアとは、デジタル圧縮されているオーディオ、動画、写真コンテンツを指します。  Windows Server Essentials およびことができますネットワーク コンピューターの一部のネットワーク上のデジタル メディア デバイスは、サーバーに保存されているデジタル メディア ファイルを再生します。  
  
 次のトピックでは、アクセスし、Windows Server Essentials に格納されているデジタル メディア ファイルを再生に関する情報を提供します。  
  

-   [デジタル メディアの概要](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [再生し、デジタル メディアを共有](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [リモートの場所から共有のデジタル メディア ファイルを再生します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [デジタル メディア ファイルをサーバーに追加します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [ダウンロード形式のオプション](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [簡単なファイルをアップロード ツール](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [表示および共有のデジタル メディアを参照](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

-   [デジタル メディアの概要](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [再生し、デジタル メディアを共有](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [リモートの場所から共有のデジタル メディア ファイルを再生します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [デジタル メディア ファイルをサーバーに追加します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [ダウンロード形式のオプション](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [簡単なファイルをアップロード ツール](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [表示および共有のデジタル メディアを参照](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

  
##  <a name="BKMK_1"></a> デジタル メディアの概要  
 デジタル メディアとは、コード化されている (デジタル圧縮されている) オーディオ、動画、写真コンテンツを指します。 コンテンツをコード化すると、オーディオや動画の入力が Windows Media ファイルなどのデジタル メディアに変換されます。 コード化したデジタル メディアはコンピューターで簡単に操作、配信、再生できます。コンピューター ネットワークで簡単に転送できます。  
  
 デジタル メディアの種類の例:Windows Media Audio (WMA)、Windows Media Video (WMV)、MP3、JPEG、AVI Windows Media Player でサポートされるデジタル メディアに関する詳細については、「 [Windows Media Player でサポートされるファイルの種類](https://support.microsoft.com/kb/316992)」を参照してください。  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>デジタル メディアをストリーム配信する理由とは  
 多くの人は、Windows Server Essentials での共有フォルダーに音楽、ビデオ、および画像を格納します。 次の操作を行う場合があります。  
  
-   **動画を見る**。 サーバーを利用し、動画と録画したテレビ番組の大量のコレクションを保存し、コンピューターやネットワーク上の他の再生機器にストリーム配信できます。 Windows Media Player を利用し、Xbox 360 やコンピューターに動画をストリーム配信できます。  
  
-   **音楽を再生する**。 **[ミュージック]** 共有フォルダーのメディア共有をオンにすると、Windows Media Connect をサポートするデバイスから音楽にアクセスできます。 共有をオンにすると、 **[ミュージック]** 共有フォルダーからストリーム配信するためにユーザー アカウントを有効にしたり、設定したりする必要はありません。  
  
-   **写真のスライドショーを行う**。 サーバーの **[フォト]** 共有フォルダーにデジタル写真を保存し、自宅または職場で、テレビに接続されているコンピューターまたは Xbox 360 からデジタル写真にアクセスできます。 写真をスライドショーで見ることができます。テレビが写真のための大きな額に変わります。  
  
### <a name="sharing-copy-protected-media"></a>コピー防止機能が付いたメディアを共有する  
  Windows Server Essentials では、コピーで保護されたメディアを共有することはできません。 これにはオンライン ミュージック ストアで購入した音楽が含まれます。  
  
 コピー防止機能が付いたメディアは、その購入に利用したコンピューターまたはデバイスでのみ再生できます。 コピー防止機能は、複数のコンピューターまたはデバイスでメディアを再生する行為を防ぐものです。メディアをサーバーにコピーし、そこから再生する場合も同様です。 ただし、Windows Server Essentials でのコピーで保護されたメディアを格納し、コンピューターまたは購入するために使用するデバイス上のメディアの再生を続行できます。  
  
##  <a name="BKMK_2"></a> 再生し、デジタル メディアを共有  
 ネットワークを設定し、コンピューターとメディア デバイスをサーバー ネットワークに接続すると、サーバーに保存し、共有しているデジタル メディア ファイルを検索できます。  
  
> [!NOTE]
>  Windows Server Essentials と互換性のあるデジタル メディア プレーヤー/受信デバイスの現在のリストを参照してください、 [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)します。  
  
 次の方法のいずれかを利用し、サーバーに保存されているデジタル メディア ファイルを検索できます。  
  

-   [検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials 上のメディア ファイルの再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player、Xbox 360、またはネットワークでネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials 上のメディア ファイルを送信します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

-   [検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials 上のメディア ファイルの再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player、Xbox 360、またはネットワークでネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials 上のメディア ファイルを送信します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

  
###  <a name="BKMK_2.1"></a> 検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials 上のメディア ファイルの再生  
 デバイスが Windows Server Essentials ネットワークに参加しているときに検索し、次の方法のいずれかでデジタル メディア ファイルを再生できます。  
  

-   [検索し、Windows Media Center を実行しているコンピューターからメディア ファイルの再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルの再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [検索し、Xbox 360 を使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [検索し、その他のデジタル メディア プレーヤーまたは Windows Server Essentials と互換性がある受信機を使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [検索し、リモート Web アクセスを使用して共有メディアを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

-   [検索し、Windows Media Center を実行しているコンピューターからメディア ファイルの再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルの再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [検索し、Xbox 360 を使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [検索し、その他のデジタル メディア プレーヤーまたは Windows Server Essentials と互換性がある受信機を使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [検索し、リモート Web アクセスを使用して共有メディアを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

  
####  <a name="BKMK_WMC"></a> 検索し、Windows Media Center を実行しているコンピューターからメディア ファイルの再生  
  
1.  **[スタート]** をクリックし、 **[すべてのプログラム]** をクリックし、 **[Windows Media Center]** をクリックします。  
  
2.  **[Windows Media Center]** ページで、検索するメディアの種類にスクロールし、メディア ライブラリをクリックします。  
  
3.  興味のあるファイルを手動で検索し、 **[検索]** をクリックし、探しているファイルの名前を入力します。  
  
4.  ファイルを表示または再生するにはメディア ファイルのイメージをクリックします。  
  
####  <a name="BKMK_MWP"></a> 検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルの再生  
  
-   コンピューターまたはメディア デバイスから、**Windows Media Player** を開き、メディア ライブラリを検索します。  
  
    > [!NOTE]
    >  検索手順は、使用している Windows Media Player のバージョンによって異なります。 詳細については、お使いのバージョンのヘルプをご覧ください。  
  
####  <a name="BKMK_Xbox"></a> 検索し、Xbox 360 を使用してメディア ファイルを再生  
  
1.  有線または無線接続で、ホーム ネットワークに Xbox 360 コンソールを接続します。  
  
2.  Windows Server Essentials を実行しているコンピューター、メディア共有を有効にします。 詳細については、トピックを参照してください。[メディア ストリーム配信のオンまたはオフ](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)します。  
  
3.  Xbox 360 コンソールを利用してデジタル メディア ファイルを再生するには  
  
    1.  **[マイ Xbox]** に進み、表示または再生するメディアの種類に応じて **[ビデオ ライブラリ]** 、 **[ミュージック ライブラリ]** 、または **[ピクチャ ライブラリ]** を選択します。  
  
    2.  サーバーの名前を選択します。  
  
        > [!NOTE]
        >  サーバーの名前が一覧にない場合、 **[コンピューター]** を選択し、 **[テスト接続]** をクリックします。  
  
    3.  ファイル一覧を閲覧し、再生する項目を選択します。  
  
####  <a name="BKMK_Other"></a> 検索し、その他のデジタル メディア プレーヤーまたは Windows Server Essentials と互換性がある受信機を使用してメディア ファイルを再生  
  
1.  [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home) にアクセスし、お使いのデジタル メディア プレーヤーまたはレシーバーが互換性のあるデバイスの一覧にあることを確認します。  
  
2.  検索手順はデジタル メディア プレーヤーによって異なるため、詳しい指示についてはお使いのデバイスのヘルプをご覧ください。  
  
####  <a name="BKMK_SharedFolders"></a> 検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生  
  
1.  Windows Server Essentials スタート パッドにサインインします。  
  
2.  スタート パッドから、 **[共有フォルダー]** をクリックします。 Windows Explorer ウィンドウが開き、サーバーにある共有フォルダーが表示されます。  
  
3.  **[検索]** ボックスにメディア ファイルの名前を入力します。 検索クエリの結果が表示されます。  
  
    > [!NOTE]
    >  あるいは、共有フォルダーをダブルクリックしてフォルダーの内容を閲覧できます。  
  
####  <a name="BKMK_RWA2"></a> 検索し、リモート Web アクセスを使用して共有メディアを再生  
  
1.  リモート Web アクセスにログオンします。  
  
2.  **[共有フォルダー]** をクリックします。 Web ページの **[共有フォルダー]** セクションに、サーバーにある共有フォルダーの一覧が表示されます。  
  
3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。  
  
###  <a name="BKMK_SendToDevice"></a> Windows Media Player、Xbox 360、またはネットワークでネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials 上のメディア ファイルを送信します。  
 **Windows Media Player** を利用し、必要なメディア ファイルを検索します。 メディア ファイルを右クリックし、 **[再生するコンピューター]** をクリックし、ネットワークに接続されているメディア デバイスにメディア ファイルを送信します。  
  
##  <a name="BKMK_3"></a> リモートの場所から共有のデジタル メディア ファイルを再生します。  
 リモート Web アクセスを使用して、Windows Server Essentials ネットワークから離れているときに、メディア ファイルを再生できます。 携帯電話、リモート コントローラー、デジタル メディア プレーヤーを利用し、サーバーに保存されている共有メディア ファイルを検索し、再生できます。  
  
#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>ネットワークから離れた場所にいるときに共有メディア ファイルを再生するには  
  
1. インターネット ブラウザーを開きます。  
  
2. リモート Web アクセスの Web サイトに進みます。 型**https://<YourDomainName\>/リモート**し Enter キーを押して、インターネット ブラウザーのアドレス バーにします。  
  
   > [!NOTE]
   >  *< ドメイン名\>* プレース ホルダーです。 アドレスを入力するようになりますので、サーバーに一意の名前がなります **https://contoso.com/remote** します。 ドメインの名前がわからない場合、リモート アクセス機能がサーバーに設定されたときにドメイン名を選択した管理者にお問い合わせください。 詳細については、「[リモート Web アクセス](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)」を参照してください。  
  
3. リモート Web アクセスのサインイン ページで、ユーザー アカウント名とパスワードを入力し、矢印をクリックします。  
  
4. 任意の方法を利用し、再生するメディア ファイルを検索します。  
  
   > [!NOTE]
   > 
   >  については、さまざまな検索方法を参照してください[コンピューターまたはネットワーク上のデジタル メディア プレーヤーから Windows Server Essentials でのプレイ メディア ファイルの検索と](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)します。  
   > 
   >  については、さまざまな検索方法を参照してください[コンピューターまたはネットワーク上のデジタル メディア プレーヤーから Windows Server Essentials でのプレイ メディア ファイルの検索と](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)します。  

  
5. メディア ファイル名が表示されたら、ファイル名をクリックし、メディアを再生します。  
  
##  <a name="BKMK_4"></a> デジタル メディア ファイルをサーバーに追加します。  

 サーバーの管理者は、サーバーに直接アクセスすることによって、またはリモート Web アクセス サイトを使用して、ダッシュ ボードにサインインして、メディア ライブラリに共有フォルダーにデジタル メディアを追加できます。 他のユーザーを使用して、サーバーにメディア ファイルを追加することができます、**共有フォルダー**スタート パッド、または Windows Phone の My Server アプリを使用して、リモート Web アクセス サイトを使用してに接続します。 メディアを再生する方法に関する詳細については、「[デジタル メディアを再生し、共有する](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。  

 サーバーの管理者は、サーバーに直接アクセスすることによって、またはリモート Web アクセス サイトを使用して、ダッシュ ボードにサインインして、メディア ライブラリに共有フォルダーにデジタル メディアを追加できます。 他のユーザーを使用して、サーバーにメディア ファイルを追加することができます、**共有フォルダー**スタート パッド、または Windows Phone の My Server アプリを使用して、リモート Web アクセス サイトを使用してに接続します。 メディアを再生する方法に関する詳細については、「[デジタル メディアを再生し、共有する](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)」を参照してください。  

  
> [!NOTE]
>  Windows Phone の My Server アプリを利用し、サーバーにメディア ファイルをアップロードすることもできます。 [Windows Phone ストア](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)から My Server アプリをダウンロードできます。 Windows Phone の My Server アプリに関する詳細については、ブログの投稿を参照してください。 [Windows Server Essentials の My Server phone アプリ](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)します。  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>サーバー上の共有フォルダーにデジタル メディア ファイルを追加するには  
  
1.  次の方法のいずれかを利用してサーバーにサインインします。  
  

    1.  リモート Web アクセスにログオンする方法については、次を参照してください。 [Use Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md)します。  

    1.  リモート Web アクセスにログオンする方法については、次を参照してください。 [Use Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)します。  

  
    2.  スタート パッドでサインイン方法の詳細については、次を参照してください。[スタート パッドの概要](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)します。  
  
2.  追加するメディアのフォルダーを検索し、クリックします。  
  
3.  追加するメディア ファイルをサーバー上の共有フォルダーにコピーして貼り付けるか、ドラッグアンドドロップします。  
  
##  <a name="BKMK_5"></a> ダウンロード形式のオプション  
 ファイルは 2 つの方法でダウンロードできます。 これらのオプションは、Windows ベースのコンピューターに複数のファイルまたはフォルダーをダウンロードする場合にのみ利用できます。  
  
 実行するダウンロードに合わせて次のオプションを選択します。  
  
- **圧縮された ZIP ファイル (.zip)**  
  
   ファイルを圧縮すると、元のファイルより小さい圧縮されたファイルが作成されます。 この圧縮されたファイルには「.zip」というファイル名拡張子が付きます。 圧縮することで最も高い縮小効果が得られるファイルはテキスト指向ファイルとグラフィックス ファイルです。テキスト指向ファイルには「.txt」、「.doc」、「.xls」などがあり、グラフィックス ファイル (非圧縮ファイル タイプを使用) には「.bmp」などがあります。 「.jpg」や「.gif」ファイルのような一部のグラフィックス ファイルでは圧縮技術が既に使用されており、圧縮してもファイル サイズはそれほど小さくなりません。 また、さまざまなグラフィックスを含む Word ドキュメントは、ほとんどがテキストのドキュメントほどには縮小されません。  
  
  > [!NOTE]
  >  このオプションで使用できるインターナショナル ファイル名は限られています。  
  
- **自己解凍実行可能ファイル (.exe)**  
  
   自己解凍実行ファイルは、解凍 (実行可能) プログラムと圧縮されたファイルを組み合わせたダウンロート可能ファイルです。 実行可能プログラムを実行すると、圧縮されたファイルが自動的に解凍されます。 これは圧縮データを配信する一般的な方法であり、受け取る人に適切な解凍ツールがあるかどうか心配する必要がありません。  
  
  > [!NOTE]
  >  このオプションでは Unicode 文字が使用できます。  
  
  実際のダウンロードが始まる前に、exe または zip ファイルが作成されます。 ダウンロードするファイルの数や合計サイズによっては、数分かかる場合があります。 ダウンロード ファイルが作成されると、バックグラウンドでファイルのダウンロードが始まります。 ダウンロードが完了するまで、作業を続けられます。  
  
##  <a name="BKMK_6"></a> 簡単なファイルをアップロード ツール  
 ファイルの簡単アップロード ツールには、Windows Server Essentials サーバー上のファイルのアップロード プロセスが効率化します。 ファイルの簡単アップロード ツールに必要な 1 つのバッチで Windows Server Essentials サーバー上の共有フォルダーにアップロードすると、多くのファイルを追加することができます。 詳細については、ブログ投稿の「 [リモート Web アクセス ファイル共有に関する理解](http://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx)」を参照してください。  
  
##  <a name="BKMK_7"></a> 表示および共有のデジタル メディアを参照  
 ダッシュボード、スタート パッド、リモート Web アクセスの Web サイト、Windows Phone の My Server のいずれかを利用し、リソースを表示または閲覧できます。  
  
#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>ダッシュボードから共有メディアを表示または閲覧するには  
  
1.  サーバー ダッシュボードを開きます。  
  
2.  メイン ナビゲーション バーで、 **[記憶域]** をクリックします。  
  
3.  **[サーバー フォルダー]** タブをクリックします。サーバー フォルダーの一覧が表示されます。  
  
4.  フォルダーをダブルクリックし、フォルダーの内容を表示します。  
  
#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>ネットワーク コンピューターからスタート パッドを利用し、共有メディアを表示し、閲覧するには  
  
1.  スタート パッドにサインインします。  
  
2.  **[共有フォルダー]** をクリックします。 Windows Explorer が開き、サーバーの共有フォルダーの一覧が表示されます。  
  
3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。  
  
#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>リモート Web アクセスを利用し、共有メディアを表示し、閲覧するには  
  
1.  リモート Web アクセスにログオンします。  
  
2.  **[共有フォルダー]** をクリックします。 Web ページの **[共有フォルダー]** セクションに、サーバーにある共有フォルダーの一覧が表示されます。  
  
3.  フォルダーをダブルクリックし、フォルダーの内容を表示します。  
  
## <a name="see-also"></a>関連項目  
  
-   [デジタル メディアを管理します。](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)  
  

-   [接続の確立します。](Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモートで作業します。](Work-Remotely-in-Windows-Server-Essentials.md)

-   [接続の確立します。](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [共有フォルダーの使用](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモートで作業します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)

