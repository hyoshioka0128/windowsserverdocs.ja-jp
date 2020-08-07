---
title: ntfrsutl
description: Ntfrsutl コマンドの参照記事。これにより、NT ファイルレプリケーションサービス (NTFRS) の内部テーブル、スレッド、およびメモリ情報がダンプされます。
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2676e4cc4d920d766f9cc122f127d3d5e8c9548a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885293"
---
# <a name="ntfrsutl"></a>ntfrsutl

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルサーバーとリモートサーバーの両方から、NT ファイルレプリケーションサービス (NTFRS) の内部テーブル、スレッド、およびメモリ情報をダンプします。 サービスコントロールマネージャー (SCM) での NTFRS の回復設定は、コンピューター上の重要なログイベントを特定して維持するために重要な場合があります。 このツールを使用すると、これらの設定を簡単に確認できます。

## <a name="syntax"></a>構文

```
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]
ntfrsutl[memory|threads|stage][<computer>]
ntfrsutl ds[<computer>]
ntfrsutl [sets][<computer>]
ntfrsutl [version][<computer>]
ntfrsutl poll[/quickly[=[<n>]]][/slowly[=[<n>]]][/now][<computer>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| idtable | ID テーブルを指定します。 |
| configtable | FRS 構成テーブルを指定します。 |
| inlog | 受信ログを指定します。 |
| outlog | 送信ログを指定します。 |
| `<computer>` | コンピューターを指定します。 |
| メモリ | メモリ使用量を指定します。 |
| スレッド | メモリ使用量を指定します。 |
| 準備 | メモリ使用量を指定します。 |
| ds | NTFRS サービスの DS のビューを一覧表示します。 |
| セット | アクティブなレプリカセットを指定します。 |
| version | API と NTFRS サービスのバージョンを指定します。 |
| 投票 | 現在のポーリング間隔を指定します。<ul><li>`/quickly`-安定した構成を取得するまで迅速にポーリングします。</li><li>`/quickly=`-既定の分単位の間隔でポーリングを迅速に行います。</li><li>`/quickly=<n>`- *N*分ごとにポーリングを迅速に行います。</li><li>`/slowly`-安定した構成を取得するまで、ポーリング速度が低下します。</li><li>`/slowly=`-既定の分数 (分単位) ごとにポーリングが遅くなります。</li><li>`/slowly=<n>`- *N*分ごとにポーリングが遅くなります。</li><li>`/now`-今すぐポーリング。</li></ul>|
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

ファイルレプリケーションのポーリング間隔を決定するには、次のように入力します。

```
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1
```

現在の NTFRS アプリケーションプログラムインターフェイス (API) のバージョンを確認するには、次のように入力します。

```
C:\Program Files\SupportTools>ntfrsutl version
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
