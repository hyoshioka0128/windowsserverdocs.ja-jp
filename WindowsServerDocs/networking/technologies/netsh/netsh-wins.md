---
title: ネットワーク シェル (Netsh) のサンプル バッチ ファイル
description: このトピックでは、Windows Server 2016 で Netsh を使用して複数のタスクを実行するバッチファイルを作成する方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86fbe66978f7c09a332bba16a27a13fa029cb5a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401919"
---
# <a name="network-shell-netsh-example-batch-file"></a>ネットワークシェル \(Netsh\) 例バッチファイル

適用対象: Windows Server 2016

このトピックでは、Windows Server 2016 で Netsh を使用して複数のタスクを実行するバッチファイルを作成する方法について説明します。 この例のバッチファイルでは、 **netsh wins**コンテキストが使用されています。

## <a name="example-batch-file-overview"></a>バッチファイルの概要の例

Windows インターネットネームサービス用の Netsh コマンドを使用して、バッチファイルやその他のスクリプトでタスクを自動化する \(WINS\) できます。 次のバッチファイルの例は、WINS の Netsh コマンドを使用して、さまざまな関連タスクを実行する方法を示しています。

このバッチファイルの例では、WINS\-は IP アドレス192.168.125.30、WINS\-B は IP アドレスが192.168.0.189 の wins サーバーです。

バッチファイルの例では、次のタスクを行います。

- IP アドレス192.168.0.205、マイ\_レコード \[04h\]を持つ動的名レコードを WINS\-に追加します。
- Wins のプッシュ/プルレプリケーションパートナーとして WINS\-B を設定し\-
- Wins\-B に接続し、wins\-を WINS\-B のプッシュ/プルレプリケーションパートナーとして設定します。
- Wins\-A から WINS\-B へのプッシュレプリケーションを開始します。
- WINS\-B に接続して、新しいレコード、マイ\_レコードが正常にレプリケートされたことを確認します。

## <a name="netsh-example-batch-file"></a>Netsh サンプルバッチファイル

次のバッチファイルの例では、コメントを含む行の前に "rem" が付いています。 Netsh はコメントを無視します。

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>サンプルバッチファイルで使用される Netsh WINS コマンド

次のセクションでは、この例の手順で使用される**netsh wins**コマンドの一覧を示します。

- **サーバー**。 現在の WINS コマンド\-行のコンテキストを、その名前または IP アドレスで指定されたサーバーにシフトします。
- **名前を追加**します。 WINS サーバーに名前を登録します。
- **パートナーを追加**します。 WINS サーバーにレプリケーションパートナーを追加します。
- **初期化プッシュ**。 プッシュトリガーを開始し、WINS サーバーに送信します。
- **名前を表示**します。 WINS サーバーデータベース内の特定のレコードの詳細情報を表示します。  

詳細については、「[ネットワークシェル (Netsh)](netsh.md)」を参照してください。
