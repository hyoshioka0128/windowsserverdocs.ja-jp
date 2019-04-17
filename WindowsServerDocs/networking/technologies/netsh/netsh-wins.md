---
title: ネットワーク シェル (Netsh) バッチ ファイルの例
description: このトピックを使用すると、Windows Server 2016 では、Netsh を使用して複数のタスクを実行するバッチ ファイルを作成するのに方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh-example-batch-file"></a>ネットワーク シェル \(Netsh\) バッチ ファイルの例

Windows Server 2016 の適用対象:

このトピックを使用すると、Windows Server 2016 では、Netsh を使用して複数のタスクを実行するバッチ ファイルを作成するのに方法について説明します。 この例のバッチ ファイルで、**netsh wins**コンテキストを使用します。

## <a name="example-batch-file-overview"></a>バッチ ファイルの例の概要

タスクを自動化するのにバッチ ファイルでの Windows インターネット ネーム サービス \(WINS\) 用の Netsh コマンドとその他のスクリプトを使用することができます。 バッチ ファイルの次の例では、WINS 用の Netsh コマンドを使用して、さまざまな関連するタスクを実行する方法について説明します。

この例のバッチ ファイルで WINS\ A は 192.168.125.30 IP アドレスを持つ WINS サーバーで、WINS\ B は 192.168.0.189 IP アドレスを持つ WINS サーバーです。

バッチ ファイルの例では、次のタスクが実現しています。

- 追加すると、動的な名前 192.168.0.205 の IP アドレス レコードの MY\_RECORD \[04h\]、WINS\ に
- WINS\ A のプッシュまたはプル レプリケーション パートナーとして WINS\ B の設定します。
- で WINS\ B に接続し、設定 WINS\ に WINS\ B のプッシュまたはプル レプリケーション パートナーとしては、
- WINS\ A から WINS\ B へのプッシュ レプリケーションを開始します。
- WINS\-b MY\_RECORD、新しいレコードが正常にレプリケートされていることを確認するには接続します。

## <a name="netsh-example-batch-file"></a>Netsh バッチ ファイルの例

次のサンプル バッチ ファイルのコメントが含まれている行が付きます"rem、"の注釈。 Netsh では、コメントを無視します。

    rem: Begin example batch file.
    
    rem two WINS servers:
    
    rem (WINS-A) 192.168.125.30
    
    rem (WINS-B) 192.168.0.189
    
    rem 1. Connect to (WINS-A), and add the dynamic name MY\_RECORD \[04h\] to the (WINS-A) database.
    
    netsh wins server 192.168.125.30 add name Name=MY\_RECORD EndChar=04 IP={192.168.0.205}
    
    rem 2. Connect to (WINS-A), and set (WINS-B) as a push/pull replication partner of (WINS-A).
    
    netsh wins server 192.168.125.30 add partner Server=192.168.0.189 Type=2
    
    rem 3. Connect to (WINS-B), and set (WINS-A) as a push/pull replication partner of (WINS-B).
    
    netsh wins server 192.168.0.189 add partner Server=192.168.125.30 Type=2
    
    rem 4. Connect back to (WINS-A), and initiate a push replication to (WINS-B).
    
    netsh wins server 192.168.125.30 init push Server=192.168.0.189 PropReq=0
    
    rem 5. Connect to (WINS-B), and check that the record MY\_RECORD \[04h\] was replicated successfully.
    
    netsh wins server 192.168.0.189 show name Name=MY\_RECORD EndChar=04
    
    rem 6. End example batch file.

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>WINS コマンドをバッチ ファイルの例で使用されます。

次のセクションのリスト、**netsh wins**この例の手順で使用されるコマンドです。

- **サーバー**します。 現在の WINS コマンド ライン コンテキストを名前または IP アドレスで指定されたサーバーに移動します。
- **名前を追加**します。 WINS サーバーの名前を登録します。
- **パートナーを追加する**します。 WINS サーバー上のレプリケーション パートナーを追加します。
- **init プッシュ**します。 開始し、WINS サーバーにプッシュ トリガーを送信します。
- **名前を表示する**します。 WINS サーバーのデータベースの特定のレコードの詳細情報を表示します。  

詳細については、次を参照してください。[ネットワーク シェル (Netsh)](netsh.md)します。
