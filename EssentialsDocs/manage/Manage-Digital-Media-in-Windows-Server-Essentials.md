---
title: Windows Server Essentials でのデジタル メディアの管理
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9378bffa-487c-43ca-9ec3-7e7864d2dd9a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 87ec5218455672cbfd2bc1d77244fd263b91362c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433302"
---
# <a name="manage-digital-media-in-windows-server-essentials"></a>Windows Server Essentials でのデジタル メディアの管理

>適用先:Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

次のトピックでは、サーバーのメディア ストリーム配信機能と、ネットワークでメディア ストリーム配信を設定し、使用する方法について説明します。  
  
> [!NOTE]
>  既定では、メディア ストリーミング機能がない Windows Server Essentials と Windows Server 2012 R2、Windows Server Essentials エクスペリエンス役割がインストールされました。 これらのバージョンでメディア ストリーム配信機能を追加するには、Microsoft Download Center から [Windows Server Essentials Media Pack をダウンロードし、インストール](https://www.microsoft.com/download/details.aspx?id=40837) します。  
  
-   [デジタル メディアの概要](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [ダッシュ ボードを使用してメディア サーバーを管理します。](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [メディア ストリーミングのしくみ](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [メディア ストリーム配信のオン/オフ](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [デジタル メディア ファイルをサーバーに追加します。](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [許可またはサーバー上のメディア ライブラリへのアクセス制限](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [メディア ライブラリ名の変更します。](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [デジタル メディアの共有を停止します。](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [サーバー上の共有ファイルにアクセスするサーバー メッセージ ブロック (SMB) プロトコルを使用するメディア デバイスを有効にします。](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [共通プロセッサとビデオのプロファイルをサポート](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_CommonProcessors)  
  
-   [メディア ファイルの種類に関する既知の問題](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_KnownIssues)  
  
##  <a name="BKMK_1"></a> デジタル メディアの概要  
 デジタル メディアとは、コード化されている (デジタル圧縮されている) オーディオ、動画、写真コンテンツを指します。 コンテンツをコード化すると、オーディオや動画の入力が Windows Media ファイルなどのデジタル メディアに変換されます。 コード化したデジタル メディアはコンピューターで簡単に操作、配信、再生できます。コンピューター ネットワークで簡単に転送できます。  
  
 デジタル メディアの種類の例:Windows Media Audio (WMA)、Windows Media Video (WMV)、MP3、JPEG、AVI Windows Media Player でサポートされるデジタル メディアに関する詳細については、「 [Windows Media Player でサポートされるファイルの種類](https://support.microsoft.com/kb/316992)」を参照してください。  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>デジタル メディアをストリーム配信する理由とは  
 多くの人は、Windows Server Essentials での共有フォルダーに音楽、ビデオ、および画像を格納します。 次の操作を行うことがあります。  
  
-   **動画を見る**。 サーバーを利用し、動画と録画したテレビ番組の大量のコレクションを保存し、コンピューターやネットワーク上の他の再生機器にストリーム配信できます。 Windows Media Player を利用し、Xbox 360 やコンピューターに動画をストリーム配信できます。  
  
-   **音楽を再生する**。 **[ミュージック]** 共有フォルダーのメディア共有をオンにすると、Windows Media Connect をサポートするデバイスから音楽にアクセスできます。 共有をオンにすると、 **[ミュージック]** 共有フォルダーからストリーム配信するためにユーザー アカウントを有効にしたり、設定したりする必要はありません。  
  
-   **写真のスライドショーを行う**。 サーバーの **[フォト]** 共有フォルダーにデジタル写真を保存し、自宅または職場で、テレビに接続されているコンピューターまたは Xbox 360 からデジタル写真にアクセスできます。 写真をスライドショーで見ることができます。テレビが写真のための大きな額に変わります。  
  
###  <a name="BKMK_1.5"></a> メディアのコピーで保護された共有  
  Windows Server Essentials では、コピーで保護されたメディアを共有することはできません。 これにはオンライン ミュージック ストアで購入した音楽が含まれます。  
  
 コピー防止機能が付いたメディアは、その購入に利用したコンピューターまたはデバイスでのみ再生できます。 コピー防止機能は、複数のコンピューターまたはデバイスでメディアを再生する行為を防ぐものです。メディアをサーバーにコピーし、そこから再生する場合も同様です。 ただし、Windows Server Essentials でのコピーで保護されたメディアを格納し、コンピューターまたは購入するために使用するデバイス上のメディアの再生を続行できます。  
  
##  <a name="BKMK_2"></a> ダッシュ ボードを使用してメディア サーバーを管理します。  
  Windows Server Essentials では、Windows Server Essentials ダッシュ ボードを使用して一般的な管理タスクを実行できます。 ダッシュボードの **[サーバー設定]** ページの **[メディア]** タブは次の機能を提供します。  
  
|セクション|機能|  
|-------------|-------------------|  
|メディア サーバー|**[オン/オフ]** ボタンでは、メディア ストリーム配信のオンとオフを切り替えることができます。|  
|動画ストリーム配信の画質|ドロップダウン矢印で、サーバーから再生する動画のストリーム配信時の画質を選択できます。|  
|メディア ライブラリ|メディア ライブラリの名前を表示します。 ライブラリの既定の名前は「 **Digital Media Library**」です。これはメディア ストリーム配信をオンにしたときに作成されます。 メディア ライブラリの名前を変更する方法については、「[メディア ライブラリの名前を変更する](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)」を参照してください。 **[カスタマイズ]** をクリックし、メディア ライブラリで共有するフォルダーをカスタマイズできます。|  
  
 詳細については、「[サーバーのメディア ライブラリを許可または制限する](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)」と「[コピー防止機能が付いたメディアの共有](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1.5)」を参照してください。  
  
##  <a name="BKMK_3"></a> メディア ストリーミングのしくみ  
 メディア ストリーム配信機能 Windows Server Essentials では、ネットワーク、コンピューターと一部のネットワーク対応デジタル メディア デバイス、サーバーに保存されているデジタル メディア ファイルを再生できます。  
  
 メディア サーバーをオンにすると、メディア ライブラリで共有しているコンテンツをサーバーからストリーム配信されるメディアを受信できるネットワーク上のデバイスで再生できます。 ほとんどの種類のデジタル メディア ファイルをストリーム配信できます。 最も一般的なストリーム配信可能ファイルには次のようなものがあります。  
  
- Windows Media 形式 (.asf、.wma、.wmv、.wm)  
  
- Audio Visual Interleave (.avi)  
  
- Moving Pictures Experts Group (.mpeg、.mpg、.mp3)  
  
- Audio for Windows (.wav)  
  
- CD Audio Track (.cda)  
  
  ファイルを再生するには、共有フォルダーにある曲、動画、写真を見つけ、ファイルをダブルクリックします。コンテンツがサーバーからコンピューターにストリーム配信され、再生されます。 検索して、サーバーに格納されているデジタル メディア ファイルを再生する方法については、次を参照してください。 [Play Digital Media](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)します。  
  
  メディアをストリーム配信するには、次のハードウェアが必要です。  
  
- 有線または無線のプライベート ネットワーク  
  
- ネットワーク上の別のコンピューターまたはデジタル メディア レシーバー (またはネットワーク対応デジタル メディア プレーヤー) と呼ばれているデバイス デジタル メディア レシーバーは、コンピューターを使用して制御することができます、ワイヤード (有線) またはワイヤレス ネットワークに接続されているハードウェア デバイスですか? 場合でも、コンピューターが別の部屋にします。  
  
  詳細については、次を参照してください。[メディア ストリーム配信のオンまたはオフ](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)します。  
  
##  <a name="BKMK_4"></a> メディア ストリーム配信のオン/オフ  
 ファイルをサポートされているデジタル メディア レシーバー (DMR) など、コンピューター、携帯電話、テレビ、デジタル メディア レシーバー エクステンダー (Xbox を含む、Windows Media Center のストリーミングで音楽、ビデオ、および Windows Server Essentials から画像を共有することができます。360)、およびその他の個人向け電子機器。  
  
 現在の Windows Server Essentials と互換性のあるデジタル メディア デバイスの一覧を表示するには、次を参照してください。、 [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)します。  
  
### <a name="enabling-media-sharing"></a>メディア共有を有効にする  
 Windows Server Essentials で保存されているメディアを共有するには、メディア ストリーミングを有効にする必要があります。 メディア ストリーム配信は既定でオフになっています。  
  
####  <a name="BKMK_2.5"></a> メディア ストリーム配信のオンまたはオフに  
  
1. Windows Server Essentials ダッシュ ボードを開きます。  
  
2. **[設定]** をクリックし、 **[メディア]** をクリックし、次のいずれかの操作を行います。  
  
   -   **[オンにする]** をクリックし、サーバーのメディア ライブラリに保存されているすべてのファイルの共有を開始します。  
  
   -   **[オフにする]** をクリックし、サーバーのメディア ライブラリに保存されているすべてのファイルの共有を停止します。  
  
3. メディア ライブラリの追加フォルダーを共有する場合、 **[カスタマイズ]** をクリックし、メディア ライブラリに保存する共有フォルダーごとに **[はい]** を選択します。  
  
4. **[OK]** をクリックして変更を保存します。  
  
   Windows Media Player でサポートされるデジタル メディア タイプに関する詳細については、「 [Windows Media Player でサポートされるファイルの種類](https://support.microsoft.com/kb/316992)」を参照してください。  
  
   詳細については、「 [Allow or restrict access to a media library on the server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)」を参照してください。  
  
##  <a name="BKMK_5"></a> デジタル メディア ファイルをサーバーに追加します。  
 サーバーの管理者は、サーバーに直接アクセスすることによって、またはリモート Web アクセス サイトを使用して、ダッシュ ボードにサインインして、メディア ライブラリに共有フォルダーにデジタル メディアを追加できます。 他のユーザーを使用して、サーバーにメディア ファイルを追加することができます、**共有フォルダー**スタート パッド、または Windows Phone の My Server アプリを使用して、リモート Web アクセス サイトを使用してに接続します。 メディアの再生方法の詳細については、次を参照してください。 [Play Digital Media](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)します。  
  
> [!NOTE]
>  Windows Phone の My Server アプリを利用し、サーバーにメディア ファイルをアップロードすることもできます。 [Windows Phone ストア](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)から My Server アプリをダウンロードできます。 Windows Phone の My Server アプリに関する詳細については、ブログの投稿を参照してください。 [Windows Server Essentials の My Server phone アプリ](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx)します。  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>サーバー上の共有フォルダーにデジタル メディア ファイルを追加するには  
  
1.  次の方法のいずれかを利用してサーバーにサインインします。  
  
    1.  リモート Web アクセスにログオンする方法については、「 [Log on to Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)」を参照してください。  
  
    2.  スタート パッドでサインイン方法の詳細については、次を参照してください。[スタート パッドの概要](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)します。  
  
2.  追加するメディアのフォルダーを検索し、クリックします。  
  
3.  追加するメディア ファイルをサーバーの共有フォルダーにコピーして貼り付けるか、ドラッグアンドドロップします。  
  
##  <a name="BKMK_6"></a> 許可またはサーバー上のメディア ライブラリへのアクセス制限  
  
-   メディア共有をオンにすると、次の 4 つの事前定義フォルダー作成されます。ミュージック、ピクチャ、ビデオ、録画されたテレビ これらのフォルダーがサーバーに既にあった場合、メディア共有用の共有フォルダーとしてその既存のフォルダーが再利用されます。 既存フォルダーのすべてのメディア コンテンツ、ユーザーのアクセス許可は保持されますが、およびネットワークのすべてのユーザーと共有されます。  
  
-   共有フォルダーのメディア ライブラリ共有をオンにする前に、メディア ライブラリ共有は共有フォルダーに設定したあらゆる種類のユーザー アカウント アクセスを回避することを知ってください。 たとえば、 **[フォト]** 共有フォルダーのメディア ライブラリ共有をオンにして、 **[フォト]** 共有フォルダーで「Bobby」という名前のユーザー アカウントに **[アクセスなし]** を設定します。 Bobby は **[ビデオ]** 共有フォルダーからサポートされるあらゆるデジタル メディア プレーヤーまたは DMR にデジタル メディアをストリーム配信できます。 このようなストリーム配信を望まないデジタル メディアがある場合、メディア ライブラリ共有がオンになっていないフォルダーにそのファイルを保存します。  
  
-   共有フォルダーのメディア ライブラリ共有にする場合は、あらゆるサポートされているデジタル メディア プレーヤーまたは DMR、Windows Server Essentials ネットワークにアクセスできることができますもデジタル メディアにアクセスその共有フォルダー。 たとえば、無線ネットワークが安全でない場合、無線ネットワークの範囲内にいれば、だれでもそのフォルダーのデジタル メディアにアクセスできる可能性があります。 メディア ライブラリ共有をオンにする前に、無線ネットワークの安全を確認してください。 詳細については、無線アクセス ポイントの文書を参照してください。  
  
##  <a name="BKMK_8"></a> メディア ライブラリ名の変更します。  
 メディア ライブラリの既定の名前は「**Digital Media Server**」です。 Windows Server Essentials でメディア ストリーム配信を有効にすると作成されます。 メディア ストリーム配信する方法の詳細詳細については、次を参照してください。[メディア ストリーム配信のオンまたはオフに](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.5)します。 サーバー ダッシュボードを利用すれば、メディア ライブラリ名をいつでも変更できます。  
  
#### <a name="to-rename-the-media-library"></a>メディア ライブラリの名前を変更するには  
  
1.  サーバー ダッシュボードを開きます。 スタート パッドからダッシュボードを開くには、 **[ダッシュボード]** をクリックし、サーバーのパスワードを入力し、矢印をクリックしてサインインします。  
  
2.  サーバーのダッシュボードで、 **[設定]** をクリックします。  
  
3.  **[設定]** ページで、 **[メディア]** タブをクリックします。  
  
4.  **[メディア設定]** ページの **[メディア ライブラリ]** セクションで、メディア ライブラリの名前をクリックします。  
  
5.  **[メディア ライブラリの名前を変更する]** ダイアログ ボックスで、メディア ライブラリの新しい名前を入力し、 **[OK]** をクリックします。  
  
##  <a name="BKMK_9"></a> デジタル メディアの共有を停止します。  
 サーバーの管理者は、Windows Server Essentials を実行しているサーバー上の共有フォルダーに格納されているデジタル メディアの共有を停止できます。  
  
#### <a name="to-stop-sharing-media-in-shared-folders"></a>共有フォルダーのメディアの共有を停止するには  
  
1.  サーバー ダッシュボードを開きます。  
  
2.  ダッシュボードの **[ホーム]** ページで、 **[セットアップ]** をクリックし、 **[メディア サーバーのセットアップ]** をクリックし、 **[クリックして、メディア サーバーをセットアップします]** をクリックします。  
  
3.  **[メディア]** 設定ページで、次のオプションの 1 つを選択できます。  
  
    -   **[オフにする]** をクリックし、サーバーに保存されているすべてのファイルの共有を停止します。  
  
    -   **[カスタマイズ]** をクリックし、共有を停止するフォルダーに対して **[いいえ]** を選択します。  
  
4.  **[適用]** または **[OK]** をクリックし、変更を保存します。  
  
##  <a name="BKMK_10"></a> サーバー上の共有ファイルにアクセスするサーバー メッセージ ブロック (SMB) プロトコルを使用するメディア デバイスを有効にします。  
 (メディア ストリーム配信の) DLNA の代わりに、ネットワークのファイルと共有のアクセスにサーバー メッセージ ブロック (SMB) を利用するデバイスでは、ゲスト アカウントを有効にする必要があります。 この設定により、ネットワーク上のすべてのデバイスまたはユーザーが認証なしで共有フォルダーの内容を表示できます。  
  
> [!CAUTION]
>  ゲスト アカウントを有効にすると、既定ではだれでもサーバー上の共有リソースにアクセスできます。  
  
##  <a name="BKMK_CommonProcessors"></a> 共通プロセッサとビデオのプロファイルをサポート  
 Windows Server Essentials サーバーからメディアをストリーム配信する、Windows 7 または Windows 8 オペレーティング システムまたはその他のネットワークに接続されたデバイス (デジタル メディア プレーヤーなど)、または Media Center エクステンダー (Xbox 360 など) を実行しているコンピューターを使用することができます。 ネットワークから離れた場所にいるとき、リモート Web アクセス メディア プレーヤーを利用し、サーバーに保存されているファイルを再生できます。  
  
 200 KBps ～ 10 MBps のデータ転送速度が必要です。 ご利用のコンピューターとデバイスが認識し、再生できるメディア形式を使用する必要があります。 すべてのデバイスで同じメディア形式をサポートしているわけではありません。所有しているメディア ファイルをご利用のコンピューターとデバイスで再生する方法はあるはずです。  
  
  Windows Server Essentials には、コンピューターまたはデバイスの機能を決定し、サポートされている 1 つに、サポートされていない動画ファイルを動的に変換するトランス コードのサポートが含まれています。 一般的に、Windows Media Player 12 が Windows 7 または Windows 8 を実行しているコンピューターでコンテンツを再生できる場合、サーバーにあるそのコンテンツはネットワークに接続されているデバイスで再生されます。  
  
 トランスコーディングに選択される形式とビットレートは、サーバーのプロセッサの性能に大幅に依存します。 プロセッサの性能は、Windows エクスペリエンス指標の一部として確認されます。 サーバーの性能スコアを判断するには、次のいずれかを行います。  
  
- Windows 7 またはサーバーと同じプロセッサを搭載した Windows 8 を実行しているネットワーク コンピューターに移動し、**コントロール パネルの [** 、] をクリックして**パフォーマンスの情報とツール**で情報を確認し、**速度、コンピューターのパフォーマンスを向上させる**ページ。  
  
- プロセッサのメーカーに問い合わせます。  
  
  最も快適にご利用いただくために、お使いのサーバーのプロセッサに適した動画ストリーム配信解像度をお選びください。 サーバーは自動的に次の設定の 1 つにビットレートを調整します。  
  
- **低** プロセッサ スコアが 3.6 未満の場合  
  
- **中** プロセッサ スコアが 3.6 超で 4.2 未満の場合  
  
- **高** プロセッサ スコアが 4.2 超で 6.0 未満の場合  
  
- **最高** プロセッサ スコアが 6.0 超の場合  
  
  ご利用のサーバーよりも大きい処理能力を必要とする動画ストリーム配信解像度を選択した場合、バッファーが発生し、サーバーからメディアをストリーム配信している最中に停止することがあります。  
  
> [!NOTE]
>  リモート Web アクセス経由で高解像度の動画をストリーム配信する場合、スコアが 6.0 以上のプロセッサが必要になります。  
  
##  <a name="BKMK_KnownIssues"></a> メディア ファイルの種類に関する既知の問題  
 リモート Web アクセスのメディア ストリーム配信機能は、Windows Media Player 12 ネットワーク共有サービスを利用します。 リモート Web アクセスのメディア ストリーム配信は Windows Media Player 12 と Silverlight 4 でサポートされるオーディオ、動画、ピクチャのファイル タイプをサポートします。  
  
 次の表は、リモート Web アクセスのメディア ストリーム配信でサポートされるファイル タイプ (形式) の一覧です。 この表にないメディア ファイル タイプがサーバーに置かれている場合、リモート Web アクセスのメディア ストリーム配信ではそのファイル タイプをストリーム配信できません。  
  
|ファイルの種類|ファイル名拡張子|  
|---------------|-------------------------|  
|3GPP ファイル|.3gp、.3gpp、.3g2、.3gp2|  
|Audio Data Transport Stream (ADTS) オーディオ ファイル|.adts と .adt|  
|AU オーディオ ファイル|.au と .snd|  
|Audio Interchange File Format (AIFF) オーディオ ファイル|.aif、.aifc、.aiff|  
|AVCHD ファイル|.m2ts、.m2t、.mts|  
|CD オーディオ ディスク|.cda|  
|DVD-Video ディスク|.vob|  
|JPEG ピクチャ ファイル|.jpg|  
|MP3 オーディオ ファイル|.mp3 と .m3u|  
|MPEG 動画ファイル|.mpeg、.mpg、.m1v、.mpa、.mpe、.mp4、.mp4v、.m4v、.m4a、.mov|  
|Windows のオーディオ ファイルと動画ファイル|.avi と .wav|  
|Windows Media のオーディオ ファイルと動画ファイル|.asf、.asx、.wax、.wm、.wma、.wmd、.wmp、.wmv、.wmx、.wpl、.wvx|  
  
> [!NOTE]
>  この表に記載されているファイル タイプを使用できない場合、そのファイルは Windows Media Player ではサポートされていないコーデックでコード化されている可能性があります。  
  
 サポートされるファイル形式の詳細については、「 [Windows Media Player でサポートされるファイルの種類](https://go.microsoft.com/fwlink/p/?LinkID=196118) 」、および Silverlight の場合は、「 [サポートされるメディア形式、プロトコル、ログ フィールド](https://go.microsoft.com/fwlink/p/?LinkId=203339) 」を参照してください。  
  
## <a name="see-also"></a>関連項目  
  
-   [デジタル メディアを再生します。](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
