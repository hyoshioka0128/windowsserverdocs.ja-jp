---
title: "Windows Server Essentials でデジタル メディアを再生します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 8228d0b17a58858ed893181ddceb465715ffdeb5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Windows Server Essentials でデジタル メディアを再生します。

>適用対象: Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

デジタル メディアは、オーディオ、ビデオ、およびデジタル圧縮されている写真コンテンツを指します。  Windows Server Essentials により、ネットワーク上のコンピューターと一部のネットワーク上のデジタル メディア デバイス、サーバーに保存されているデジタル メディア ファイルを再生します。  
  
 次のトピックでは、アクセスし、Windows Server Essentials に保存されているデジタル メディア ファイルを再生に関する情報を提供します。  
  

-   [デジタル メディアの概要](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [プレイし、デジタル メディアを共有します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [リモートの場所から共有デジタル メディア ファイルを再生します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [デジタル メディア ファイルをサーバーに追加します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [ダウンロード形式のオプション](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [容易なファイルのアップロード ツール](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [表示し、共有のデジタル メディアの閲覧](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

-   [デジタル メディアの概要](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [プレイし、デジタル メディアを共有します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [リモートの場所から共有デジタル メディア ファイルを再生します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [デジタル メディア ファイルをサーバーに追加します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [ダウンロード形式のオプション](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [容易なファイルのアップロード ツール](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [表示し、共有のデジタル メディアの閲覧](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

  
##  <a name="BKMK_1"></a>デジタル メディアの概要  
 デジタル メディアは、オーディオ、ビデオ、および (デジタル圧縮) エンコードされている写真コンテンツを指します。 コンテンツをエンコードすると、オーディオとビデオの入力が Windows Media ファイルなどのデジタル メディア ファイルに変換する必要があります。 デジタル メディアをエンコードするに簡単に操作、分散、およびできコンピューターによって再生、コンピューター ネットワーク経由で送信される簡単にします。  
  
 デジタル メディアの種類の例: Windows Media オーディオ (WMA)、Windows Media Video (WMV)、MP3、JPEG、AVI します。 Windows Media Player でサポートされているデジタル メディアの種類については、次を参照してください。[ファイルの種類が Windows Media Player でサポートされている](https://support.microsoft.com/kb/316992)します。  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>デジタル メディアをストリーム配信必要なはなぜですか。  
 多くのユーザーは、Windows Server Essentials での共有フォルダーに音楽、ビデオ、および画像を保存します。 実行する場合がある可能性がありますに従って。  
  
-   **ビデオを視聴**します。 保存し、ビデオの大量のコレクションをストリーム配信するサーバーを使用できるし、録画したテレビ番組、コンピューターやその他の再生デバイス、ネットワーク上でします。 Windows Media Player を使用して、Xbox 360、またはコンピューターのビデオをストリーミングすることができます。  
  
-   **音楽を再生する**します。 メディア共有をオンにすると、**音楽**共有フォルダは、Windows Media Connect をサポートするデバイスから音楽にアクセスすることができます。 有効にするか、またはからストリーム配信するすべてのユーザー アカウントを構成する必要はありません、**音楽**共有フォルダーの共有をオンにした後です。  
  
-   **写真のスライド ショーを提示**します。 デジタル写真を保存することができます、**写真**サーバー上のフォルダーを共有し、任意のコンピューターから、または、自宅または職場で、テレビに接続されている Xbox 360 からそれらにアクセスします。 これは大きな額にお使いのテレビをショー写真のスライド ショーを視聴できます。  
  
### <a name="sharing-copy-protected-media"></a>コピーで保護されているメディアの共有  
  Windows Server Essentials では、コピーで保護されたメディアを共有することはできません。 これには、オンライン ミュージック ストアを通じて購入した音楽が含まれます。  
  
 Copy-protected メディアは、コンピューターまたは購入するために使用するデバイスでのみ再生できます。 コピー防止には、メディアをサーバーにコピーし、そこから再生した場合でも、1 つ以上のコンピューター/デバイス、メディアを再生できないようにします。 ただし、Windows Server Essentials でのコピーで保護されたメディアを保存し、コンピューターまたは購入するために使用するデバイスでのメディアを再生を続行できます。  
  
##  <a name="BKMK_2"></a>プレイし、デジタル メディアを共有します。  
 ネットワークをセットアップし、サーバー ネットワークに、コンピューターとメディア デバイスを正常に接続した後は、デジタル メディア ファイルを保存して、サーバーで共有を検索できます。  
  
> [!NOTE]
>  現在の Windows Server Essentials と互換性のあるデジタル メディア プレーヤー/受信デバイスの一覧を表示するには、次を参照してください。、[Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)します。  
  
 検索し、サーバーに保存されているデジタル メディア ファイルを再生するには、次の方法のいずれかを使用することができます。  
  

-   [検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials にあるメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player、Xbox 360、またはネットワークのネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials にあるメディア ファイルを送信します。](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

-   [検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials にあるメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Windows Media Player、Xbox 360、またはネットワークのネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials にあるメディア ファイルを送信します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

  
###  <a name="BKMK_2.1"></a>検索し、ネットワーク上のコンピューターまたはデジタル メディア プレーヤーから Windows Server Essentials にあるメディア ファイルを再生  
 デバイスが Windows Server Essentials ネットワークに参加している場合を検索し、次の方法のいずれかでデジタル メディア ファイルを再生できます。  
  

-   [検索し、Windows Media Center を実行しているコンピューターからメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [検索し、Xbox 360 を使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [検索し、その他のデジタル メディア プレーヤーまたはレシーバーの Windows Server Essentials と互換性のあるを使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [検索し、リモート Web アクセスを使用して、共有メディアを再生](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

-   [検索し、Windows Media Center を実行しているコンピューターからメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [検索し、Xbox 360 を使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [検索し、その他のデジタル メディア プレーヤーまたはレシーバーの Windows Server Essentials と互換性のあるを使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [検索し、リモート Web アクセスを使用して、共有メディアを再生](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

  
####  <a name="BKMK_WMC"></a>検索し、Windows Media Center を実行しているコンピューターからメディア ファイルを再生  
  
1.  をクリックして**開始**、] をクリックして**すべてのプログラム**、] をクリックし、**Windows Media Center**します。  
  
2.  **Windows Media Center** ] ページで、検索するメディアの種類にスクロールし、メディア ライブラリ] をクリックします。  
  
3.  、興味のある] をクリックするか、ファイルを手動で検索**検索**し検索するファイルの名前を入力します。  
  
4.  表示またはファイルを再生するメディア ファイルのイメージをクリックします。  
  
####  <a name="BKMK_MWP"></a>検索し、Windows Media Player を使用して Windows を実行しているコンピューターからメディア ファイルを再生  
  
-   コンピューターまたはメディア デバイスから開く**Windows Media Player**と、メディア ライブラリを検索します。  
  
    > [!NOTE]
    >  検索手順は、使用している Windows Media Player のバージョンによって異なります。 詳細については、お使いのヘルプを参照してください。  
  
####  <a name="BKMK_Xbox"></a>検索し、Xbox 360 を使用してメディア ファイルを再生  
  
1.  ワイヤード (有線) またはワイヤレス接続を使用して、Xbox 360 本体をホーム ネットワークに接続します。  
  
2.  Windows Server Essentials を実行しているコンピューターでは、メディアの共有をオンにします。 詳細については、トピックを参照してください。[メディア ストリーム配信のオンまたはオフに](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)します。  
  
3.  デジタル メディア ファイルを再生、Xbox 360 コンソールを使用します。  
  
    1.  移動**マイ Xbox**、し、[**ビデオ ライブラリ**、**ミュージック ライブラリ**、または**画像ライブラリ**表示または再生するメディアの種類に応じて、します。  
  
    2.  サーバーの名前を選択します。  
  
        > [!NOTE]
        >  サーバーの名前が表示されない場合は、選択**コンピューター**、] をクリックし、**接続のテスト**します。  
  
    3.  ファイルの一覧を参照し、再生する項目を選択します。  
  
####  <a name="BKMK_Other"></a>検索し、その他のデジタル メディア プレーヤーまたはレシーバーの Windows Server Essentials と互換性のあるを使用してメディア ファイルを再生  
  
1.  移動、[Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)し、デジタル メディア プレーヤーまたはレシーバーが互換性のあるデバイスの一覧に表示されているかどうかを確認します。  
  
2.  検索手順は、使用しているデジタル メディア プレーヤーによって異なる、ために詳細な手順については、デバイスのヘルプを参照してください。  
  
####  <a name="BKMK_SharedFolders"></a>検索し、スタート パッドの共有フォルダー機能を使用してメディア ファイルを再生  
  
1.  Windows Server Essentials スタート パッドにログインします。  
  
2.  クリックし、スタート パッド**共有フォルダー**します。 Windows エクスプ ローラー ウィンドウが開き、サーバー上の共有フォルダーを表示します。  
  
3.  **検索**ボックスにメディア ファイルの名前を入力します。 検索クエリの結果が表示されます。  
  
    > [!NOTE]
    >  オプションとして、フォルダーの内容を参照する共有フォルダーをダブルクリックすることもできます。  
  
####  <a name="BKMK_RWA2"></a>検索し、リモート Web アクセスを使用して、共有メディアを再生  
  
1.  リモート Web アクセスにログオンします。  
  
2.  をクリックして**共有フォルダーの**します。 **共有フォルダー** Web ページのセクションでは、サーバー上の共有フォルダーの一覧が表示されます。  
  
3.  フォルダーの内容を表示するフォルダーをダブルクリックします。  
  
###  <a name="BKMK_SendToDevice"></a>Windows Media Player、Xbox 360、またはネットワークのネットワーク対応デジタル メディア プレーヤーには、Windows Server Essentials にあるメディア ファイルを送信します。  
 使用**Windows Media Player**するメディア ファイルを検索します。 メディア ファイルを右クリックし、をクリックして**リモート再生を**ネットワーク メディア デバイスにメディア ファイルを送信します。  
  
##  <a name="BKMK_3"></a>リモートの場所から共有デジタル メディア ファイルを再生します。  
 リモート Web アクセスを使用して、Windows Server Essentials ネットワークから離れているときに、メディア ファイルを再生することができます。 携帯電話、リモート コンピューターまたはデジタル メディア プレーヤーを使用して、検索し、サーバー上に保存されている共有メディア ファイルを再生することができます。  
  
#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>ネットワークから離れているときに、共有メディア ファイルを再生するには  
  
1.  インターネット ブラウザーを開きます。  
  
2.  リモート Web アクセス Web サイトに移動します。 種類**https://<YourDomainName\>/remote**し、Enter キーを押します、インターネット ブラウザーのアドレス バーにします。  
  
    > [!NOTE]
    >  *< YourDomainName\ >*プレース ホルダーです。 アドレスを入力するようになりますように、サーバーに一意である名であることが**https://contoso.com/remote**します。 コンピューターのドメイン名を把握していない場合、サーバー上でリモート アクセス機能が設定されている場合、ドメイン名を選択したを管理者に依頼します。 詳細については、次を参照してください。[リモート Web アクセスを有効にする](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)します。  
  
3.  リモート Web アクセスのサインイン] ページで、ユーザー アカウント名とパスワードを入力し、矢印をクリックします。  
  
4.  再生するメディア ファイルを検索する任意の方法を使用します。  
  
    > [!NOTE]

    >  については、さまざまな検索方法を参照してください[コンピューターまたはネットワーク上のデジタル メディア プレーヤーから Windows Server Essentials にある再生メディア ファイルを検索して](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)します。  

    >  については、さまざまな検索方法を参照してください[コンピューターまたはネットワーク上のデジタル メディア プレーヤーから Windows Server Essentials にある再生メディア ファイルを検索して](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)します。  

  
5.  メディア ファイルの名前が表示されたら、メディアを再生するファイル名をクリックします。  
  
##  <a name="BKMK_4"></a>デジタル メディア ファイルをサーバーに追加します。  

 サーバー管理者はサーバーに直接アクセスするか、ダッシュ ボードへのログインにリモート Web アクセス サイトを使用して、メディア ライブラリ共有のフォルダーにデジタル メディアを追加できます。 その他のユーザーを使用してサーバーにメディア ファイルを追加することができます、**共有フォルダー**または Windows Phone の My Server アプリを使用して、リモート Web アクセス サイトを使用して、スタート パッドに接続します。 メディアを再生する方法については、次を参照してください。[プレイし、デジタル メディアを共有](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)します。  

 サーバー管理者はサーバーに直接アクセスするか、ダッシュ ボードへのログインにリモート Web アクセス サイトを使用して、メディア ライブラリ共有のフォルダーにデジタル メディアを追加できます。 その他のユーザーを使用してサーバーにメディア ファイルを追加することができます、**共有フォルダー**または Windows Phone の My Server アプリを使用して、リモート Web アクセス サイトを使用して、スタート パッドに接続します。 メディアを再生する方法については、次を参照してください。[プレイし、デジタル メディアを共有](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)します。  

  
> [!NOTE]
>  Windows Phone の My Server アプリを使用してサーバーにメディア ファイルをアップロードすることもできます。 My Server アプリをダウンロードすることができます、[Windows Phone ストア](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)します。 Windows Phone の My Server アプリに関する詳細については、ブログ記事を参照してください。[Windows Server Essentials の My Server phone アプリ](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)します。  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>サーバー上の共有フォルダーにデジタル メディア ファイルを追加するには  
  
1.  サーバーにログインするには、次の方法のいずれかを使用します。  
  

    1.  リモート Web アクセスにログオン詳細については、次を参照してください。[リモート Web アクセスの使用](Use-Remote-Web-Access-in-Windows-Server-Essentials.md)します。  

    1.  リモート Web アクセスにログオン詳細については、次を参照してください。[リモート Web アクセスの使用](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)します。  

  
    2.  スタート パッドを使用してログインの詳細については、次を参照してください。[スタート パッドの概要](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)します。  
  
2.  検索し、追加するメディアのフォルダーをクリックします。  
  
3.  コピーや貼り付け、ドラッグ アンド ドロップ、メディア ファイルを適切なを追加することは、サーバー上のフォルダーを共有します。  
  
##  <a name="BKMK_5"></a>ダウンロード形式のオプション  
 ファイルをダウンロードするための 2 つのオプションがあります。 これらのオプションは、Windows ベースのコンピューターに複数のファイルまたはフォルダーをダウンロードする場合にのみ使用します。  
  
 ダウンロードのニーズに合った次のオプションを選択します。  
  
-   **圧縮された ZIP ファイル (.zip)**  
  
     ファイルを圧縮して、元のファイルよりも小さいファイルの圧縮バージョンを作成します。 ファイルの圧縮バージョンは、ファイル名拡張子が .zip します。 圧縮することで、最もが削減されるファイルの種類はテキスト指向ファイルの種類 (.txt、.doc、および .xls) などとグラフィックス ファイル (.bmp) などの非圧縮ファイル タイプを使用します。 一部のグラフィックス ファイルなど、.jpg、.gif ファイルでは、既に圧縮を使用し、ファイル サイズが縮小圧縮することでごくわずかです。 また、さまざまなグラフィックスを含む Word ドキュメントはテキストではほとんどの場合は、ドキュメントほど減少しません。  
  
    > [!NOTE]
    >  このオプションは、インターナショナル ファイル名、限定的なサポートを提供します。  
  
-   **自己解凍実行ファイル (.exe)**  
  
     自己解凍実行可能ファイルは、解凍 (実行可能) プログラムを組み合わせて、圧縮されたファイルをダウンロードできるファイルです。 実行可能プログラムを実行すると、圧縮されたファイルに自動的に展開します。 これは、受信者が適切な解凍ツールにあるかどうか心配せずに圧縮されたデータを配布する一般的な方法です。  
  
    > [!NOTE]
    >  このオプションは、Unicode 文字をサポートします。  
  
 実際のダウンロードを開始する前に、.exe ファイルか .zip ファイルが作成されます。 ファイルの数とに応じてダウンロードされるファイルの合計サイズ、このに数分かかる場合があります。 ダウンロード ファイルが作成された後は、ファイルをダウンロードするバック グラウンドで発生します。 これにより、ダウンロード プロセスが完了するまでの作業を続行できます。  
  
##  <a name="BKMK_6"></a>容易なファイルのアップロード ツール  
 ファイルの簡単アップロード ツールには、Windows Server Essentials サーバー上のファイルをアップロードするプロセスが合理化されます。 ファイルの簡単アップロード ツールに必要な 1 つのバッチで Windows Server Essentials サーバー上の共有フォルダーにアップロードすると、多くのファイルを追加することができます。 詳細については、ブログ記事を参照してください。[理解リモート Web アクセス ファイル共有](http://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx)します。  
  
##  <a name="BKMK_7"></a>表示し、共有のデジタル メディアの閲覧  
 表示したり、Windows Phone のダッシュ ボード、スタート パッド、リモート Web アクセス Web サイトまたは My Server アプリを使用してリソースを参照することができます。  
  
#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>表示し、ダッシュ ボードから共有メディアを閲覧するには  
  
1.  サーバー ダッシュ ボードを開きます。  
  
2.  メイン ナビゲーション バーをクリックして**記憶域**します。  
  
3.  をクリックして、**サーバー フォルダー** ] タブ。サーバー フォルダーの一覧が表示されます。  
  
4.  フォルダーの内容を表示するフォルダーをダブルクリックします。  
  
#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>表示し、ネットワーク コンピューターからスタート パッドを使用して、共有メディアを閲覧するには  
  
1.  スタート パッドにログインします。  
  
2.  をクリックして**共有フォルダーの**します。 Windows エクスプ ローラーが開き、サーバー上で共有フォルダーの一覧を表示します。  
  
3.  フォルダーの内容を表示するフォルダーをダブルクリックします。  
  
#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>表示し、リモート Web アクセスを使用して、共有メディアを閲覧するには  
  
1.  リモート Web アクセスにログオンします。  
  
2.  をクリックして**共有フォルダーの**します。 **共有フォルダー** Web ページのセクションでは、サーバー上の共有フォルダーの一覧が表示されます。  
  
3.  フォルダーの内容を表示するフォルダーをダブルクリックします。  
  
## <a name="see-also"></a>参照してください。  
  
-   [デジタル メディアを管理します。](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)  
  

-   [接続します。](Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモート操作します。](Work-Remotely-in-Windows-Server-Essentials.md)

-   [接続します。](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [共有フォルダーの使用](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [リモート操作します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)

