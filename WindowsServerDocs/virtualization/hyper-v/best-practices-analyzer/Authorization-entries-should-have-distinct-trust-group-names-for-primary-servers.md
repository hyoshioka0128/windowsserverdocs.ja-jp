---
title: 承認エントリが同じ信頼グループの一部ではない仮想マシンのプライマリ サーバーに対して個別の信頼グループの名前
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8827a3a7-9f3c-4f51-826a-8e2ec43e01df
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e5c5b1a6bf8ef0bbceb5dde6b28cd951f399fc5e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882963"
---
# <a name="authorization-entries-should-have-distinct-trust-group-names-for-primary-servers-with-virtual-machines-that-are-not-part-of-the-same-trust-group"></a>承認エントリが同じ信頼グループの一部ではない仮想マシンのプライマリ サーバーに対して個別の信頼グループの名前

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
*サーバーでは、任意の仮想マシンと同じレプリケーション タグに関連付けられている承認一覧でサーバーからレプリカ仮想マシンのレプリケーション要求を受け入れられます。*  
  
## <a name="impact"></a>**影響**  
*プライバシーとさまざまな承認エントリに属するプライマリ サーバーからレプリケーションを受け入れる仮想マシンのセキュリティ問題の可能性があります。次の承認エントリへの影響:\<承認エントリの一覧 >*  
  
## <a name="resolution"></a>**解決方法**  
*プライマリ サーバーと同じセキュリティ グループの一部ではない仮想マシンの承認エントリでさまざまなタグを使用します。レプリケーションのタグを構成する HYPER-V の設定を変更します。*  
  


