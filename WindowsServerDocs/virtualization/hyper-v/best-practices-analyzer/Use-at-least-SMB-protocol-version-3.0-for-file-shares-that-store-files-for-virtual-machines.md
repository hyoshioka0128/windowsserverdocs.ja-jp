---
title: バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b2393e2aa0418758ff59c527cef6f38a0c8b8402
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948389"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*仮想マシンファイルまたは仮想ハードディスクファイルは、SMB プロトコルバージョン3.0 以降をサポートしていないファイル共有に格納されます。*

## <a name="impact"></a>**影響**
*Microsoft では、この構成をサポートしていません。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*SMB プロトコルバージョン3.0 以降を使用しているファイル共有にファイルを移動します。*



