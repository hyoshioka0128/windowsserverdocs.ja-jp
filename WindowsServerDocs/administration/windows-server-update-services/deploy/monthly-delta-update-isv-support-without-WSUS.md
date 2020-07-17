---
title: WSUS を使用しない毎月の差分更新 ISV のサポート
description: Windows Server Update Service (WSUS) のトピック - 独立系ソフトウェア ベンダー (ISV) が WSUS Express 更新プログラム配信ではなく毎月の差分更新プログラムを一時的に使用してパッケージ サイズを小さくする方法
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 3ccddd3bfd55ae340dc5273905bb475e7d2cb98a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80828745"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>WSUS を使用しない毎月の差分更新 ISV のサポート

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

Windows 10 更新プログラムでは、すべてのパッケージにそれまでのすべての修正が含まれています。これは一貫性を保ち、更新を簡素化するためですが、それによってダウンロードのサイズが大きくなることがあります。  

Windows では、バージョン 7 以降、[エクスプレス](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)と呼ばれる機能を使用して Windows Update ダウンロードのサイズを縮小できるようになりました。コンシューマー デバイスでは既定でサポートされていますが、Windows 10 エンタープライズ デバイスでエクスプレスを利用するには Windows Server Update Services (WSUS) が必要です。 WSUS を利用できる場合は、「[更新プログラムのエクスプレス配信 ISV のサポート](express-update-delivery-ISV-support.md)」を参照してください。 これを使用して更新プログラムのエクスプレス配信を有効にすることをお勧めします。 

現在 WSUS がインストールされていなくても、当面必要な更新パッケージのサイズが比較的小さい場合は、毎月の差分更新を使用できます。 差分更新では、パッケージ サイズが大幅に縮小されますが、WSUS Expres 更新プログラム配信ほどではありません。 パッケージ サイズを最大限に縮小するには、可能な限り WSUS Expres 更新プログラムをデプロイすることをお勧めします。 次に示すのは、Windows 10 バージョン 1607 の差分、累積、エクスプレスのダウンロード サイズを比較したグラフです。

![ダウンロード サイズの比較](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>毎月の差分更新とは

毎月のセキュリティ更新には次の 2 つのバリエーションがあります:差分と累積。

毎月の差分更新は新しいものであり、更新パッケージのサイズを縮小するために WSUS を使用できない ISV 向けの暫定的なソリューションです。

>[!IMPORTANT]
>**差分更新は、Windows 10 バージョン 1607 (Anniversary Update)、バージョン 1703 (Creators Update)、バージョン 1709 (Fall Creators Update) のサービスに利用できます。** バージョン 1709 より後のリリースでは、増分更新を引き続き利用するために[更新プログラムのエクスプレス配信](express-update-delivery-ISV-support.md)をサポートするデプロイ インフラストラクチャを実装する必要があります。

毎月の差分更新を使用すると、パッケージには 1 か月分の更新プログラムのみが含まれます。 毎月の累積には、その更新プログラムのリリースまでのすべての更新プログラムが含まれるので、毎月拡大する大きなファイルになります。 差分更新と毎月の更新は、毎月第 2 火曜日にリリースされ、Update Tuesday とも呼ばれています。 次の表は、差分更新と累積更新を比較したものです。

|                    | 毎月の**差分**更新                                                                                                                                                                                                       | 毎月の**累積**更新                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scope**          | **その月の新しい修正のみ**を含む単一の更新プログラム                                                                                                                                                                           | その月と過去のすべての月のすべての新しい修正を含む単一の更新プログラム                                                                                                                                                   |
| **アプリケーション**    | 前の月の更新 (累積または差分) が適用された場合にのみ適用できます                                                                                                                                           | いつでも適用できます                                                                                                                                                                                                |
| **配信**       | 他のツールやプロセスで使用するためにダウンロードできる **Windows Update カタログにのみ発行されます**。 Windows Update に接続されている PC には提供されません                                                         | Windows Update (すべてのコンシューマー PC によってインストールされます)、WSUS、Windows Update カタログに発行されます                                                                                                                |

差分と累積は同じサポート技術情報番号と同じ分類を持ち、同時にリリースされます。 更新プログラムは、カタログ内の更新プログラムのタイトルまたは msu の名前で区別できます。

- 2017-02 x64 ベース システム用 Windows 10 Version 1607 の " *\***差分更新プログラム**\**  " (KB1234567)
- 2017-02 x86 ベース システム用 Windows 10 Version 1607 の " *\***累積更新プログラム**\**  " (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>毎月の差分更新を使用するケース

クライアント デバイスの更新プログラムのサイズが問題になる場合は、前月の月次更新プログラムがインストールされているデバイス上で差分更新を使用し、更新が遅れているデバイス上で累積更新を使用することをお勧めします。 このようにすると、すべてのデバイスを最新の状態にするために必要な更新プログラムが 1 つだけになります。 この場合、組織内のデバイスがどの程度新しいかに基づいて異なる更新プログラムをデプロイする必要があるため、全体的な更新管理プロセスに小さな調整が必要です。

![ダウンロード サイズの比較](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>差分と累積の更新プログラムが同じ月にデプロイされないようにする

差分更新と累積更新は同時に利用できるため、両方の更新プログラムを同じ月にデプロイするとどうなるかを理解することが重要です。

同じバージョンの差分および累積更新を承認してデプロイした場合、両方が PC にダウンロードされるため追加のネットワーク トラフィックが生成されるだけでなく、再起動後にコンピューターで Windows を起動できない可能性があります。

差分と累積の両方の更新プログラムが誤ってインストールされ、コンピューターが起動しなくなった場合は、次の手順で復旧できます。

1. WinRE コマンド プロンプトでブートします
2. 保留中状態のパッケージを一覧表示します。

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **例**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. **get-packages** にパイプで指定したテキスト ファイルを開きます。 インストール保留中の修正プログラムが表示されている場合は、パッケージ名ごとに **remove-package** を実行します。
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **例**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >アンインストール保留中の修正プログラムは削除しないでください。

>[!IMPORTANT]
>**差分更新は、Windows 10 バージョン 1607 (Anniversary Update)、バージョン 1703 (Creators Update)、バージョン 1709 (Fall Creators Update) のサービスに利用できます。** バージョン 1709 より後のリリースでは、増分更新を引き続き利用するために[更新プログラムのエクスプレス配信](express-update-delivery-ISV-support.md)をサポートするデプロイ インフラストラクチャを実装する必要があります。
