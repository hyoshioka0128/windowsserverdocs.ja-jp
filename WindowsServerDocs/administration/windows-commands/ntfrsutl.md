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

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

NT ファイルレプリケーションサービスの内部テーブル、スレッド、およびメモリの情報をダンプします。 @no__t は、0NTFRS @ no__t-1 です。 ローカルサーバーとリモートサーバーに対して実行されます。 サービスコントロールマネージャーの NTFRS の回復設定 \(SCM @ no__t-1 を使用すると、コンピューター上の重要なログイベントを特定して維持することが重要になります。 このツールを使用すると、これらの設定を簡単に確認できます。   
  
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
|    投票     | 現在のポーリング間隔を指定します。<br /><br />パラメーター:<br /><br /><ul><li>**\/quickly** **\=** \[ <N> @ no__t @ no__t-8 @ no__t-9polls を迅速に @ no__t-10<br /><br /><ul><li>安定した構成が rectrieved になる**まで迅速に @no__t-** 1</li><li>**すぐに @ no__t-1** \- は既定の分ごとにポーリングを行います。</li><li>**すばやく @ no__t-1**<N> @no__t 3 回、 *N*分ごとにポーリングを行います。</li></ul></li><li>**\/slowly**\[ **\=** \[ <N> @ no__t @ no__t-8 \(polls が遅い @ no__t-10<br /><br /><ul><li>安定した \- は安定した構成が取得される**までゆっくりと**ポーリングします</li><li>**ゆっくり @ no__t-1** \- ポーリングが既定の分数ごとに遅くなる</li><li>**ゆっくり @ no__t-1**<N> @no__t、 *N*分ごとに迅速にポーリング</li></ul></li><li>**\/now** \(polls @ no__t-3</li></ul> |
|     \/ ですか。     |                                                                                                                                                                                                                                                                                                                            コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                                                                                                                                            |
  
## <a name="BKMK_Examples"></a>例  
ファイルレプリケーションのポーリング間隔を確認するには、次のようにします。  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
現在の NTFRS アプリケーションプログラムのインターフェイスを特定するには \(API @ no__t のバージョン:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
  
  

