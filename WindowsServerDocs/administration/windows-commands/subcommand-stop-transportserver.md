---
title: サブコマンドの停止 TransportServer
description: 停止 TransportServer のリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4321ec991b2c20911f992e4c3c38e5c9cfa5f165
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721621"
---
# <a name="subcommand-stop-transportserver"></a>サブコマンド: 停止 TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバー上のすべてのサービスを停止します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 トランスポート サーバーが指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a><a name="BKMK_examples"></a>例
サービスを停止するには、次のいずれかを入力します。
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[無効 transportserver コマンド](using-the-disable-transportserver-command.md)
を使用して[有効](using-the-enable-transportserver-command.md)
にする transportserver コマンドを使用して[get](using-the-get-transportserver-command.md)
transportserver コマンドを使用して[サブコマンド: set transportserver](subcommand-set-transportserver.md)
[サブコマンド: 開始 transportserver](subcommand-start-transportserver.md)
