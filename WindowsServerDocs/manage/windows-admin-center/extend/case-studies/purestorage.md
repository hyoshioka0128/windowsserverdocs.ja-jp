---
title: Windows Admin Center SDK のケース スタディ - 純粋な記憶域
description: Windows Admin Center SDK のケース スタディ - 純粋な記憶域
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: ebeec824f802f020d0ece17524ba43b1baeba893
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2019
ms.locfileid: "8995367"
---
# 純粋な記憶域の拡張機能

## Windows Admin Center のエンド ツー エンドの配列の管理を提供します。 

[純粋な記憶域](https://www.purestorage.com/)は、enterprise、競争力のビジネスを加速するデータを中心としたアーキテクチャを提供するオール フラッシュ データ記憶域ソリューションを提供します。  純粋なは Microsoft Windows server では、認定、Microsoft ゴールド パートナーであり、Azure などのキーのマイクロソフト ソリューションの技術的な統合を開発して HYPER-V、SQL Server、System Center、Windows PowerShell、および Windows SMB します。 最近純粋なは、純粋な FlashArray 製品に 1 つのウィンドウのビューを提供する Windows Admin Center の最新リリースをサポートしている拡張機能のテクニカル プレビューを発表しました。  この拡張機能からユーザーの監視のタスクの実施、リアルタイムのパフォーマンス メトリックを表示および記憶域ボリュームとイニシエーターを管理するための 1 つのツールから能力がします。

早い段階で、Windows Admin Center は、"Project Honolulu"と呼ばれていました、純粋なお客様に提供することの値が表示されていたし、パートナーつにまとめられた Windows Admin Center を提供する 1 つのウィンドウから複数の純粋な記憶域 FlashArrays を管理すること。

純粋な"Project Honolulu"のユース ケースを調査を開始すると、すぐに実体化された Windows Admin Center と FlashArray の間で統一された管理エクスペリエンスを提供する可能性があります。 純粋な機能の実装の詳細の定義を支援 Windows Admin Center のエンジニア リング チームと緊密に連携します。 純粋なは Windows Admin Center の初期段階でフィードバックを提供して、Microsoft のチームに貢献を行うこともでした。 

![純粋な記憶域の拡張機能](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Windows Admin Center 内から直接管理を有効にする、FlashArray web インターフェイスを模倣した機能セットを統合しますされています。 お客様とパートナーで 2 つの異なる管理ツールと連携する必要があるとガラスの 1 つのウィンドウが役立ちます。 単一の管理ポイントだけでなくメリットをお客様できるようになりますコンテキスト、FlashArray に接続されている Windows サーバーを管理します。"</cite>
>
> -Barkz、テクニカル ディレクター Microsoft ソリューションとの統合、純粋な記憶域

純粋な記憶域ソリューション拡張機能に含まれている機能は次のとおりです。
- 複数の FlashArrays に接続します。
- IOPs、帯域幅、待機時間、データの削減スペースの管理など、FlashArray の詳細を表示します。 これらは、FlashArray 管理 GUI から取得したすべての同じ詳細です。
- Windows Server ホストとクラスター共有ボリューム (Csv) の共有ボリュームへのアクセスを有効にするために使用が構成済みのホスト グループを表示します。
- ビューがホスト: すべての接続情報がホスト名、iSCSI を含む利用可能な修飾名 (Iqn) と World Wide Name (Wwn)。
- 作成し、ボリュームを破棄する機能が含まれます: ボリュームを管理します。 ボリュームが破棄されるとは破棄項目バケットに配置し、メイン FlashArray 管理 GUI から Eradicate する必要があります。
- イニシエーターを管理するには、これは、Windows Admin Center の展開によって管理されている個々 のサーバーにコンテキストを提供する最も興味深い機能のいずれか。 マルチパス IO (MPIO) がインストールされている構成および作成/マウントの新しいボリュームの場合は、個々 の Windows サーバー、チェックに接続されているディスク (ボリューム) を表示できます。

[ビデオ デモ](https://youtu.be/IFAeCAd6V2g)が作成されているすべての純粋な記憶域ソリューション拡張機能を提供する機能を示しています。 

次のスクリーン ショット ディスク (ボリューム) が特定の Windows Server ホストに接続されている表示を示しています。 接続の詳細を表示するだけでなく、マルチパス IO が構成されているかどうかを確認します。

![純粋な記憶域の拡張機能](../../media/extend-case-study-purestorage/purestorage-2.png)

だけでなく、ディスクを表示するには、新しいボリュームを作成して Windows ディスクの管理ツールを使用することがなく、ホストにすぐにマウントします。

![純粋な記憶域の拡張機能](../../media/extend-case-study-purestorage/purestorage-3.png)

Technical Preview、これまでに収集されたお客様からのフィードバックを解放する非常に肯定的がも提供されます。 今後のリリースを追加するさまざまな機能を把握します。 

その他の情報
- [純粋な記憶域拡張機能の発表に関するブログの投稿](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2)ポッド キャスト
