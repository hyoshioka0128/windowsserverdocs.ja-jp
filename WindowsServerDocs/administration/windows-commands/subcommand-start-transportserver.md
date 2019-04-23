---
title: サブコマンド開始 TransportServer
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5fdfea020019a45eceac0142160f9d5d4d97b989
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848633"
---
# <a name="subcommand-start-transportserver"></a>サブコマンド: 開始 TransportServer

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを開始します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="BKMK_examples"></a>例
サーバーを起動するには、次のいずれかを入力します。
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[TransportServer 無効にするコマンドを使用して](using-the-disable-transportserver-command.md)
[TransportServer 有効にするコマンドを使用して](using-the-enable-transportserver-command.md)
[get TransportServer コマンドを使用して](using-the-get-transportserver-command.md)
[サブコマンド: Set-transportserver](subcommand-set-transportserver.md)
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
