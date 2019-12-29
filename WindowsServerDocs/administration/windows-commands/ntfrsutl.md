---
title: ntfrsutl
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f1301b6876698e9eb552ae0ef9e70ed278319a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372625"
---
# <a name="ntfrsutl"></a>ntfrsutl

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

NT ファイルレプリケーションサービスの内部テーブル、スレッド、およびメモリ情報を \(NTFRS\)にダンプします。 ローカルサーバーとリモートサーバーに対して実行されます。 サービスコントロールマネージャー \(SCM\) での NTFRS の回復設定は、コンピューター上の重要なログイベントを特定して維持するために重要な場合があります。 このツールを使用すると、これらの設定を簡単に確認できます。   
  
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
  
|  パラメーター  |                                                                                                                                                                                                                                                                                                                                        説明                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   idtable   |                                                                                                                                                                                                                                                                                                                                          ID テーブル                                                                                                                                                                                                                                                                                                                                          |
| configtable |                                                                                                                                                                                                                                                                                                                                  FRS 構成テーブル                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        受信ログ                                                                                                                                                                                                                                                                                                                                         |
|   outlog    |                                                                                                                                                                                                                                                                                                                                        送信ログ                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  コンピューターを指定します。                                                                                                                                                                                                                                                                                                                                   |
|   memory    |                                                                                                                                                                                                                                                                                                                                        メモリ使用量                                                                                                                                                                                                                                                                                                                                        |
|   レッド   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    stage    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     Ds      |                                                                                                                                                                                                                                                                                                                         NTFRS サービスの DS のビューを一覧表示します。                                                                                                                                                                                                                                                                                                                          |
|    組     |                                                                                                                                                                                                                                                                                                                             アクティブなレプリカセットを指定します                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       API と NTFRS サービスのバージョンを指定します。                                                                                                                                                                                                                                                                                                                        |
|    投票     | 現在のポーリング間隔を指定します。<br /><br />パラメーター:<br /><br /><ul><li>**\=** \[ <N>\]\]をすばやく\[ **\/** 、\(ポーリングを迅速に\)<br /><br /><ul><li>安定した構成が rectrieved になる**まで迅速にポーリング \-**</li><li>既定の分ごとに迅速に **\=** \- ポーリングできます。</li><li>*N*分ごとに迅速に **\=** <N> \- ポーリング</li></ul></li><li>**\/速度が遅い**\[ **\=** \[ <N>\]\] \(ポーリングに時間がかかる\)<br /><br /><ul><li>安定した構成が取得されるまで、**緩やか**な \- ポーリングを行う</li><li>**低速\=** \- ポーリングが既定の分数ごとに遅くなる</li><li>**速度が遅い\=** <N> \- ポーリングを*N*分ごとに迅速に行う</li></ul></li><li>今すぐポーリングを \( **\/** \)</li></ul> |
|     \/ ですか。     |                                                                                                                                                                                                                                                                                                                            コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                                                                                                                                            |
  
## <a name="BKMK_Examples"></a>例  
ファイルレプリケーションのポーリング間隔を確認するには、次のようにします。  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
現在の NTFRS アプリケーションプログラムインターフェイス \(API\) バージョンを確認するには、次のようにします。  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
  
  

