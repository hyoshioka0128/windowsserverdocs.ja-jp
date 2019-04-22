---
title: リリース ノート - Windows Server 2019 に関する重要な問題
description: クラッシュ、ハング、インストールの障害およびデータの損失を回避するために回避策を必要とする重要な問題をまとめたものです。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: d5d84bb1cd204a5419271cc3668343f8ac9c9a54
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824523"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>リリース ノート - Windows Server 2019 に関する重要な問題

>適用先:Windows Server 2019

これらのリリース ノートは、Windows Server で最も重要な問題を要約&reg;2019年オペレーティング システム、既知の場合の回避や、問題を回避する方法を含むです。 設計による変更、新機能、および今回のリリースで修正プログラムについては、次を参照してください。[で Windows Server 2019 新](whats-new-19.md)と特定の機能チームからのお知らせします。 指定しない場合、報告された各問題はすべてのエディションおよび Windows Server 2019 のインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  
  
## <a name="release-notes"></a>リリース ノート
次の既知の問題は、Windows Server 2019 表示されます。 
<table border="1" rules="rows">
  <thead align="left" valign="middle">
    <tr>
      <th>タイトル</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody align="left" valign="middle">
    <tr>
      <td>サーバーのセットアップ中にインストール オプション メニューには、ドイツ語のテキストが切り捨てられて</td>
      <td>デスクトップ エクスペリエンスのインストール オプションの説明が最後に、不足していると正しくない文字をある「をインストールするオペレーティング システムの選択」という、オペレーティング システムの選択ウィンドウで、ドイツ語サーバーのメディアからセットアップを実行する場合文。 完全なドイツ語のテキストがここで表示されるはずです。  
      <br/>
      <p><i>Durch diese オプション wird サイコロ vollständige grafische Umgebung von Windows installiert、wodurch zusätzlicher Speicherplatz verbraucht wird します。Sie kann hilfreich sein、wenn Sie den Windows デスクトップ verwenden möchten 並べ替えた über eine アプリ verfügen、サイコロ grafische Umgebung benötigt を終了します。</i> </p>
      <p>これには、パブリックの可用性の Windows Server 2019、Windows Server、バージョンは 1809、および Microsoft HYPER-V Server 2019 では、リリース、ドイツ語のメディアのみに影響します。</p></td>
    </tr>
    <tr>
      <td>Windows Server のブランド化イメージが Windows Server バージョンは 1809 のセットアップ時に正しくないです。  </td>
      <td>Windows Server バージョンは 1809 のセットアップ エクスペリエンス中には、一部の初期画面の背景画像は、"Windows Server 2019"を示します。  Windows server、バージョン 1709 および 1803、この必要がありますだけと"Windows Server"します。  その他の製品にその他の場所への影響がないと、Windows Server 2019 製品への影響はありません。  問題は、Windows Server バージョンは 1809、ボリューム ライセンスのお客様が、ボリューム ライセンス サービス センターへのアクセスにのみ使用できますのセットアップ時にこの 1 つのイメージに制限されます。  
      </td>
    </tr>
  </tbody>
</table>


### <a name="copyright"></a>著作権  
このドキュメントは「現状有姿のまま」提供されます。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、ドキュメントを複製して使用することができます。  

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  


1.0  
