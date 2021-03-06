---
title: 機能について
description: このトピックでは、Insights のシステムで機能の概念を定義し、Windows Server 2019 で使用できる既定の機能が導入されています。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 21932a3e45d7fc6711400eb30c63c3412bbc116e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830973"
---
# <a name="understanding-capabilities"></a>機能について

>適用先:Windows Server 2019

このトピックでは、Insights のシステムで機能の概念を定義し、Windows Server 2019 で使用できる既定の機能が導入されています。 

このトピックでは、データ ソース、予測の時間帯、および予測状態の既定の機能の使用にも説明します。 

## <a name="capability-overview"></a>機能の概要
システム Insights 機能とは、machine learning またはシステム データを提供するを分析して統計モデルの増加、展開の機能を把握します。 Insights のシステムに既定の機能の初期セットが導入されていて、オペレーティング システムを更新することがなく新機能を動的に追加することができます。 

>[!NOTE]
>詳細ドキュメントを作成する方法を説明を追加して、更新プログラム機能が利用可能な[ここ](adding-and-developing-capabilities.md)、および[管理の機能ドキュメント](managing-capabilities.md)についてのより高度な情報を提供します機能。

また、各機能は、Windows Server のインスタンスでローカルに実行し、各機能を個別に管理することができます。

### <a name="capability-outputs"></a>機能の出力
機能の 1 つが呼び出されたときに、その分析または予測の結果を説明するために出力を提供します。 各出力に含める必要があります、**状態**と**状態の説明**予測と各結果を説明するオプションで含めることができます、予測に関連付けられている機能に固有のデータ。 **状態の説明**のコンテキストの説明を提供するのに役立ちます、**状態**、レポート機能と、 **OK**、**警告**、または**重大**状態。 また、機能の 1 つを使用できます、**エラー**または**None**状態の予測が行われていない場合。 同時に、ここでは、機能の状態とその基本的な意味です。 

- **[Ok]** -も問題ないです。
- **警告**- 早急な措置が必要ありませんを参照してください。 
- **重要な**-を参照してくださいをすぐに行う必要があります。 
- **エラー** -不明な問題の原因と失敗する機能。 
- **None** -予測は行われませんでした。 データのない予測を行うための機能に固有の理由がないことが考えられます。 

ユーザーがアクセスできる JSON ファイル、およびファイル パスの結果に含まれている任意の機能に固有のデータの配置さらに、 [PowerShell を使用して検出できます](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results)します。 

## <a name="default-capabilities"></a>既定の機能
Windows Server の 2019 では、システム Insights には、容量の予測に重点を置いた 4 つの既定の機能が導入されています。

- **CPU 処理能力予測**-予測の CPU 使用率。 
- **ネットワーク容量の予測**-ネットワークの各ネットワーク アダプターの使用状況を予測します。 
- **記憶域の合計使用量予測**-予測は、すべてのローカル ドライブで記憶域の消費量を合計します。 
- **ボリュームの使用量予測**-各ボリュームのストレージ使用量を予測します。

各機能は以前の将来の使用状況を予測の履歴データを分析し、**短期的な動作ではなく、長期的な傾向を予測できるようにすべての予測機能**、正しく管理者を支援ハードウェアをプロビジョニングし、将来のリソースの競合を回避するために、ワークロードをチューニングします。 長期的な使用状況を対象にこれらの機能、ので、これらの機能は、1 日のデータを分析します。 

### <a name="forecasting-model"></a>予測モデル
既定の機能では、予測モデルを使用して、将来の使用量を予測して、各予測のモデルはローカルでトレーニング コンピューターのデータ。 このモデルは長いの的な傾向を検出するために設計されていて、特定の動作や各マシンの使用状況の微妙な差異を調整する機能により、各 Windows Server のインスタンスで再トレーニングします。

>[!NOTE]
>数万のマシンを含むデータセットを使用して多くのモデルのテストに必要なを使用するモデルの種類を決定します。 分析と、これらのモデルの調整、しました、自己回帰の予測モデルを使用するようにトレーニングに多くの時間を必要としない中に視覚的に直感的な正確な予測が生成されます。 ただし、このモデルでは、ため、3 週間以内のデータが得られるまで、各機能が基本的な線形の傾向を使用して、トレーニング データの 3 週間が必要です。

### <a name="forecasting-timelines"></a>タイムラインの予測
既定の機能は、将来のデータが収集済みの日数に基づいて指定の日数を予測します。 次の表では、これらの機能の予測のタイムラインを示します。

| 入力データ サイズ | 予測の長さ |
| --------------- | --------------- |
| 0 ~ 5 日間 | 予測は行われません。 |
| 6 ~ 180 日間 | 1/3 * 入力データのサイズ |
| 180 ~ 365 日 | 60 日間 | 

### <a name="forecasting-data"></a>予測データ
各機能は、将来の使用量を予測する 1 日のデータを分析します。 CPU、ネットワーク、およびでも記憶域使用率、ただし、頻繁に変更できます、1 日を通して、マシン上の作業負荷を動的に調整することです。 使用量が、1 日を通して定数がないためには、1 つのデータ ポイントで毎日の使用状況を正しく表す必要があります。 次の表は、特定のデータ ポイントと、データの処理方法を詳細します。


| 機能名 | データ ソース | フィルター処理のロジック |
| --------------- | -------------- | ---------------- |
 ボリュームの使用量の予測          | ボリュームのサイズ                    | 日単位の最大使用率              
 記憶域の合計使用量の予測   | ボリュームのサイズ、ディスクのサイズの合計の合計              | 日単位の最大使用率             
 CPU 容量の予測                | [% プロセッサ時間]  | 1 日あたり最大 2 時間の平均   
 ネットワーク容量の予測         | Bytes total/sec         | 1 日あたり最大 2 時間の平均  

フィルター処理のロジックの上、各機能が管理者に通知と将来の使用量で利用可能な容量: 明確超える場合でも、CPU 使用率が 100% をヒット一時的にしようとしたことに注意してください。 を評価するときに CPU 使用率がない可能性があります。意味のあるパフォーマンスの低下やリソースの競合が発生します。 CPU とネットワークは、次に、必要があります瞬間的なスパイクではなく、持続的な使用率が高い。 CPU の平均を計算し、ネットワーク全体の 1 日を通して使用状況、ただし、失う可能性が重要な使用方法については、高 CPU やネットワークの使用状況のいくつかの時間が重要なワークロードのパフォーマンスに影響する明確にします。 各日に最大 2 時間の平均を使用して、これらの極端なを回避し、分析するには、各機能の意味のあるデータを引き続き作成します。

ボリュームと記憶域の合計使用量は、ただし、記憶域使用率超えることはできません、使用可能な容量では、すぐにでも、そのこれらの機能の 1 日の最大使用率が使用します。 

### <a name="forecasting-statuses"></a>状態の予測
すべてのシステム Insights 機能に関連付けられた各予測状態を出力する必要があります。 既定の各機能は、各予測状態を定義するのに、次のロジックを使用します。
- **[OK]**:予測は、使用可能な容量を超えていません。
- **警告**:予測は、次の 30 日以内に利用可能な容量を超えています。 
- **重要な**:予測は、次の 7 日間に使用可能な容量を超えています。 
- **Error**: 機能の実行で予期しないエラーが発生します。 
- **[なし]**:予測を行うための十分なデータがありません。 データの不足が考えられますか、データが最近報告されていないためです。

>[!NOTE]
>場合、複数のボリュームやネットワーク アダプターなどの複数のインスタンスで機能の予測状態は、すべてのインスタンス間で最も重大な状態を反映します。 ボリュームまたはネットワーク アダプターごとに個々 の状態は、Windows Admin Center で、または各機能の出力に含まれるデータの表示。 既定の機能の JSON の出力を解析する方法については、次を参照してください。[このブログ](https://aka.ms/systeminsights-mitigationscripts)します。 


## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [システム Insights の概要](overview.md)
- [機能を管理します。](managing-capabilities.md)
- [追加して、機能の開発](adding-and-developing-capabilities.md)
- [システム Insights に関する FAQ](faq.md)
