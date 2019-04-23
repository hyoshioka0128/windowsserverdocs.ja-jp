---
title: フィルター処理されていない SCSI コマンドを許可する仮想マシンを構成しない場合
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f401ce4d72f88d72529a95acea2a999df93679b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888273"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>フィルター処理されていない SCSI コマンドを許可する仮想マシンを構成しない場合

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*フィルター処理されていない SCSI コマンドを許可する仮想マシンが構成されます。*  
  
## <a name="impact"></a>影響  
  
*SCSI コマンドのポーズをフィルター処理、セキュリティ リスクをバイパスします。この構成は、ゲスト オペレーティング システムで実行されているストレージ アプリケーションの互換性のために必要な場合にのみ有効にする必要があります。次の仮想マシンは SCSI コマンドをフィルター処理されていない許可するように構成されます。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*この構成が必要なかどうかを判断する、記憶域ベンダーに問い合わせてください。また、管理オペレーティング システムまたはその他のゲスト オペレーティング システムが改ざんされた場合または異常な動作のコマンドをブロックする仮想マシンを再構成します。*  
  


