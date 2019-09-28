---
title: 'リリース ノート: Windows Server 2019 に関する重要な問題'
description: クラッシュ、ハング、インストールの失敗、およびデータの損失を回避するための対策を必要とする重大な問題についてまとめます。
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 6f0a13401810adebb299f0b0c9607bfe58bb405d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360813"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>リリース ノート: Windows Server 2019 に関する重要な問題

>適用先:Windows Server 2019

これらのリリース ノートでは、Windows Server 2019 オペレーティング システムの最も重大な問題とその回避策 (存在する場合) がまとめられています。 このリリースにおける計画的な変更点、新機能、および修正プログラムについては、「[Windows Server 2019 の新機能](whats-new-19.md)」と特定の機能チームからのお知らせを参照してください。 特に指定がない限り、報告されている問題は、Windows Server 2019 のすべてのエディションとインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  

## <a name="release-notes"></a>リリース ノート

Windows Server 2019 には、以下の既知の問題が存在します。

| タイトル         | 説明                            |
| -----         | -----------                            |
| サーバーのセットアップ時のインストール オプション メニューで、ドイツ語のテキストが切り捨てられる | [インストールするオペレーティング システムを選択してください] というタイトルのオペレーティング システム選択ウィンドウで、ドイツ語版のサーバー メディアからセットアップを実行すると、デスクトップ エクスペリエンスのインストール オプションに関する説明が欠落し、文の末尾に間違った文字が表示されます。 表示されるはずのドイツ語のテキストの全文を次に示します。<br/>      <br/>`Durch diese Option wird die vollständige grafische Umgebung von Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird. Sie kann hilfreich sein, wenn Sie den Windows-Desktop verwenden möchten oder über eine App verfügen, die die grafische Umgebung benötigt.` <br><br>これは、Windows Server 2019、Windows Server バージョン 1809、および Microsoft Hyper-V Server 2019 の一般公開でリリースされたドイツ語版のメディアにのみ影響します。|
| Windows Server バージョン 1809 のセットアップ時の Windows Server のブランド画像が正しくない | Windows Server バージョン 1809 のセットアップ エクスペリエンスで、初期画面の一部の背景画像に &quot;Windows Server 2019&quot; と表示されます。  Windows Server バージョン 1709 および 1803 では、これは単に &quot;Windows Server&quot; と表示される必要があります。  この製品の他の場所に影響はなく、Windows Server 2019 製品への影響もありません。  この問題は、ボリューム ライセンス サービス センターにアクセスするボリューム ラインセスをご利用のお客さまのみが利用できる Windows Server バージョン 1809 のセットアップ時に、この 1 つの画像でのみ発生します。<br/> |

### <a name="copyright"></a>著作権

このドキュメントは「現状有姿のまま」提供されます。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、ドキュメントを複製して使用することができます。

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  


1.0  
