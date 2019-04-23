---
title: ネットワーク シェル (Netsh) のサンプル バッチ ファイル
description: このトピックを使用すると、Windows Server 2016 で Netsh を使用して複数のタスクを実行するバッチ ファイルを作成するのに方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880173"
---
# <a name="network-shell-netsh-example-batch-file"></a>ネットワーク シェル\(Netsh\)バッチ ファイルの例

適用先:Windows Server 2016

このトピックを使用すると、Windows Server 2016 で Netsh を使用して、複数のタスクを実行するバッチ ファイルを作成するのに方法について説明します。 この例のバッチ ファイルで、 **netsh wins**コンテキストが使用されます。

## <a name="example-batch-file-overview"></a>バッチ ファイルの例の概要

Windows インターネット ネーム サービス用の Netsh コマンドを使用する\(WINS\)でバッチ ファイルやその他のスクリプト タスクを自動化します。 次のバッチ ファイルの例では、WINS の Netsh コマンドを使用して、さまざまな関連タスクを実行する方法を示します。

この例のバッチ ファイルで WINS\-A は、IP アドレス 192.168.125.30 と WINS の WINS サーバー\-B が 192.168.0.189 IP アドレスを持つ WINS サーバー。

バッチ ファイルの例では、次のタスクを実現します。

- 動的な名前レコードを追加で IP アドレス、192.168.0.205 MY\_レコード\[04 h\]、WINS に\-A
- WINS 設定\-WINS のプッシュ/プル レプリケーション パートナーとして B\-A
- WINS に接続する\-B、および、セットの WINS\-WINS のプッシュ/プル レプリケーション パートナーとして A\-B
- WINS からプッシュ レプリケーションを開始します\-wins A\-B
- WINS に接続する\-B ことを確認する新しいレコード、MY\_レコードが正常にレプリケートされました。

## <a name="netsh-example-batch-file"></a>Netsh バッチ ファイルの例

次の例のバッチ ファイルでコメントを含む行が"rem、"で注釈の前します。 Netsh では、コメントは無視されます。

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>バッチ ファイルの例で使用される、Netsh WINS コマンド

次のセクションの一覧、 **netsh wins**この例の手順で使用されるコマンド。

- **server**します。 現在の WINS コマンドをシフト\-行コンテキスト、名前または IP アドレスで指定されたサーバーにします。
- **名前を追加**します。 WINS サーバーの名前を登録します。
- **パートナーを追加する**します。 WINS サーバーのレプリケーション パートナーを追加します。
- **init プッシュ**します。 開始し、プッシュ トリガーを WINS サーバーに送信します。
- **名前を表示する**します。 WINS サーバー データベースの特定のレコードの詳細な情報を表示します。  

詳細については、次を参照してください。[ネットワーク シェル (Netsh)](netsh.md)します。
