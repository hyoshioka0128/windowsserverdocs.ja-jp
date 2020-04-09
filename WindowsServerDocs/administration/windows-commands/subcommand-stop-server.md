---
title: サブコマンドの停止-サーバー
description: Windows コマンドに関するトピックでは、サブコマンドを停止します。これにより、Windows 展開サービスサーバー上のすべてのサービスが停止されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2671e7a2c2e5bb542cecd9374ad6364d68ff5bd4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833715"
---
# <a name="subcommand-stop-server"></a>サブコマンド: 停止サーバー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバー上のすべてのサービスを停止します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
サービスを停止するには、次のいずれかを入力します。
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[、無効にするサーバーのコマンドを使用して](using-the-disable-server-command.md)
[、有効にするサーバーのコマンドを使用して](using-the-enable-server-command.md)
[get サーバー コマンドを使用して](using-the-get-server-command.md)
[Initialize サーバー コマンドを使用して](using-the-initialize-server-command.md)
[サブコマンド: サーバーを設定する](subcommand-set-server.md)
[サブコマンド: サーバーを起動](subcommand-start-server.md)
[非サーバー オプション](the-uninitialize-server-option.md)
