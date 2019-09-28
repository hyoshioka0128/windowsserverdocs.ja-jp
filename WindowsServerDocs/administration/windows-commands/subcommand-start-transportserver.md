---
title: サブコマンドの開始 TransportServer
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c1bdf80aa9c255e12e1e4821467d556eb67f8691
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370733"
---
# <a name="subcommand-start-transportserver"></a>サブコマンド: 開始 TransportServer

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポートサーバーのすべてのサービスを開始します。
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
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[TransportServer 無効にするコマンドを使用して](using-the-disable-transportserver-command.md)
[TransportServer 有効にするコマンドを使用して](using-the-enable-transportserver-command.md)
[get TransportServer コマンドを使用して](using-the-get-transportserver-command.md)
[サブコマンド: Set-transportserver](subcommand-set-transportserver.md)
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
