---
title: 更新プログラムのエクスプレス配信 ISV のサポート
description: Windows Server Update Service (WSUS) トピック-独立系ソフトウェアベンダー (ISV) が WSUS を使用して高速更新配信を構成する方法
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 0f5893d47219e9263ed7f35bee472848a47c6164
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868737"
---
# <a name="express-update-delivery-isv-support"></a>更新プログラムのエクスプレス配信 ISV のサポート

>適用先:Windows 10、Windows Server 2016

すべてのパッケージには、一貫性と簡潔さを確保するために以前にリリースされたすべての修正が含まれているので、Windows 10 更新プログラムのダウンロードは大きくなる  

バージョン7以降、Windows では、 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)という機能を使用して Windows Update ダウンロードのサイズを縮小できるようになりましたが、コンシューマーデバイスでは既定でサポートされていますが、windows 10 enterprise デバイスでは WINDOWS SERVER UPDATE SERVICES (WSUS) が必要です。Express の利点。

## <a name="how-microsoft-supports-express"></a>マイクロソフトによるエクスプレスのサポート方法

- **WSUS スタンドアロンでの Express**

    高速更新配信は、[サポートされているすべてのバージョンの WSUS で既に使用可能](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)です。

- **Windows Update に直接接続されているデバイスでの Express** 

    コンシューマーデバイスは高速ダウンロードをサポートします。これらのデバイスは、Windows Update (WU) クライアントを使用して、更新プログラムのスキャン、ダウンロード、およびインストールを行います。 ダウンロードフェーズでは、WU クライアントが高速パッケージを要求し、適切なバイト範囲をダウンロードします。

-  **[Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** を使って管理しているエンタープライズ デバイスでも、構成を変更せずに更新プログラムのエクスプレス配信を活用できます。

## <a name="how-isvs-can-take-advantage-of-express"></a>Isv が Express を活用する方法

Isv は、WSUS と WU クライアントを使用して、高速更新配信をサポートできます。 Microsoft では次の3つの手順を推奨しています。各手順については、以下のセクションで詳しく説明します。

1.  [**WSUS の構成**](#BKMK_1)

    スキャン & 更新の同期には WSUS サーバーが必要です (詳細についてはこちらを参照して[ください](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx))。

2.  [**ISV ファイルキャッシュを指定して設定する**](#BKMK_2)

    更新プログラムのキャビネットファイル (.cab ファイル) と高速パッケージ (psf ファイル) を含む更新プログラムのコンテンツをホストするには、ISV ファイルキャッシュを使用することをお勧めします。

3.  [**WU クライアント操作を送信するように ISV クライアントエージェントを設定する**](#BKMK_3)

>[!NOTE]
>(またはそれ以降) 1 月 2017 ([KB3213986 (OS ビルド 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693)をインストールするには、Windows 10 バージョン1607リリースの累積的な更新プログラムが必要です。
    
   - ISV クライアントエージェントは、承認する更新プログラムと、更新プログラムをダウンロードしてインストールするタイミングを決定します。
   - WU クライアントによって、ダウンロード要求をダウンロードして開始するバイト範囲が決定されます。

### <a name="BKMK_1"></a>手順 1:WSUS の構成

WSUS は、ダウンロードする必要がある高速パッケージを記述するすべてのメタデータを Windows Update および管理するためのインターフェイスとして機能します。 を展開する必要がある場合は[**Windows Server Update Services 3.0 SP2 の概要**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)」を参照してください。 WSUS が展開されたら、更新プログラムのコンテンツを WSUS サーバーにローカルに格納するかどうかが主に考慮されます。 WSUS を構成する場合は、更新プログラムをローカルに保存しないことをお勧めします。 ここでは、これらのパッケージを展開するソフトウェアが環境内に既に存在することを前提としています。 WSUS ローカルストレージを構成する方法の詳細については、「[**更新プログラムの保存場所を決定**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)する」を参照してください。

### <a name="BKMK_2"></a>手順 2:ISV ファイルキャッシュを指定して設定する 

#### <a name="specify-the-isv-file-cache"></a>ISV ファイルキャッシュの指定

[**構成サービスプロバイダーのリファレンス**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)で詳細に説明されている新しいクライアント側のグループポリシーとモバイルデバイス管理 (MDM) の設定では、ISV ファイルキャッシュの場所を定義します。

| **Name**                                              | **[説明]**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 更新プログラムの代替のダウンロード場所を構成します。 | Microsoft Update から更新プログラムをホストする代替イントラネットサーバーを指定します。 この更新サービスを使用して、ネットワーク上のコンピューターを自動的に更新することができます。 |

ISV ファイルキャッシュ用に別のダウンロード場所を設定する場合、次の2つのオプションがあります。

1. Isv **HTTP サーバーのホスト名を指定し**ます。これは isv ファイルキャッシュです。
    
    この方法では、ポリシーで指定された HTTP サーバーにダウンロード要求を行うように WU クライアントを構成します。

2. **Localhost を指定する**
 
    この方法では、localhost にダウンロード要求を行うように WU クライアントを構成します。 これにより、ISV クライアントエージェントは、これらの要求を処理し、必要に応じて、ダウンロード要求を満たすようにルーティングできます。

> [!IMPORTANT]
> ISV ファイルキャッシュには、次のものが必要です。                                                          
> - サーバーは RFC に準拠した HTTP 1.1 である必要があります。<http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> 具体的には、web サーバーは                                                                                                                                                                                                                                      [**HEAD**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)要求と[**GET**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm)要求<br>                                                                                                                                                                                                                                                                                                  -部分的な範囲の要求<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   -キープアライブ<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -"転送エンコード: チャンク処理" を使用しないでください。                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV ファイルキャッシュの設定

ISV ファイルキャッシュには、管理されたクライアントにインストールされる更新プログラムに関連付けられたファイルが設定されている必要があります。 

**ISV ファイルキャッシュを設定するには:**

1. [WSUS api](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx)を使用して、MU サービスの更新プログラムのファイルパスとファイル名にアクセスします。

    WSUS サーバー上の各更新プログラムのメタデータには、次のように Microsoft Update 上の更新プログラムのファイルパスとファイル名が含まれます (Microsoft Update の **<http://download.windowsupdate.com>** ホスト名は太字で、その後にファイルのパスとファイル名を指定します):/c/msdownload/update/software/updt/2016/09/windows 10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74

2. 次の2つの方法のいずれかを使用して、Microsoft Update からファイルをダウンロードし、ISV ファイルキャッシュに保存します。 

   - **MU サービスと同じフォルダーパス**を使用してファイルを保存する

   - **ISV が定義したフォルダーパス**を使用してファイルを格納する

     HTTP GET 要求 (MU フォルダーパスとファイル名を参照する**http GET**要求) を ISV ファイルの場所にリダイレクトします。

### <a name="BKMK_3"></a>手順 3:WU クライアント操作を送信するように ISV クライアントエージェントを設定する

ISV クライアントエージェントは、次の推奨されるワークフローを使用して、承認された更新プログラムのダウンロードとインストールを調整します。

1.  ISV クライアントエージェントは、WSUS サーバーに対してスキャンを実行するために WU クライアントを呼び出します。

2.  スキャンによって、適用可能な更新プログラムのセットが WU クライアントに返されます。

3.  ISV クライアントは、承認、ダウンロード、およびインストールする更新プログラムを決定します。

4.  ISV クライアントエージェントは、承認された更新プログラムをダウンロードするために WU クライアントを呼び出します。

5.  更新プログラムがダウンロードされると、ISV クライアントエージェントは、承認された更新プログラムをインストールするために WU クライアントを呼び出します。

WU クライアントを使用した更新プログラムのスキャン、ダウンロード、およびインストールに関する追加情報については、「[更新プログラムの検索、ダウンロード、およびインストール](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx)」を参照してください。

### <a name="download-workflow-options"></a>ワークフローオプションのダウンロード

ISV ファイルキャッシュからのワークフローオプションのダウンロードには、次の2つの図があります。

![ワークフロー1](../../media/express-update-delivery-isv-support/image1.png)

![ワークフロー2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>エクスプレス ダウンロードのしくみ

- エクスプレスをサポートする OS 更新プログラムでは、以下の 2 つのバージョンのファイル ペイロードがサービスに保存されます。

  - **ファイルの完全バージョン**--基本的に、更新バイナリのローカルバージョンを置き換えます。

  - **Express バージョン**--デバイス上の既存のバイナリにパッチを適用するために必要なデルタが含まれています。 

    フルファイルバージョンと Express バージョンの両方が更新プログラムのメタデータで参照されており、スキャンフェーズの一部としてクライアントにダウンロードされています。 

    **高速ダウンロードは次のように機能します。**

    WU クライアントは、Express を最初にダウンロードしようとします。特定の状況下では、必要に応じて (たとえば、バイト範囲の要求をサポートしていないプロキシを経由する場合など)、ファイル全体にフォールバックします。

  1. WU クライアントが高速ダウンロードを開始すると、 **wu クライアントは最初**に、express パッケージの一部であるスタブをダウンロードします。

  2. **WU クライアントは、このスタブを Windows インストーラーに渡します。このスタブ**は、スタブを使用してローカルインベントリを実行し、デバイス上のファイルの差分を、提供されている最新バージョンのファイルに取得するために必要なものと比較します。

  3. 次に、Windows インストーラーは、必要と判断された**範囲をダウンロードするように WU クライアントに要求**します。

  4. **WU クライアントは、これらの範囲をダウンロードし、それらを Windows インストーラーに渡し**ます。これにより、範囲が適用され、追加の範囲が必要かどうかが決まります。 これは、Windows インストーラーによって、必要なすべての範囲がダウンロードされたことが WU クライアントに通知されるまで繰り返されます。

  この時点で、ダウンロードが完了し、更新プログラムのインストール準備が整います。

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>配信の最適化による帯域幅の消費の削減

配信の最適化 (DO) は、オペレーティングシステムの更新、オペレーティングシステムのアップグレード、およびアプリケーションの帯域幅の消費量を削減することを検討している企業向けの、自己編成型の分散キャッシュソリューションです。 クライアントは、指定されたダウンロード場所 (このシナリオでは ISV ファイルキャッシュ) と共に代替ソース (ネットワーク上の他のピアなど) からこれらの要素をダウンロードできます。

Windows 10 Enterprise および教育では、既定で、組織のネットワークでのみピアツーピア共有を行うことができますが、グループポリシーとモバイルデバイス管理 (MDM) 設定を使用して異なる方法で構成できます。

詳細については、「 [Windows 10 更新プログラムの配信の最適化を構成](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization)する」を参照してください。
