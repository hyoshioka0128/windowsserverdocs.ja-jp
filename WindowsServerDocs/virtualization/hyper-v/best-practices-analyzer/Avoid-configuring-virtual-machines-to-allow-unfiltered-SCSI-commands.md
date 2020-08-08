---
title: フィルター処理される SCSI コマンドを許可するようにバーチャルマシンを構成しない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 33c211073c74da334abb8b483fa36974216a1185
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948585"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>フィルター処理される SCSI コマンドを許可するようにバーチャルマシンを構成しない

>適用先:Windows Server 2016



*ベストプラクティスとスキャンの詳細については、「ベストプラクティスアナライザー」を参照してください* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|操作|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*フィルター処理されていない SCSI コマンドを許可するようにバーチャルマシンが構成されています。*

## <a name="impact"></a>影響

*SCSI コマンドフィルターをバイパスすると、セキュリティ上のリスクが生じます。この構成は、ゲストオペレーティングシステムで実行されているストレージアプリケーションとの互換性を確保するために必要な場合にのみ有効にしてください。次のバーチャルマシンは、フィルター処理されていない SCSI コマンドを許可するように構成されています:*

\<list of virtual machine names>

## <a name="resolution"></a>解決方法

*この構成が必要かどうかを判断するには、記憶域のベンダーに問い合わせてください。また、管理オペレーティングシステムまたはその他のゲストオペレーティングシステムが侵害されたり、通常とは異なる動作が発生したりした場合は、コマンドをブロックするようにバーチャルマシンを再構成します。*



