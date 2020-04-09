---
title: VSS ベースのバックアップ用のゲストオペレーティングシステムを構成して、Hyper-v レプリカのアプリケーション整合性スナップショットを有効にする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f7a77b2cb743f478525f839e1c64ecc892b3fb04
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862065"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>VSS ベースのバックアップ用のゲストオペレーティングシステムを構成して、Hyper-v レプリカのアプリケーション整合性スナップショットを有効にする

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*アプリケーション整合性スナップショットを使用するには、レプリケーションに参加している仮想マシンのゲストオペレーティングシステムで、ボリュームシャドウコピーサービス (VSS) が有効になっていて構成されている必要があります。*  
  
## <a name="impact"></a>影響  
*レプリケーション構成でアプリケーション整合性スナップショットが指定されている場合でも、VSS が構成されていないと、Hyper-v はそれらを使用しません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*仮想マシンに統合サービスをインストールするには、仮想マシン接続を使用します。*  
  


