---
title: WSUS を使用しない月次デルタ更新 ISV サポート
description: Windows Server Update Service (WSUS) のトピック-独立系ソフトウェアベンダー (ISV) が WSUS Express 更新プログラム配信ではなく毎月デルタ更新プログラムを一時的に使用してパッケージサイズを小さくする方法
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 9077cb87d1d0f6d59ad037c93f5608d3b698feaa
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868715"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>WSUS を使用しない月次デルタ更新 ISV サポート

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

すべてのパッケージには、一貫性と簡潔さを確保するために以前にリリースされたすべての修正が含まれているので、Windows 10 更新プログラムのダウンロードは大きくなる  

バージョン7以降、Windows では、 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)という機能を使用して Windows Update ダウンロードのサイズを縮小できるようになりましたが、コンシューマーデバイスでは既定でサポートされていますが、windows 10 enterprise デバイスでは WINDOWS SERVER UPDATE SERVICES (WSUS) が必要です。Express の利点。 WSUS を使用できる場合は、「 [Express update DELIVERY ISV サポート](express-update-delivery-ISV-support.md)」を参照してください。 高速更新配信を有効にするには、これを使用することをお勧めします。 

現在 WSUS がインストールされていないが、中間の更新パッケージのサイズが小さい場合は、毎月の差分更新を使用できます。 差分更新では、パッケージのサイズが大幅に削減されますが、WSUS Express 更新プログラムの配信ほど多くはありません。 パッケージのサイズを最大限に減らすには、可能な限り WSUS Express の更新プログラムを展開することをお勧めします。 次に示すのは、Windows 10 バージョン1607のデルタ、累積、高速のダウンロードサイズを比較したグラフです。

![ダウンロードサイズの比較](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>毎月の差分更新とは

毎月のセキュリティ更新プログラムには、次の2つのバリエーションがあります。デルタと累積。

毎月の差分更新は新しいものであり、更新パッケージのサイズを減らすために WSUS を使用できない Isv 向けの暫定的なソリューションです。

>[!IMPORTANT]
>**差分更新は、Windows 10 バージョン 1607 (記念日更新)、バージョン 1703 (作成者の更新)、バージョン 1709 (作成者の更新プログラム) のサービスで利用できます。** バージョン1709以降のリリースでは、増分更新を引き続き利用するために、[高速更新配信](express-update-delivery-ISV-support.md)をサポートする展開インフラストラクチャを実装する必要があります。

毎月の差分更新を使用すると、パッケージには1か月の更新プログラムのみが含まれます。 月単位の累積には、その更新プログラムのリリースまでのすべての更新プログラムが含まれており、その結果、毎月拡張されるファイルが大きくなります。 差分更新と月次更新は、毎月第2火曜日にリリースされます。これは、"火曜日の更新" とも呼ばれます。 次の表は、差分更新と累積更新を比較したものです。

|                    | 毎月の**差分**更新                                                                                                                                                                                                       | 月単位の**累積的**な更新プログラム                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scope**          | **その月の新しい修正のみ**を含む単一の更新                                                                                                                                                                           | その月と過去のすべての月のすべての新しい修正を含む単一の更新                                                                                                                                                   |
| **アプリケーション**    | 前の月の更新が適用された場合にのみ適用できます (累積または差分)                                                                                                                                           | いつでも適用できます。                                                                                                                                                                                                |
| **伝達**       | 他のツールやプロセスで使用するためにダウンロードできる**Windows Update カタログにのみパブリッシュ**されます。 に接続されている Pc には提供されません Windows Update                                                         | Windows Update (すべてのコンシューマー Pc でインストール)、WSUS、Windows Update カタログに発行されます。                                                                                                                |

差分と累積は同じ数の KB 番号を持ち、同じ分類とリリースが同時に存在します。 更新プログラムは、カタログ内の更新プログラムのタイトルまたは msu の名前のいずれかで区別できます。

-  2017-02 *\*\*x64 ベースシステム*用の Windows 10 バージョン1607のデルタ更新プログラム (KB1234567)
-  2017-02 *\*\*x86 ベースシステム用の Windows 10 バージョン1607の**累積的な更新プログラム*** (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>毎月の差分更新を使用する場合

クライアントデバイスの更新プログラムのサイズに問題がある場合は、前月の更新プログラムがインストールされているデバイスでデルタ更新プログラムを使用し、遅延しているデバイスで累積更新プログラムを使用することをお勧めします。 このようにして、すべてのデバイスが最新の状態になるために必要なのは1つの更新だけです。 これには、組織内のデバイスの最新の状態に基づいてさまざまな更新プログラムを展開する必要があるため、更新プログラム全体の管理プロセスでは小さな調整が必要です。

![ダウンロードサイズの比較](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>差分更新と累積更新プログラムが同じ月に展開されないようにする

差分更新と累積更新プログラムは同時に利用できるため、両方の更新プログラムを同じ月に展開した場合の動作を理解することが重要です。

同じバージョンのデルタと累積更新プログラムを承認して展開した場合、追加のネットワークトラフィックが生成されるのは、両方が PC にダウンロードされても、再起動後にコンピューターを Windows で再起動できない場合があるためです。

差分更新と累積更新プログラムの両方が誤ってインストールされ、コンピューターが起動しなくなった場合は、次の手順で回復できます。

1. WinRE コマンドプロンプトでブートする
2. 保留中の状態のパッケージを一覧表示します。

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **例**:` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. パイプを使用して**パッケージ**化したテキストファイルを開きます。 インストール保留中の修正プログラムがある場合は、パッケージ名ごとに**削除パッケージ**を実行します。
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **例**:`x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >アンインストール保留中の修正プログラムを削除しないでください。

>[!IMPORTANT]
>**差分更新は、Windows 10 バージョン 1607 (記念日更新)、バージョン 1703 (作成者の更新)、バージョン 1709 (作成者の更新プログラム) のサービスで利用できます。** バージョン1709以降のリリースでは、増分更新を引き続き利用するために、[高速更新配信](express-update-delivery-ISV-support.md)をサポートする展開インフラストラクチャを実装する必要があります。
