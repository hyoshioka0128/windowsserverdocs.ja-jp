---
title: サブコマンドの開始 TransportServer
description: サブコマンドのリファレンストピックで、トランスポートサーバーのすべてのサービスを開始する TransportServer を開始します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 92bd68421883c49ec29dfb78f06121bff880b01e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721642"
---
# <a name="subcommand-start-transportserver"></a>サブコマンド: 開始 TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを開始します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サーバーを起動するには、次のいずれかを入力します。
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[のキー無効 transportserver コマンド](using-the-disable-transportserver-command.md)
を使用して[有効](using-the-enable-transportserver-command.md)
にする transportserver コマンドを使用して[get](using-the-get-transportserver-command.md)
transportserver コマンドを使用して[サブコマンド: set](subcommand-set-transportserver.md)
transportserver[サブコマンド: 停止 transportserver](subcommand-stop-transportserver.md)
