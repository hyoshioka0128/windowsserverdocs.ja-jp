---
title: ntfrsutl
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2dd245b7d85d6d5668262d3800ab72e35b852246
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836623"
---
# <a name="ntfrsutl"></a>ntfrsutl

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

内部テーブル、スレッド、および、NT ファイル レプリケーション サービスのメモリ情報をダンプ\(NTFRS\)します。 これは、ローカルおよびリモート サーバーに対して実行します。 NTFRS サービス コントロール マネージャーでの回復設定\(SCM\)を検索し、コンピューター上の重要なログ イベントを保持することの重要なことができます。 このツールは、これらの設定を確認する便利なメソッドを提供します。   
  
## <a name="syntax"></a>構文  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|idtable|テーブルな ID|  
|configtable|FRS 構成テーブル|  
|インバウンド ログ|受信ログ|  
|アウト バウンド ログします。|出力方向のログ|  
|<computer>|コンピューターを指定します。|  
|memory|メモリ使用量|  
|スレッド||  
|ステージ||  
|ds|DS の NTFRS サービスのビューを一覧表示します。|  
|セット|アクティブなレプリカ セットを指定します|  
|version|API と NTFRS サービスのバージョンを指定します。|  
|ポーリング|現在のポーリング間隔を指定します。<br /><br />パラメーター:<br /><br /><ul><li>**\/すばやく**\[ **\=** \[ <N> \] \]\(すばやくポーリング  \)<br /><br /><ul><li>**すばやく**\-安定した構成は rectrieved までを迅速にポーリングします。</li><li>**すばやく\=** \-すばやく既定分ごとにポーリングします。</li><li>**すばやく\=** <N> \-すばやくポーリングすべて*N*分</li></ul></li><li>**\/緩やかに変化**\[ **\=** \[ <N> \] \] \(緩やかに変化をポーリング\)<br /><br /><ul><li>**緩やかに変化**\-安定した構成が取得されるまでは、緩やかに変化はポーリング</li><li>**緩やかに変化\=** \-既定の間隔でポーリング緩やかに変化</li><li>**緩やかに変化\=** <N> \-すばやくポーリングすべて*N*分</li></ul></li><li>**\/今すぐ**\(ポーリングするようになりました\)</li></ul>|  
|\/ ですか。|コマンド プロンプトにヘルプを表示します。|  
  
## <a name="BKMK_Examples"></a>例  
ファイル レプリケーションのポーリング間隔を決定します。  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
現在、NTFRS アプリケーション プログラム インターフェイスを決定する\(API\)バージョン。  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
  
  

