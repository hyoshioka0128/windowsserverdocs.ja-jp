---
title: リリース ノート - Windows Server 2019 に関する重要な問題
description: クラッシュ、ハング、インストールの障害およびデータの損失を回避するために回避策を必要とする重要な問題をまとめたものです。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 515255c301d343aa1b83bcfb506f2e3baa6ca969
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810741"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>リリース ノート - Windows Server 2019 に関する重要な問題

>適用先:Windows Server 2019

これらのリリース ノートがわかっている場合の回避や、問題を回避する方法を含めて、Windows Server 2019 オペレーティング システムで最も重要な問題を要約します。 設計による変更、新機能、および今回のリリースで修正プログラムについては、次を参照してください。[で Windows Server 2019 新](whats-new-19.md)と特定の機能チームからのお知らせします。 指定しない場合、報告された各問題はすべてのエディションおよび Windows Server 2019 のインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  

## <a name="release-notes"></a>リリース ノート

次の既知の問題は、Windows Server 2019 表示されます。

| タイトル         | 説明                            |
| -----         | -----------                            |
| サーバーのセットアップ中にインストール オプション メニューには、ドイツ語のテキストが切り捨てられて | デスクトップ エクスペリエンスのインストール オプションの説明が最後に、不足していると正しくない文字をある「をインストールするオペレーティング システムの選択」という、オペレーティング システムの選択ウィンドウで、ドイツ語サーバーのメディアからセットアップを実行する場合文。 完全なドイツ語のテキストがここで表示されるはずです。<br/>      <br/>`Durch diese Option wird die vollständige grafische Umgebung von Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird. Sie kann hilfreich sein, wenn Sie den Windows-Desktop verwenden möchten oder über eine App verfügen, die die grafische Umgebung benötigt.` <br><br>これには、パブリックの可用性の Windows Server 2019、Windows Server、バージョンは 1809、および Microsoft HYPER-V Server 2019 では、リリース、ドイツ語のメディアのみに影響します。|
| Windows Server のブランド化イメージが Windows Server バージョンは 1809 のセットアップ時に正しくないです。 | Windows Server バージョンは 1809 のセットアップ エクスペリエンス中にいくつかの最初の背景画像が表示を画面&quot;Windows Server 2019&quot;します。  、Windows server バージョン 1709 および 1803、これだけ表示されるはずと&quot;Windows Server&quot;します。  その他の製品にその他の場所への影響がないと、Windows Server 2019 製品への影響はありません。  問題は、Windows Server バージョンは 1809、ボリューム ライセンスのお客様が、ボリューム ライセンス サービス センターへのアクセスにのみ使用できますのセットアップ時にこの 1 つのイメージに制限されます。<br/> |

### <a name="copyright"></a>著作権

このドキュメントは「現状有姿のまま」提供されます。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、ドキュメントを複製して使用することができます。

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  


1.0  
