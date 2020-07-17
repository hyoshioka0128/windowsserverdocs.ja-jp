---
title: 更新プログラムのエクスプレス配信 ISV のサポート
description: Windows Server Update Service (WSUS) のトピック -独立系ソフトウェア ベンダー (ISV) が WSUS を使用して更新プログラムのエクスプレス配信を構成する方法
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 60d01ef425ed96160cd76afdd7c27c081c778add
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80828775"
---
# <a name="express-update-delivery-isv-support"></a>更新プログラムのエクスプレス配信 ISV のサポート

>適用先:Windows 10、Windows Server 2016

Windows 10 更新プログラムでは、すべてのパッケージにそれまでのすべての修正が含まれています。これは一貫性を保ち、更新を簡素化するためですが、それによってダウンロードのサイズが大きくなることがあります。  

Windows では、バージョン 7 以降、[エクスプレス](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)と呼ばれる機能を使用して Windows Update ダウンロードのサイズを縮小できるようになりました。コンシューマー デバイスでは既定でサポートされていますが、Windows 10 エンタープライズ デバイスでエクスプレスを利用するには、Windows Server Update Services (WSUS) が必要です。

## <a name="how-microsoft-supports-express"></a>Microsoft によるエクスプレスのサポート方法

- **WSUS スタンドアロンでのエクスプレス**

    更新プログラムのエクスプレス配信は、既に [WSUS のサポートされているすべてのバージョン](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)で使用できます。

- **Windows Update に直接接続されているデバイスでのエクスプレス** 

    コンシューマー デバイスはエクスプレス ダウンロードをサポートしています。これらのデバイスは、Windows Update (WU) クライアントを使用して、更新プログラムのスキャン、ダウンロード、およびインストールを行います。 ダウンロード フェーズ中に、WU クライアントがエクスプレス パッケージを要求し、適切なバイト範囲をダウンロードします。

-  **[Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** を使って管理しているエンタープライズ デバイスでも、構成を変更せずに更新プログラムのエクスプレス配信を活用できます。

## <a name="how-isvs-can-take-advantage-of-express"></a>ISV がエクスプレスを活用する方法

ISV は、WSUS と WU クライアントを使用して、更新プログラムのエクスプレス配信をサポートできます。 Microsoft では次の 3 つの手順を推奨しています。以下のセクションで、各手順について詳しく説明します。

1.  [**WSUS を構成する**](#BKMK_1)

    スキャンと更新の同期を行うには WSUS サーバーが必要です (詳細については、[こちら](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx)を参照してください)

2.  [**ISV ファイル キャッシュを指定して設定する**](#BKMK_2)

    更新プログラムのコンテンツをホストするには、ISV ファイル キャッシュを使用することをお勧めします。これには、更新プログラムのキャビネット ファイル (.cab ファイル) とエクスプレス パッケージ (.psf ファイル) が含まれています。

3.  [**WU クライアント操作を送信するように ISV クライアント エージェントを設定する**](#BKMK_3)

>[!NOTE]
>2017 年 1 月 (またはそれ以降) の Windows 10 バージョン 1607 リリースの累積的な更新プログラム ([KB3213986 (OS ビルド 14393.693)](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693) をインストールする必要があります。
    
   - ISV クライアント エージェントは、承認する更新プログラムと、更新プログラムをダウンロードしてインストールするタイミングを決定します
   - WU クライアントは、ダウンロードするバイト範囲を決定し、ダウンロード要求を開始します

### <a name="step-1-configure-wsus"></a><a name=BKMK_1></a>手順 1: WSUS を構成する

WSUS は、Windows Update へのインターフェイスとして機能し、ダウンロードする必要があるエクスプレス パッケージを記述するすべてのメタデータを管理します。 展開する必要がある場合は、[**Windows Server Update Services 3.0 SP2 の概要**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)に関するページを参照してください。 WSUS が展開された後の主な考慮事項は、更新プログラムのコンテンツを WSUS サーバーにローカルに保存するかどうかです。 WSUS を構成する場合は、更新プログラムをローカルに保存しないことをお勧めします。 ここでは、これらのパッケージを展開するソフトウェアが環境内に既に存在することを前提としています。 WSUS ローカル ストレージを構成する方法の詳細については、[**更新プログラムの保存場所の決定**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)に関するページを参照してください。

### <a name="step-2-specify-and-populate-the-isv-file-cache"></a><a name=BKMK_2></a>手順 2: ISV ファイル キャッシュを指定して設定する 

#### <a name="specify-the-isv-file-cache"></a>ISV ファイル キャッシュを指定する

「[**構成サービス プロバイダーのリファレンス**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)」で詳細に説明されている新しいクライアント側のグループ ポリシーとモバイル デバイス管理 (MDM) の設定は、ISV ファイル キャッシュの場所を定義します。

| **名前**                                              | **説明**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 更新プログラムの別のダウンロード場所を構成します。 | Microsoft Update からの更新プログラムをホストする代替のイントラネット サーバーを指定します。 この更新サービスを使用して、ネットワーク上のコンピューターを自動的に更新できます |

ISV ファイル キャッシュの別のダウンロード場所を設定する場合は、次の 2 つのオプションがあります。

1. **ISV の HTTP サーバーのホスト名を指定する**。これが ISV ファイル キャッシュです
    
    この方法では、ポリシーで指定された HTTP サーバーにダウンロード要求を行うように WU クライアントを構成します

2. **localhost を指定する**
 
    この方法では、localhost にダウンロード要求を行うように WU クライアントを構成します。 これにより、ISV クライアント エージェントがこれらの要求を処理し、必要に応じて、ダウンロード要求を満たすようにルーティングできます。

> [!IMPORTANT]
> ISV ファイル キャッシュには次のことが必要です。                                                          
> - サーバーは RFC (<http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                              ) に基づき HTTP 1.1 準拠である必要があります  
> 具体的には、Web サーバーが [**HEAD**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 要求と [**GET**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) 要求をサポートする必要があります<br>                                                                                                                                                                                                                                                                                                  - 部分的な範囲の要求<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   - Keep-Alive<br>                                                                                                                                                                                                                                                                                                                                                                                                                            - Transfer-Encoding:chunked を使用しないでください                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV ファイル キャッシュを設定する

ISV ファイル キャッシュには、管理対象のクライアントにインストールされる更新プログラムに関連付けられたファイルが設定されている必要があります。 

**ISV ファイル キャッシュを設定するには、次の手順に従います。**

1. [WSUS API](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx) を使用して、MU サービスの更新プログラムのファイル パスとファイル名にアクセスします。

    WSUS サーバー上の各更新プログラムのメタデータには、次のように、Microsoft Update 上の更新プログラムのファイル パスとファイル名が含まれます (Microsoft Update のホスト名は太字で、その後にファイル パスとファイル名が続きます): **<http://download.windowsupdate.com>** /c/msdownload/update/software/updt/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74 .msu

2. Microsoft Update からファイルをダウンロードし、次の 2 つの方法のいずれかを使用して ISV ファイル キャッシュに保存します。 

   - **MU サービスと同じフォルダー パス**を使用してファイルを保存する

   - **ISV が定義したフォルダー パス**を使用してファイルを保存する

     HTTP サーバー (または localhost) から、MU フォルダー パスとファイル名を参照する **HTTP GET** 要求を ISV ファイルの場所にリダイレクトします。

### <a name="step-3-set-up-an-isv-client-agent-to-direct-wu-client-operations"></a><a name=BKMK_3></a>手順 3: WU クライアント操作を送信するように ISV クライアント エージェントを設定する

ISV クライアント エージェントは、次の推奨されるワークフローを使用して、承認された更新プログラムのダウンロードとインストールを調整します。

1.  ISV クライアント エージェントで、WSUS サーバーに対してスキャンを実行するために WU クライアントを呼び出します

2.  スキャンによって、適用可能な更新プログラムのセットが WU クライアントに返されます

3.  ISV クライアントで、承認、ダウンロード、およびインストールを行う更新プログラムを決定します

4.  ISV クライアント エージェントで、承認された更新プログラムをダウンロードするために WU クライアントを呼び出します

5.  更新プログラムがダウンロードされると、ISV クライアント エージェントが、承認された更新プログラムをインストールするために WU クライアントを呼び出します

WU クライアントを使用した更新プログラムのスキャン、ダウンロード、およびインストールの詳細については、[更新プログラムの検索、ダウンロード、およびインストール](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx)に関するページを参照してください。

### <a name="download-workflow-options"></a>ダウンロード ワークフローのオプション

次に、ISV ファイル キャッシュからのダウンロード ワークフローのオプションの 2 つの図を示します。

![ワークフロー 1](../../media/express-update-delivery-isv-support/image1.png)

![ワークフロー 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>エクスプレス ダウンロードのしくみ

- エクスプレスをサポートする OS 更新プログラムでは、以下の 2 つのバージョンのファイル ペイロードがサービスに保存されます。

  - **フルファイル版** - 基本的には、更新プログラム バイナリのローカル バージョンを置き換えます

  - **エクスプレス版** - デバイス上の既存のバイナリにパッチを適用するために必要なデルタが含まれています。 

    フルファイル版とエクスプレス版はどちらも、更新プログラムのメタデータ (スキャン段階でクライアントにダウンロードされる) で参照されます。 

    **エクスプレス ダウンロードは、次のように動作します。**

    WU クライアントはまずエクスプレス版のダウンロードを試み、状況に応じて必要であればフルファイル版にフォール バックします (バイト範囲の要求をサポートしていないプロキシを通過する場合など)。

  1. WU クライアントによるエクスプレス ダウンロードの開始時に、**WU クライアントはまずエクスプレス パッケージに含まれているスタブをダウンロード**します。

  2. **WU クライアントは、このスタブを Windows インストーラーに渡します。** Windows インストーラーは渡されたスタブを使ってローカル インベントリを行い、デバイス上のファイルのデルタを、提供されているファイルの最新バージョンを得るために必要なデルタと比較します。

  3. **Windows インストーラーは次に、必要と判断された範囲をダウンロードするように WU クライアントに要求します。**

  4. **WU クライアントは要求された範囲をダウンロードして、Windows インストーラーに渡します。** Windows インストーラーは渡された範囲を適用した後、その他に必要な範囲があるかを判断します。 この手順は、Windows インストーラーが WU クライアントに対して、必要なすべての範囲がダウンロードされたことを通知するまで繰り返されます。

  この時点で、ダウンロードが完了し、更新プログラムのインストール準備が整います。

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>配信の最適化による帯域幅の消費の削減

配信の最適化 (DO) は、オペレーティング システムの更新プログラム、オペレーティング システムのアップグレード、アプリケーションによる帯域幅の消費の削減を目指している企業向けの自己組織化された分散キャッシュ ソリューションです。 DO によって、クライアントは、指定されたダウンロードの場所 (このシナリオでは ISV ファイルキャッシュ) と組み合わせて、これらの要素を代替ソース (ネットワーク上の他のピアなど) からダウンロードできます。

Windows 10 Enterprise および Education の既定では、DO によって、組織独自のネットワークでのみピア ツー ピアの共有が許可されますが、グループ ポリシーやモバイル デバイス管理 (MDM) の設定を使用して異なる構成にすることができます。

DO の詳細については、「[Windows 10 更新プログラムの配信の最適化を構成](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization)」を参照してください。
