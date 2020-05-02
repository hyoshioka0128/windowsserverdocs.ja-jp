---
title: ntfrsutl
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 698237380d02fb1ceb4e738c6fb4f083dd31aef3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723464"
---
# <a name="ntfrsutl"></a>ntfrsutl

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

NT ファイルレプリケーションサービス\(の NTFRS\)の内部テーブル、スレッド、およびメモリの情報をダンプします。 ローカルサーバーとリモートサーバーに対して実行されます。 サービスコントロールマネージャー \(SCM\)での NTFRS の回復設定によって、コンピューター上の重要なログイベントを特定して維持することが重要になる場合があります。 このツールを使用すると、これらの設定を簡単に確認できます。   
  
## <a name="syntax"></a>構文  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                                                                                                                                                                                                                                        [説明]                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   idtable   |                                                                                                                                                                                                                                                                                                                                          ID テーブル                                                                                                                                                                                                                                                                                                                                          |
| configtable |                                                                                                                                                                                                                                                                                                                                  FRS 構成テーブル                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        受信ログ                                                                                                                                                                                                                                                                                                                                         |
|   outlog    |                                                                                                                                                                                                                                                                                                                                        送信ログ                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  コンピューターを指定します。                                                                                                                                                                                                                                                                                                                                   |
|   memory    |                                                                                                                                                                                                                                                                                                                                        メモリ使用量                                                                                                                                                                                                                                                                                                                                        |
|   スレッド   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    準備    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     ds      |                                                                                                                                                                                                                                                                                                                         NTFRS サービスの DS のビューを一覧表示します。                                                                                                                                                                                                                                                                                                                          |
|    セット     |                                                                                                                                                                                                                                                                                                                             アクティブなレプリカセットを指定します                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       API と NTFRS サービスのバージョンを指定します。                                                                                                                                                                                                                                                                                                                        |
|    投票     | 現在のポーリング間隔を指定します。<p>パラメーター:<p><ul><li>**\/迅速なポーリング**\[ **\=** \[ <N> \] \] \(  \)<p><ul><li>安定した構成が rectrieved**まで迅速に迅速にポーリング** \-</li><li>既定の分ごとに\-すばやくポーリングを行います。 **\= **</li><li>**N\=分**ごとに*N*すばやく\-ポーリングを行う<N></li></ul></li><li>**\/緩やかにポーリングする**\[ **\=** \[ <N> \] \] \(\)<p><ul><li>安定した構成が取得されるまで、**ゆっくり** \-ポーリングします。</li><li>既定の分数ごと\-に低速でポーリングする**\= **</li><li>**N\=分**ごとに迅速にポーリング*N* \- <N></li></ul></li><li>** \/今すぐポーリング** \(\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                                                                                                                                            |
  
## <a name="examples"></a>例  
ファイルレプリケーションのポーリング間隔を確認するには、次のようにします。  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
現在の NTFRS アプリケーションプログラムインターフェイス\(の API\)バージョンを確認するには、次のようにします。  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
  
  

