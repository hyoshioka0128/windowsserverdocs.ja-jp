---
title: 月単位のデルタ WSUS せず ISV のサポートを更新します。
description: Windows Server Update Service (WSUS) のトピックで、どのように独立系ソフトウェア ベンダー (ISV) はパッケージのサイズを小さく Express の WSUS 更新プログラムの配信ではなく月単位のデルタの更新プログラムを一時的に使用できます。
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
ms.openlocfilehash: c89d5eb754685fb8000ac2025af391057e77654c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848613"
---
#<a name="monthly-delta-update-isv-support-without-wsus"></a>月単位のデルタ WSUS せず ISV のサポートを更新します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

Windows 10 更新プログラムのダウンロードは、すべてのパッケージには、一貫性とわかりやすくするために確実にすべての以前にリリースされた修正プログラムが含まれているために、大規模なことができます。  

バージョン 7、Windows 以来と呼ばれる機能と Windows 更新プログラムのダウンロードのサイズを減らすことが[Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)、コンシューマー デバイスはサポートが既定では、Windows 10 enterprise デバイスが Windows Server 更新プログラムを必要とExpress を活用するために services (WSUS)。 WSUS が使用可能な場合を参照してください。[高速更新プログラムの ISV の配信サポート](express-update-delivery-ISV-support.md)します。 高速更新プログラムの配信を有効にするために使用することをお勧めします。 

WSUS がインストールされていないパッケージのサイズはそれまでの間でより小さな更新が必要な場合は、月単位のデルタの更新プログラムを使用できます。 デルタの更新プログラムがないくらい Express の WSUS 更新プログラムの配信と同様、実質的に、パッケージのサイズが減少します。 パッケージのサイズの最大の減少をできる限り WSUS Express の更新を展開することをお勧めします。 Windows 10 バージョン 1607 のデルタ、累積および Express のダウンロード サイズの比較グラフを次に示します。

![ダウンロード サイズの比較](../../media/express-update-delivery-isv-support/delta-1.png)

##<a name="what-is-monthly-delta-update"></a>月単位のデルタの更新プログラムとは何ですか。

月次セキュリティ更新プログラムの 2 つのバリエーションがあります。デルタと累積します。

デルタの月の更新は、新規および更新パッケージのサイズを減らすために使用可能な WSUS を持たない Isv の暫定的なソリューション。

>[!IMPORTANT]
>**デルタの更新プログラムは、Windows 10、バージョン 1607 (Anniversary Update)、バージョン 1703 (Creators Update)、およびバージョン 1709 (Fall Creators Update) のサービスを提供可能です。** バージョン 1709 以降後のリリースをサポートする展開インフラストラクチャを実装する必要があります[高速更新プログラムの配信](express-update-delivery-ISV-support.md)を引き続きご利用の増分更新します。

月単位のデルタの更新プログラムを使用すると、パッケージが 1 つの月の更新プログラムのみ含まれます。 毎月の累積的なには、その更新プログラムのリリースまでのすべての更新プログラムには 1 か月あたりの増大する、大規模なファイルが含まれています。 デルタと月次の更新プログラムの両方が「更新火曜日」とも呼ばれます毎月の第 2 火曜日にリリースされます。 次の表は、デルタ ファイルと累積的更新プログラムを比較します。

|                    | 毎月**デルタ**更新                                                                                                                                                                                                       | 毎月**累積**更新                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scope**          | 1 つの更新で**その月の新しい修正プログラム**                                                                                                                                                                           | 月と以前のすべての月のすべての新しい修正プログラムを 1 つの更新                                                                                                                                                   |
| **アプリケーション**    | 前の月の更新プログラムが適用されている (累積的なまたは差分) 場合にのみ適用できます。                                                                                                                                           | いつでも適用できます。                                                                                                                                                                                                |
| **配信**       | **Windows Update カタログにのみ公開**他のツールやプロセスで使用するためダウンロードできます。 Windows Update に接続されている Pc には提供されません。                                                         | Windows の更新プログラム (場所すべてコンシューマー Pc インストールされます)、WSUS、および、Windows Update カタログに発行                                                                                                                |

デルタと累積的なサポート技術情報の同じ番号、同じの分類を持つと同時にリリースします。 カタログで更新プログラム タイトルまたは msu の名前、更新プログラムを識別できます。

- 2017-02 *\***差分更新**\** (KB1234567) x64 ベース システム用の Windows 10 バージョン 1607 用
- 2017-02 *\***cumulative Update**\** (KB1234567) x86 ベース システム用の Windows 10 バージョン 1607 用                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>デルタの月の更新を使用する場合

クライアント デバイスに更新プログラムのサイズを重視する場合は、デルタの更新プログラムを使用して、前の月の更新、および累積が遅れているデバイスに更新されたデバイスでお勧めします。 これにより、すべてのデバイスには、1 つの更新に戻すことの最新の状態のみが必要です。 最新のデバイスは、組織内に基づく別の更新を展開する必要があります、全体的な更新プログラム管理プロセスで小規模な調整が必要です。

![ダウンロード サイズの比較](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>同じ月で、デルタ ファイルと累積更新プログラムの展開を防ぐ

動作を理解しておく必要が差分更新プログラムと累積更新プログラムは同時に使用可能なであるため、同じ月で両方の更新プログラムを展開する場合。

承認して、同じバージョンの差分および累積更新プログラムを展開する場合のみが生成されません追加のネットワーク トラフィック両方が、PC にダウンロードされますが、再起動後に、Windows コンピューターを再起動することができないためです。

デルタと累積的更新プログラムの両方が意図せずにインストールされているし、コンピューターが起動できなく、次の手順で回復できます。

1. WinRE コマンド プロンプトを起動します。
2. 保留状態のパッケージを一覧表示します。

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **例**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. パイプを使用して、テキスト ファイルを開く**get パッケージ**します。 インストール保留中の修正プログラムを表示する場合は、実行**パッケージの削除**パッケージ名ごとに。
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **例**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >削除しないでください保留中の修正プログラムをアンインストールします。

>[!IMPORTANT]
>**デルタの更新プログラムは、Windows 10、バージョン 1607 (Anniversary Update)、バージョン 1703 (Creators Update)、およびバージョン 1709 (Fall Creators Update) のサービスを提供可能です。** バージョン 1709 以降後のリリースをサポートする展開インフラストラクチャを実装する必要があります[高速更新プログラムの配信](express-update-delivery-ISV-support.md)を引き続きご利用の増分更新します。
