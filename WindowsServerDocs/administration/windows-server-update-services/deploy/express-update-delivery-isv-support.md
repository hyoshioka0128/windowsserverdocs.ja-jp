---
title: 更新プログラムのエクスプレス配信 ISV のサポート
description: Windows Server Update Service (WSUS) のトピックで、どのように独立系ソフトウェア ベンダー (ISV) は、WSUS を使用して高速更新プログラムの配信を構成できます。
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
ms.openlocfilehash: b891f61ff2c930591c33805d0e3bc595ebf196f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850493"
---
#<a name="express-update-delivery-isv-support"></a>更新プログラムのエクスプレス配信 ISV のサポート

>適用先:Windows 10、Windows Server 2016

Windows 10 更新プログラムのダウンロードは、すべてのパッケージには、一貫性とわかりやすくするために確実にすべての以前にリリースされた修正プログラムが含まれているために、大規模なことができます。  

バージョン 7、Windows 以来と呼ばれる機能と Windows 更新プログラムのダウンロードのサイズを減らすことが[Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)、コンシューマー デバイスはサポートが既定では、Windows 10 enterprise デバイスが Windows Server 更新プログラムを必要とExpress を活用するために services (WSUS)。

## <a name="how-microsoft-supports-express"></a>マイクロソフトによるエクスプレスのサポート方法

- **スタンドアロンの WSUS を express します。**

    高速更新プログラムの配信が既に[WSUS のサポートされているすべてのバージョンで使用できる](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)します。

- **Express で Windows Update に直接接続されているデバイスは、** 

    コンシューマー デバイスは、Express のダウンロードをサポートします。 スキャン、ダウンロードおよび更新プログラムをインストールする Windows Update (WU) クライアントを使用します。 ダウンロード フェーズでは、WU クライアントは、Express パッケージを要求し、適切なバイト範囲をダウンロードします。

-   **[Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** を使って管理しているエンタープライズ デバイスでも、構成を変更せずに更新プログラムのエクスプレス配信を活用できます。

##<a name="how-isvs-can-take-advantage-of-express"></a>Isv が高速の活用を実行する方法

Isv は、高速更新プログラムの配信をサポートするために、WSUS と WU クライアントを使用できます。 Microsoft は、次の 3 つの手順をお勧めしますは、以下のセクションで詳しく説明します。

1.  [**WSUS を構成します。**](#BKMK_1)

    WSUS サーバーが必要ですスキャンと更新プログラムの同期 (追加の情報は[ここ](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx))。

2.  [**指定し、ISV のファイル キャッシュの設定**](#BKMK_2)

    更新のキャビネット ファイル (.cab ファイル) を含む更新プログラム コンテンツをホストする ISV のファイル キャッシュをお勧めし、Express パッケージ (.psf ファイル)。

3.  [**WU クライアントの操作を ISV クライアント エージェントを設定します。**](#BKMK_3)

>[!NOTE]
>Windows 10 バージョン 1607 の累積的な更新プログラムのリリースで (または後) が必要です 2017 年 1 月 ([KB3213986 (OS ビルド 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693)をインストールします。
    
   - ISV のクライアント エージェントは、更新プログラムを承認するときにダウンロードしてインストールする更新プログラムを決定します。
   - WU クライアントをダウンロードするバイト範囲を決定し、ダウンロードの要求を開始します。

### <a name="BKMK_1"></a>手順 1:WSUS を構成します。

WSUS では、Windows Update にインターフェイスとして機能し、Express パッケージをダウンロードする必要があるを記述するすべてのメタデータを管理します。 展開する必要がある場合は、次を参照してください。 [**概要の Windows Server Update Services 3.0 SP2**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)します。 WSUS を展開した後、更新プログラムのコンテンツのローカル WSUS サーバーに保存するかどうかは、主要な考慮事項です。 WSUS を構成する場合は、更新プログラムをローカルに保存されないをお勧めします。 これにより、環境内でこれらのパッケージの展開を指示するソフトウェアが既にあることを前提としています。 WSUS のローカル ストレージを構成する方法については、次を参照してください。 [**更新プログラムの格納場所を決定する**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)します。

### <a name="BKMK_2"></a>手順 2:指定し、ISV ファイル キャッシュの設定 

####<a name="specify-the-isv-file-cache"></a>ISV ファイル キャッシュを指定します。

記載された新しいクライアント側グループ ポリシーとモバイル デバイス管理 (MDM) の設定、 [**構成サービス プロバイダー リファレンス**](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) ISV ファイル キャッシュの場所を定義します。

| **名前**                                              | **説明**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 更新プログラムを代替ダウンロード場所を構成します。 | Microsoft Update から更新をホストする別のイントラネットのサーバーを指定します。 ネットワーク上のコンピューターを自動的に更新し、この更新サービスを使用できます。 |

ISV ファイル キャッシュの代替ダウンロード場所を設定するときに、2 つのオプションがあります。

1. **ISV HTTP サーバーのホスト名を指定**、これは、ISV ファイルのキャッシュ
    
    このアプローチは、ポリシーで指定された HTTP サーバーに要求をダウンロードする WU クライアントを構成します。

2. **Localhost を指定します。**
 
    このアプローチは、localhost に要求をダウンロードする WU クライアントを構成します。 これにより、これらの要求と、ダウンロードの要求を満たすために適切なルートを処理するために、ISV クライアント エージェントです。

>[!IMPORTANT]
>ISV ファイル キャッシュには、次の必要があります。                                                          
                                                                                                                                   >- サーバーには、HTTP 1.1、rfc に準拠している必要があります。 <http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
                                                                                                                                   >具体的には、web サーバーは、サポートする必要があります。                                                                                                                                                                                                                                      [**ヘッド**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)と[**取得**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm)要求<br>                                                                                                                                                                                                                                                                                                  部分範囲の要求<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   -キープ アライブ<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -使用しない"Transfer-encoding: チャンクですか?                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV ファイル キャッシュを設定します。

管理対象クライアントにインストールする更新プログラムに関連付けられているファイルでは、ISV ファイル キャッシュを設定する必要があります。 

**ISV ファイル キャッシュを設定するには。**

1. 使用[WSUS Api](https://msdn.microsoft.com/en-us/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx)更新プログラムのファイルのパスとファイル名を MU サービスにアクセスします。

    WSUS サーバーで各更新プログラムのメタデータを含む、更新プログラムのファイルのパスとファイル名、Microsoft Update で次のように (Microsoft Update のホスト名で太字、その後にファイルのパスとファイル名): **http://download.windowsupdate.com** /c msdownload/更新/software/updt/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74.msu

2. Microsoft Update からファイルをダウンロードし、これら 2 つのメソッドのいずれかを使用して、ISV ファイル キャッシュに格納します。 

 - ストアのファイルを使用して、 **MU サービスと同じフォルダー パス**

 - ストアのファイルを使用して、 **ISV 定義フォルダーのパス**

    HTTP サーバー (または localhost) リダイレクトがある**HTTP GET**要求で、MU フォルダー パスとファイル名、ISV ファイルの場所を参照します。

### <a name="BKMK_3"></a>手順 3:WU クライアントの操作を ISV クライアント エージェントを設定します。

ISV のクライアント エージェントは、ダウンロードと、次の推奨されるワークフローを使用して承認済み更新プログラムのインストールは調整します。

1.  ISV のクライアント エージェントをスキャンして WSUS サーバーに、WU クライアントを呼び出し

2.  スキャンは、WU クライアントに適用できる更新プログラムのセットを返します

3.  ISV クライアントが承認をダウンロードしてインストールする更新プログラムを決定します

4.  ISV クライアント エージェントの呼び出し WU クライアントは、承認済み更新プログラムをダウンロードするには

5.  ISV のクライアント エージェントが承認済み更新プログラムをインストールする WU クライアントを呼び出す、更新プログラムがダウンロードされたら、

参照してください[検索、ダウンロード、および更新プログラムのインストール](https://msdn.microsoft.com/en-us/library/windows/desktop/aa387102(v=vs.85).aspx)WU クライアントを使用してスキャンする方法の詳細については、ダウンロードして更新プログラムをインストールします。

### <a name="download-workflow-options"></a>ワークフロー オプションをダウンロードします。

次は、ISV のファイル キャッシュからのダウンロードのワークフロー オプションの 2 つの図に示します。

![ワークフロー 1](../../media/express-update-delivery-isv-support/image1.png)

![ワークフロー 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>エクスプレス ダウンロードのしくみ

- エクスプレスをサポートする OS 更新プログラムでは、以下の 2 つのバージョンのファイル ペイロードがサービスに保存されます。

 - **完全なファイル バージョン**--本質的に更新プログラム バイナリのローカル バージョンを置き換える

 - **Express バージョン**-デバイス上の既存のバイナリのパッチを適用するために必要な差分を格納しています。 

   完全なファイル バージョンと、Express バージョンの両方が、スキャン フェーズの一環としてクライアントにダウンロードされた更新プログラムのメタデータで参照されます。 

   **Express のダウンロードはように動作します。**

   WU クライアントは、(たとえば、バイト範囲要求をサポートしていないプロキシを通過する) 場合に必要な場合は完全なファイルに最初に、および特定の状況 fall、Express をダウンロードしようとしました。

  1. WU クライアントは、Express のダウンロードを開始したときに**WU クライアントは、スタブをまずダウンロード**、Express パッケージの一部です。

  2. **WU クライアントは、Windows インストーラーをこのスタブを渡します**で提供されるファイルの最新バージョンを取得するために必要なデバイス上のファイルの差分を比較する、ローカルのインベントリを実行する、スタブを使用します。

  3. **Windows インストーラーは、WU クライアントは、範囲をダウンロードし、要求**これが必要になる決定されています。

  4. **WU クライアントは、これらの範囲をダウンロードし、Windows インストーラーに渡して**、適用範囲とし、追加の範囲が必要なかどうかを決定します。 これは、Windows インストーラーは、すべての必要な範囲がダウンロードされていることを WU クライアントに通知するまで繰り返されます。

  この時点で、ダウンロードが完了し、更新プログラムのインストール準備が整います。

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>配信の最適化が帯域幅の消費を削減する方法

配信の最適化 (DO) は、オペレーティング システムの更新プログラム、オペレーティング システムのアップグレード、およびアプリケーションの帯域幅の消費量を減らす必要がある企業の自己編成の分散キャッシュ ソリューションです。 選択すると、クライアントが指定のダウンロード場所 (このシナリオでは ISV ファイル キャッシュ) と組み合わせて、代替ソース (ネットワーク上の他のピア) などからそれらの要素をダウンロードするが、できます。

既定では、Windows 10 Enterprise および教育機関向けでのみ、組織のネットワーク上のピア ツー ピア共有により、操作を行いますが、異なる方法でグループ ポリシーとモバイル デバイス管理 (MDM) の設定を使用して構成することができます。

参照してください[Windows 10 用の配信の最適化の構成を更新](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization)詳細については、操作を行います。
