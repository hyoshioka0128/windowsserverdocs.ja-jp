---
title: 'The WFP virtual switch extension should be enabled if it is required by third party extensions (Hyper-V: サード パーティ製の拡張機能で必要とされている場合、WFP 仮想スイッチ拡張機能を有効にする必要がある)'
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 628f58ef57e6a461791cd9641d043acfbfd79129
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993448"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>The WFP virtual switch extension should be enabled if it is required by third party extensions (Hyper-V: サード パーティ製の拡張機能で必要とされている場合、WFP 仮想スイッチ拡張機能を有効にする必要がある)

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*Windows フィルタ リング プラットフォーム (WFP) の仮想スイッチ拡張機能は無効です。*

## <a name="impact"></a>**影響**
*次の仮想スイッチでは、いくつかサード パーティ製の仮想スイッチ拡張機能が正常に動作しない可能性があります。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*サード パーティ製の拡張機能に必要な場合は、Windows フィルタ リング プラットフォームを有効にするのにには、有効にする-VMSwitchExtension である Windows PowerShell コマンドレットを使用します。*

### <a name="enable-the-windows-filtering-platform-using-windows-powershell"></a>Windows PowerShell を使用して Windows フィルタ リング プラットフォームを有効にします。

1.  Windows PowerShell を開きます。 (デスクトップから [**スタート**] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  外部スイッチの名前の外部を交換した後、このコマンドを実行します。

```
Enable-VMSwitchExtension -VMSwitchName External -Name Microsoft Windows Filtering Platform
```

## <a name="see-also"></a>参照
[有効にする VMSwitchExtension](/powershell/module/hyper-v/enable-vmswitchextension?view=win10-ps)