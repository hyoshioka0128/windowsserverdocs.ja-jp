---
title: rpcinfo
description: リモートコンピューター上のプログラムを一覧表示する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 03450a370c84eb4659b9ebfde0729fee52e6c1f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835555"
---
# <a name="rpcinfo"></a>rpcinfo

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューター上のプログラムを一覧表示します。 **Rpcinfo** コマンド ライン ユーティリティにより、リモート プロシージャが RPC サーバーにコール (RPC) を検出した内容を報告します。 

## <a name="syntax"></a>構文
```
rpcinfo [/p [<Node>]] [/b <Program version>] [/t <Node Program> [<version>]] [/u <Node Program> [<version>]]
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/p [\<ノード >]|指定したホストのポートマッパーに登録されているすべてのプログラムを一覧表示します。 ノード (コンピューター) 名を指定しない場合、プログラムは、ローカル ホスト上のポート マッパーを照会します。|
|/b \<プログラムのバージョン >|指定したプログラムとポート マッパーに登録されているバージョンを持つすべてのネットワーク ノードからの応答を要求します。 プログラムの名前または番号とバージョン番号を指定する必要があります。|
|/t \<Node Program > [\<バージョン >]|TCP トランスポート プロトコルを使用して、指定したプログラムを呼び出します。 ノード (コンピューター) 名とプログラム名を指定する必要があります。 バージョンを指定しない場合、プログラムは、すべてのバージョンを呼び出します。|
|/u \<ノードプログラム > [\<バージョン >]|UDP トランスポート プロトコルを使用して、指定したプログラムを呼び出します。 ノード (コンピューター) 名とプログラム名を指定する必要があります。 バージョンを指定しない場合、プログラムは、すべてのバージョンを呼び出します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name="BKMK_Examples"></a>例
ポート マッパーに登録されているすべてのプログラムの一覧を次のように入力します。
```
rpcinfo /p [<Node>]
```
指定したプログラムのネットワーク ノードの応答を要求する次のように入力します。
```
rpcinfo /b <Program version>
```
伝送制御プロトコル (TCP) を使用して、プログラムを呼び出す、次のように入力します。
```
rpcinfo /t <Node Program> [<version>]
```
プログラムを呼び出すには、ユーザー データグラム プロトコル (UDP) を使用します。
```
rpcinfo /u <Node Program> [<version>]
```

## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
