---
title: ネットワーク シェル (Netsh) のサンプル バッチ ファイル
description: このトピックでは、Windows Server 2016 で Netsh を使用して複数のタスクを実行するバッチ ファイルを作成する方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f0cc6818b589c6ee2ac64115fe9e7fb71c3d20b1
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517907"
---
# <a name="network-shell-netsh-example-batch-file"></a>ネットワーク シェル (Netsh) のサンプル バッチ ファイル

適用先:Windows Server 2016

このトピックでは、Windows Server 2016 で Netsh を使用して複数のタスクを実行するバッチ ファイルを作成する方法について説明します。 このバッチ ファイルの例では、**netsh wins** のコンテキストが使用されています。

## <a name="example-batch-file-overview"></a>サンプル バッチ ファイルの概要

タスクを自動化するために、バッチ ファイルやその他のスクリプト内で Windows インターネット ネーム サービス \(WINS\) 用の Netsh コマンドを使用できます。 次のバッチ ファイルの例は、WINS の Netsh コマンドを使用して、さまざまな関連タスクを実行する方法を示しています。

このバッチ ファイルの例では、WINS\-A は IP アドレスが 192.168.125.30 の WINS サーバーで、WINS\-B は IP アドレスが192.168.0.189 の WINS サーバーです。

このサンプル バッチ ファイルでは次のタスクが実行されます。

- IP アドレス 192.168.0.205 を持つ動的な名前レコード MY\_RECORD \[04h\] を WINS\-A に追加します
- WINS\-B を WINS\-A のプッシュ/プル レプリケーション パートナーとして設定します
- WINS\-B に接続し、WINS\-A を WINS\-B のプッシュ/プル レプリケーション パートナーとして設定します
- WINS\-A から WINS\-B へのプッシュ レプリケーションを開始します
- WINS\-B に接続して、新しいレコード MY\_RECORD が正常にレプリケートされたことを確認します

## <a name="netsh-example-batch-file"></a>Netsh サンプル バッチ ファイル

次のバッチ ファイルの例では、コメントを含む行の先頭に、注釈を意味する "rem" が付いています。 Netsh はコメントを無視します。

```
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

rem 5. Connect to (WINS-B), and check that the record MY_RECORD [04h] was replicated successfully.
netsh wins server 192.168.0.189 show name Name=MY_RECORD EndChar=04

rem 6. End example batch file.
```

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>サンプル バッチ ファイルで使用される Netsh WINS コマンド

次のセクションでは、この手順例で使用されている **netsh wins** コマンドの一覧を示します。

- **server**: 現在の WINS コマンド ラインのコンテキストを、名前または IP アドレスで指定されたサーバーに移動します。
- **add name**: WINS サーバーに名前を登録します。
- **add partner**: WINS サーバーにレプリケーション パートナーを追加します。
- **init push**: プッシュ トリガーを開始し、WINS サーバーに送信します。
- **show name**: WINS サーバー データベース内の特定のレコードの詳細情報を表示します。

## <a name="additional-references"></a>その他の参照情報

- [ネットワーク シェル (netsh)](netsh.md)
