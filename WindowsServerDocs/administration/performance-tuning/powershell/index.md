---
title: PowerShell のパフォーマンス チューニング
description: PowerShell のパフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 628cc98033d8be3ee3c5db5c6747f0ea2b161b2e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891803"
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