---
title: 'The WFP virtual switch extension should be enabled if it is required by third party extensions (Hyper-V: サード パーティ製の拡張機能で必要とされている場合、WFP 仮想スイッチ拡張機能を有効にする必要がある)'
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5afe706c246276597b32400109370ba3129e5a24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850623"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>The WFP virtual switch extension should be enabled if it is required by third party extensions (Hyper-V: サード パーティ製の拡張機能で必要とされている場合、WFP 仮想スイッチ拡張機能を有効にする必要がある)

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*Windows フィルタ リング プラットフォーム (WFP) の仮想スイッチ拡張機能は無効です。*  
  
## <a name="impact"></a>**影響**  
*次の仮想スイッチにいくつかサード パーティ製の仮想スイッチ拡張機能が正常に動作しません。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell コマンドレットを有効にする VMSwitchExtension を使用して、サード パーティ製の拡張機能によって必要な場合は、Windows フィルタ リング プラットフォームを有効にします。*  
  
### <a name="enable-the-windows-filtering-platform-using-windows-powershell"></a>Windows PowerShell を使用して Windows フィルタ リング プラットフォームを有効にします。  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  外部スイッチの名前の外部を交換した後、このコマンドを実行します。  
  
```  
Enable-VMSwitchExtension -VMSwitchName External -Name "Microsoft Windows Filtering Platform"  
```  
  
## <a name="see-also"></a>関連項目  
[Enable-VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx)  
  


