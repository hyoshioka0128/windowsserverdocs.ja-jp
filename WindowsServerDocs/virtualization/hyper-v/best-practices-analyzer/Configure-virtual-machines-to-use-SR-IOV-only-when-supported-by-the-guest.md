---
title: 仮想マシンが、ゲストオペレーティングシステムでサポートされている場合にのみ sr-iov を使用するように構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8c43e06806f66ce0faae255f0f34d80a653fbe10
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366259"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>仮想マシンが、ゲストオペレーティングシステムでサポートされている場合にのみ sr-iov を使用するように構成する

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上の仮想マシンがシングルルート i/o 仮想化 (SR-IOV) を使用するように構成されていますが、ゲストオペレーティングシステムが sr-iov をサポートしていません*  
  
## <a name="impact"></a>影響  
*Sr-iov 仮想機能は、次の仮想マシンには割り当てられません。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Sr-iov をサポートしていないゲストオペレーティングシステムを実行しているすべての仮想マシンで sr-iov を無効にします。*  
  
Sr-iov は、一部の64ビット Windows ゲストでのみサポートされています。 詳細については、「 [hyper-v の機能と世代とゲストの互換性](../Hyper-V-feature-compatibility-by-generation-and-guest.md)」を参照してください。  
  


