---
title: 'リリース ノート: Windows Server 2019 に関する重要な問題'
description: クラッシュ、ハング、インストールの失敗とデータの損失を回避するために回避策を必要とする重大な問題をまとめたものです。
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
ms.sourcegitcommit: dbb4738fdac3b7911952ff11f1eaed9649d6567a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "9149892"
---
# リリース ノート: Windows Server 2019 に関する重要な問題

>適用対象: Windows Server 2019

これらのリリース ノートは、Windows server の最も重大な問題を要約&reg;がわかっている場合に、しないか、または、問題を回避する方法を含めて、2019年オペレーティング システム。 仕様変更、新機能は、このリリースで修正プログラムについては、 [Windows Server 2019 の新機能については](whats-new-19.md)特定の機能チームからのお知らせを参照してください。 これを指定しない限り、すべてのエディションおよび Windows Server 2019 のインストール オプションに報告された問題はそれぞれが適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  
  
## リリース ノート
Windows Server 2019 で次の既知の問題が存在します。 
<table border="1" rules="rows">
  <thead align="left" valign="middle">
    <tr>
      <th>タイトル</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody align="left" valign="middle">
    <tr>
      <td>サーバーのセットアップ中にインストール オプション メニューには、ドイツ語のテキストが切り詰められています。</td>
      <td>デスクトップ エクスペリエンス インストール オプションの説明が不足していると、不適切な文字を最後にある必要が「、インストールするオペレーティング システムの選択」というタイトル、オペレーティング システムの選択ウィンドウで、ドイツ語のサーバー メディアからセットアップを実行するとき文します。 表示する必要があります、完全にドイツ語のテキストを次に示します。  
      <br/>
      <p><i>Durch diese オプション wird ダイス vollständige grafische Umgebung が Windows installiert、wodurch zusätzlicher Speicherplatz verbraucht wird します。 Sie kann hilfreich sein、wenn Sie den Windows デスクトップ verwenden möchten 並べ替えた über eine アプリ verfügen、ダイス grafische Umgebung benötigt を終了します。</i> </p>
      <p>これは、パブリック可用性の Windows Server 2019、Windows Server version 1809、および Microsoft HYPER-V Server 2019 でリリースされるドイツ語のメディアのみ影響します。</p></td>
    </tr>
    <tr>
      <td>Windows Server ブランドの画像が Windows Server version 1809 のセットアップ中に正しくないです。  </td>
      <td>Windows Server version 1809 のセットアップ エクスペリエンス中には、一部の初期画面の背景画像は、"Windows Server 2019"を示します。  として Windows Server バージョン 1709 および 1803、このする必要がありますだけと答えます"Windows Server"。  その他の製品でその他の場所への影響がないと、Windows Server 2019 の製品への影響はありません。  この問題は、Windows Server version 1809 では、ボリューム ライセンスのお客様が、ボリューム ライセンス サービス センターへのアクセスにのみ利用可能なのセットアップ中にこの 1 つのイメージに限定されます。  
      </td>
    </tr>
  </tbody>
</table>


### 著作権  
このドキュメントは「現状有姿のまま」提供されます。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、このドキュメントを複製して使用することができます。  

&copy;2019 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  


1.0  
