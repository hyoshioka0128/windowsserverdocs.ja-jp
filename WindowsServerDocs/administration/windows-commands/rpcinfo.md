---
title: rpcinfo
description: リモート コンピューター上のプログラムを一覧表示する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 4aba1e57d5a61103310fbe7abcac391e543be5aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826373"
---
# <a name="rpcinfo"></a>rpcinfo

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューター上のプログラムを一覧表示します。 **Rpcinfo** コマンド ライン ユーティリティにより、リモート プロシージャが RPC サーバーにコール (RPC) を検出した内容を報告します。 

## <a name="syntax"></a>構文
```
rpcinfo [/p [<Node>]] [/b <Program version>] [/t <Node Program> [<version>]] [/u <Node Program> [<version>]]
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/p [\<ノード >]|指定したホスト上のポート マッパーに登録されているすべてのプログラムを一覧表示します。 ノード (コンピューター) 名を指定しない場合、プログラムは、ローカル ホスト上のポート マッパーを照会します。|
|/b\<プログラムのバージョン >|指定したプログラムとポート マッパーに登録されているバージョンを持つすべてのネットワーク ノードからの応答を要求します。 プログラムの名前または番号とバージョン番号を指定する必要があります。|
|/t\<ノード プログラム > [\<バージョン >]|TCP トランスポート プロトコルを使用して、指定したプログラムを呼び出します。 ノード (コンピューター) 名とプログラム名を指定する必要があります。 バージョンを指定しない場合、プログラムは、すべてのバージョンを呼び出します。|
|/u\<ノード プログラム > [\<バージョン >]|UDP トランスポート プロトコルを使用して、指定したプログラムを呼び出します。 ノード (コンピューター) 名とプログラム名を指定する必要があります。 バージョンを指定しない場合、プログラムは、すべてのバージョンを呼び出します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_Examples"></a>例
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
-   [コマンドライン構文キー](command-line-syntax-key.md)
