---
title: 機能の追加と開発
description: System Insights を使用すると、OS の更新を必要とせずに、新しい予測機能を System Insights に追加できます。 これにより、Microsoft やサードパーティを含む開発者は、お客様の関心のあるシナリオに対処するための新機能を作成および提供することができます。 新しい機能では、収集および分析するカスタムデータを指定し、既存の System Insights 管理プレーンと統合することもできます。
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 0dd4e24197d5a8c438d70a849e435ce28792dfce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858435"
---
# <a name="adding-and-developing-new-capabilities"></a>新機能の追加と開発

>適用対象: Windows Server 2019

System Insights を使用すると、OS の更新を必要とせずに、新しい予測機能を System Insights に追加できます。 これにより、Microsoft やサードパーティを含む開発者は、お客様の関心のあるシナリオに対処するための新機能を作成および提供することができます。 

新しい機能は、既存の System Insights インフラストラクチャと統合し、拡張することができます。

- 新しい機能で**は、任意のパフォーマンスカウンターまたはシステムイベントを指定**できます。このイベントは、ローカルに収集されて保存され、機能が呼び出されたときに分析のために機能に返されます。  
- 新しい機能**では、既存の Windows 管理センターと PowerShell の管理プレーンを活用**できます。 新しい機能が System Insights で検出可能になるだけでなく、カスタムスケジュールや修復アクションの恩恵を受けることもできます。 

## <a name="manage-new-capabilities"></a>新機能の管理
- PowerShell を使用して機能を追加、削除、更新する方法に[ついて説明](add-remove-update-capabilities.md)します。 

## <a name="develop-a-capability"></a>機能の開発
独自のカスタム機能の作成を開始する際には、次のリソースを参考にしてください。
- 収集できるデータソースについて[説明](data-sources.md)します。
- 機能を記述するために必要なクラスとインターフェイスが含まれている System Insights NuGet パッケージを[ダウンロード](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/)します。
- System Insights のクラスとインターフェイスの詳細については、API のドキュメントを[参照](https://aka.ms/systeminsights-api)してください。 
- [使用](https://aka.ms/systeminsights-samplecapability)を開始するには、System Insights のサンプル機能を使用します。 ここでは、機能を登録する方法、収集するデータソースを指定する方法、およびシステムデータの分析を開始する方法を示します。

>[!NOTE]
>これはプレリリース機能です。 新しい機能を追加してフィードバックを組み込むため、変更される可能性があります。

## <a name="see-also"></a>参照
System Insights の詳細については、次のリソースを参照してください。

- [System Insights の概要](overview.md)
- [機能について](understanding-capabilities.md)
- [管理機能](managing-capabilities.md)
- [機能の追加、削除、更新](add-remove-update-capabilities.md)
- [System Insights の FAQ](faq.md)