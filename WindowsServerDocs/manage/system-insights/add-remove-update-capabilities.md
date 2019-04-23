---
title: 機能の追加、削除、更新
description: Insights のシステムでは、既存のデータ収集と管理機能を活用する新機能を作成することができます。 また、プラットフォームのサポートを追加、削除、およびこれらの機能更新プログラムを管理するがあることが重要です。 このトピックでは、追加、削除、およびシステム Insights での機能の更新に高度な機能について説明します。
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
ms.openlocfilehash: 07fb036d1c4aa4a63107594ec1f81cb5be1c7724
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880163"
---
# <a name="adding-removing-and-updating-capabilities"></a>機能の追加、削除、更新

>適用先:Windows Server 2019

Insights のシステムでは、既存のデータ収集と管理機能を活用する新機能を作成することができます。 これらの機能が作成されると、ただし、これはも追加、削除、およびこれらの機能更新プログラムを管理するプラットフォームのサポートがあることも重要です。 

このトピックでは、追加、削除、およびシステム Insights での機能の更新に高度な機能について説明します。 

## <a name="adding-a-capability"></a>機能の 1 つの追加
使用していつでも新しい機能を追加することができますシステム Insights、**追加 InsightsCapability**コマンドレット。 **追加 InsightsCapability**機能名と機能のライブラリを指定する必要があります。 機能のライブラリには、機能の説明、データ ソース、および予測ロジックが含まれています。

```PowerShell
Add-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapability.dll"
```

Insights のシステムに機能が追加された後すぐに呼び出すし、PowerShell または Windows Admin Center を使用して機能を管理します。 

## <a name="updating-a-capability"></a>機能の 1 つの更新
Insights のシステムでは機能を使用して、更新することもできます、 **Update InsightsCapability**コマンドレット。

```PowerShell
Update-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapabilityv2.dll"
```

機能の 1 つの更新機能の説明、データ ソース、およびその機能に関連付けられている予測ロジックを変更することができますが、新しい機能ライブラリを指定することができます。 重要なは、機能の 1 つの更新は、すべての構成とカスタム スケジュール、アクション、および履歴予測結果を含む、その機能に関する履歴情報が保持されます。 

## <a name="removing-a-capability"></a>機能の 1 つを削除します。
システム Insights を使用して、機能を削除することも、**削除 InsightsCapability**コマンドレット。 

```PowerShell
Remove-InsightsCapability -Name "Sample capability" 
```
>[!NOTE]
>既定の予測機能を削除できません。

機能の 1 つを完全に削除するには、機能と、スケジュール、修復アクション、および過去の予測結果を含む、関連付けられているすべての情報が削除されます。 

>[!TIP]
>機能に関連付けられているすべての情報を完全に削除する方法について懸念している場合に削除するのではなく、機能を無効にすることを検討します。 

## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [システム Insights の概要](overview.md)
- [機能の理解](understanding-capabilities.md)
- [機能を管理します。](managing-capabilities.md)
- [追加して、機能の開発](adding-and-developing-capabilities.md)
- [システム Insights に関する FAQ](faq.md)