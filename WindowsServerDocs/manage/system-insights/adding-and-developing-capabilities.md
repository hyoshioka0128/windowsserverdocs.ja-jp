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
ms.openlocfilehash: 891edb108bc2c298c70b29c596fb8d0ca0e06b7e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475189"
---
# <a name="adding-and-developing-new-capabilities"></a>新機能の追加と開発

>適用先:Windows Server 2019

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

## <a name="additional-references"></a>その他のリファレンス
System Insights の詳細については、次のリソースを参照してください。

- [システム インサイトの概要](overview.md)
- [機能について](understanding-capabilities.md)
- [管理機能](managing-capabilities.md)
- [機能の追加、削除、更新](add-remove-update-capabilities.md)
- [System Insights の FAQ](faq.md)