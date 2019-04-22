---
title: 機能の追加と開発
description: Insights のシステムでは、任意の OS 更新プログラムを必要とせず、システム Insights に新しい予測機能を追加することができます。 これにより、Microsoft とサード パーティを作成し、関心のあるシナリオに対処する機能の新しい中間リリースを提供するなど、開発者ができます。 既存のシステム Insights 管理プレーンの統合もと新機能は、カスタム データを収集して分析するを指定できます。
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
ms.date: 7/31/2018
ms.openlocfilehash: 8caddead774ac69a38906f3c0a0d2eaf005c1d28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817483"
---
# <a name="adding-and-developing-new-capabilities"></a>追加して、新しい機能の開発

>適用先:Windows Server 2019

Insights のシステムでは、任意の OS 更新プログラムを必要とせず、システム Insights に新しい予測機能を追加することができます。 これにより、Microsoft とサード パーティを作成し、関心のあるシナリオに対処する機能の新しい中間リリースを提供するなど、開発者ができます。 

すべての新機能と統合、既存のシステム Insights インフラストラクチャを拡張します。

- 新機能のことができます**パフォーマンス カウンターまたはシステム イベントを指定**、これは収集、ローカルに永続化および機能が呼び出されたときに、分析のための機能に返されます。  
- 新しい機能は**既存の Windows Admin Center を活用して、管理プレーンの PowerShell**します。 だけでなく、新機能は、Insights のシステムで検出されるからカスタムのスケジュールと修復アクションにも活用します。 

## <a name="manage-new-capabilities"></a>新しい機能を管理します。
- [学習](add-remove-update-capabilities.md)を追加、削除、および PowerShell を使用して機能を更新する方法。 

## <a name="develop-a-capability"></a>機能の 1 つの開発します。
独自のカスタム機能を記述を開始に役立つ次のリソースを使用します。
- [学習](data-sources.md)についてデータ ソースを収集することができます。
- [ダウンロード](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/)システム Insights NuGet パッケージは、クラスと機能の 1 つを記述する必要があるインターフェイスが含まれています。
- [参照してください](https://aka.ms/systeminsights-api)API ドキュメントをシステム Insights クラスとインターフェイスについて説明します。 
- [使用](https://aka.ms/systeminsights-samplecapability)に役立つシステム Insights サンプルの機能は、開始を取得します。 これは、機能の 1 つの登録を収集するデータ ソースを指定、およびシステム データの分析を開始する方法を示します。

>[!NOTE]
>これは、プレリリース機能です。 新しい機能を追加し、フィードバックを組み込むと、変更される可能性が。

## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [システム Insights の概要](overview.md)
- [機能の理解](understanding-capabilities.md)
- [機能を管理します。](managing-capabilities.md)
- [追加、削除、および機能の更新](add-remove-update-capabilities.md)
- [システム Insights に関する FAQ](faq.md)