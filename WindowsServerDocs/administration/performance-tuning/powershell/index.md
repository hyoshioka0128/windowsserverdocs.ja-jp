---
title: PowerShell のパフォーマンス チューニング
description: PowerShell のパフォーマンス チューニング
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: jasonsh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 382305e2bd15ef6fcb038c3fa064bc2841eabae1
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80851955"
---
# <a name="performance-tuning-for-powershell"></a>PowerShell のパフォーマンス チューニング

このドキュメントでは、PowerShell 5.1 で可能な限り最適なパフォーマンスを達成するための一般的なガイドラインについて説明します。 このドキュメントで説明されている問題の一部は、今後のバージョンで解決する可能性があります。

このドキュメントでは、ベスト プラクティスについては説明しません。

このドキュメントのガイダンスは、十分に検討してから適用してください。
* 多くの場合、パフォーマンスは問題にならず、10 ミリ秒または 100 ミリ秒の短縮はまったく気付かれない可能性があります。
* このドキュメントのガイダンスの中には、混乱を招き、一部の PowerShell ユーザーにはなじみのない、一般的でない PowerShell の使用方法を説明しているものがあります。

以下のトピックでは、具体的なガイダンスを提供します。

-   [スクリプト作成に関する考慮事項](script-authoring-considerations.md)

-   [モジュール作成に関する考慮事項](module-authoring-considerations.md)