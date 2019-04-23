---
title: HYPER-V レプリカのアプリケーション整合性スナップショットを有効にする VSS ベースのバックアップ用ゲスト オペレーティング システムを構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b4300dd4b7adc0cef8544215b5da62044a97301b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863893"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>HYPER-V レプリカのアプリケーション整合性スナップショットを有効にする VSS ベースのバックアップ用ゲスト オペレーティング システムを構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*アプリケーション整合性スナップショットでは、ボリューム シャドウ コピー サービス (VSS) が有効になっているし、レプリケーションに参加している仮想マシンのゲスト オペレーティング システムで構成されていることが必要です。*  
  
## <a name="impact"></a>影響  
*レプリケーションの構成では、アプリケーション整合性スナップショットが指定されている場合でも、HYPER-V は使用しませんに VSS が構成されていない場合。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*仮想マシンで統合サービスをインストールするには、仮想マシンの接続を使用します。*  
  


