---
title: Windows Admin Center SDK のケース スタディの純粋なストレージ
description: Windows Admin Center SDK のケース スタディの純粋なストレージ
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849923"
---
# <a name="pure-storage-extension"></a>純粋なストレージの拡張機能

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Windows Admin Center のエンド ツー エンドの配列の管理を提供します。 

[純粋な記憶域](https://www.purestorage.com/)エンタープライズ、ビジネスの競争優位性を促進するデータ中心のアーキテクチャを提供するオール フラッシュ データ記憶域ソリューションを提供します。  純粋な Microsoft Windows server の認定、Microsoft ゴールド パートナーし、技術的な統合など、Azure では、重要な Microsoft ソリューションを開発して、HYPER-V、SQL Server、System Center、Windows PowerShell、および Windows SMB します。 純粋には、純粋な FlashArray 製品に単一枠ビューを提供する Windows Admin Center の最新リリースをサポートしている拡張機能のテクニカル プレビューを最近発表しました。  この拡張機能からのユーザーは監視タスクを実行、リアルタイムのパフォーマンスのメトリックを表示および記憶域ボリュームとイニシエーターを管理するための 1 つのツールから学ぶ: トレーニング情報します。

早い段階で、Windows Admin Center は、「プロジェクト ホノルル」と呼ばれますが、純粋は顧客に提供するための値を確認し、Windows Admin Center を提供するガラスの 1 つのウィンドウから複数の純粋な記憶域 FlashArrays を管理する機能をパートナーします。

純粋な「プロジェクト ホノルル」によるユース ケースを調査を開始するときに、すぐに Windows Admin Center と FlashArray の間の統一された管理エクスペリエンスを提供する可能性を実現します。 純粋な機能の実装の詳細を定義に役立ち、Windows Admin Center エンジニア リング チームと緊密に連携します。 純粋な Windows Admin Center の初期の段階でのフィードバックの提供や Microsoft チームへの投稿を行うこともできました。 

![純粋なストレージの拡張機能](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Windows Admin Center 内から直接管理できるように、FlashArray web インターフェイスを模倣する機能セットを統合しました。2 つのさまざまな管理ツールではなくガラスの 1 つのペインからは、顧客やパートナーが役立ちます。単一の管理ポイントに加えて利点顧客できなくコンテキストに応じて、FlashArray に接続されている Windows サーバーを管理する。"</cite>
>
> --Barkz、テクニカル ディレクターを Microsoft ソリューションと統合、純粋なストレージ

純粋なストレージ ソリューションの拡張機能に含まれている機能は次のとおりです。
- 複数の FlashArrays に接続します。
- IOPs、帯域幅、待機時間、データの削減、スペースの管理を含む、FlashArray 詳細を表示します。 これらは、FlashArray 管理 GUI から取得したすべての同じ詳細です。
- Windows Server ホストとクラスター化共有ボリューム (Csv) の共有ボリュームへのアクセスを有効にするに使用される構成済みのホスト グループを表示します。
- ビュー ホスト: iSCSI ホスト名を含む使用可能なすべての接続情報修飾名 (Iqn) とワールド ワイド名 (Wwn)。
- ボリュームを管理するには、作成およびボリュームを破棄する機能が含まれます。 ボリュームが破棄され、破棄のアイテムのバケットに配置されますメイン FlashArray 管理 GUI から Eradicate する必要があります。
- イニシエーターを管理するには、これは、Windows Admin Center 展開によって管理されている個々 のサーバーにコンテキストを提供する最も興味深い機能の 1 つ。 マルチパス IO (MPIO) がインストールされている構成と作成/マウントの新しいボリュームの場合は、チェック、個々 の Windows サーバーに接続されたディスク (ボリューム) を表示できます。

A[デモ ビデオについて](https://youtu.be/IFAeCAd6V2g)が作成されたすべての純粋なストレージ ソリューションの拡張機能を提供する機能を示すです。 

次のスクリーン ショットには、特定の Windows Server ホストに接続しているどのようなディスク (ボリューム) を表示する示しています。 接続の詳細を表示する以外にマルチパス IO が構成されているかどうかを確認します。

![純粋なストレージの拡張機能](../../media/extend-case-study-purestorage/purestorage-2.png)

だけでなく、ディスクを表示するには、新しいボリュームを作成およびすぐに Windows ディスク管理ツールを使用することがなく、ホストにマウントします。

![純粋なストレージの拡張機能](../../media/extend-case-study-purestorage/purestorage-3.png)

以降、Technical Preview をリリースするには、これまでに収集されたお客様のフィードバックは非常に肯定的し、がも提供されます。 将来のリリースを追加するさまざまな機能を把握します。 

その他の情報:
- [純粋なストレージの拡張機能のお知らせブログの投稿](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2)ポッド キャスト
