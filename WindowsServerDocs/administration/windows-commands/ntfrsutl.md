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
ms.openlocfilehash: dc1275b7936a88b14b7658e2fe27d3958a035a04
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820928"
---
# <a name="ntfrsutl"></a>ntfrsutl

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

NT ファイルレプリケーションサービスの NTFRS の内部テーブル、スレッド、およびメモリの情報をダンプし \( \) ます。 ローカルサーバーとリモートサーバーに対して実行されます。 サービスコントロールマネージャー SCM での NTFRS の回復設定によって、 \( \) コンピューター上の重要なログイベントを特定して維持することが重要になる場合があります。 このツールを使用すると、これらの設定を簡単に確認できます。

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

|  パラメーター  |                                                                                                                                                                                                                                                                                                                                        説明                                                                                                                                                                                                                                                                                                                                         |
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
|    投票     | 現在のポーリング間隔を指定します。<p>パラメーター:<p><ul><li>** \/ すばやく** \[ **\=** \[<N>\]\]\(迅速なポーリング  \)<p><ul><li>**すばやく** \-安定した構成が rectrieved まで迅速にポーリング</li><li>**すばやく \= **\-既定の分ごとにポーリングを迅速に行います。</li><li>**すばやく \= ** <N>\- *N*分ごとに迅速にポーリング</li></ul></li><li>** \/ ゆっくり** \[ **\=** \[<N>\]\]\(ポーリング速度が遅い\)<p><ul><li>**ゆっくり** \-安定した構成が取得されるまで、ポーリングが遅くなります。</li><li>**ゆっくり \= **\-既定の分数ごとにポーリングが遅くなります</li><li>**ゆっくり \= ** <N>\- *N*分ごとに迅速にポーリング</li></ul></li><li>** \/ ここで** \(今すぐポーリング\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                                                                                                                                                            |

## <a name="examples"></a>例
ファイルレプリケーションのポーリング間隔を確認するには、次のようにします。

```
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1
```

現在の NTFRS アプリケーションプログラムインターフェイスの API バージョンを確認するには、次のようにし \( \) ます。

```
C:\Program Files\SupportTools>ntfrsutl version
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)




