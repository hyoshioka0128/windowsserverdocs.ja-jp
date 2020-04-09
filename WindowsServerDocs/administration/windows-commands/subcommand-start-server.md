---
title: サブコマンドの開始-サーバー
description: Windows コマンドに関するトピックの「start-Server」を参照してください。これにより、Windows 展開サービスサーバーのすべてのサービスが開始されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc3e0d11348dd6b531671e62139f2ce2c884c5ee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833745"
---
# <a name="subcommand-start-server"></a>サブコマンド: 開始サーバー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバーのすべてのサービスを開始します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|起動するサーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
サーバーを起動するには、次のいずれかを入力します。
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[、無効にするサーバーのコマンドを使用して](using-the-disable-server-command.md)
[、有効にするサーバーのコマンドを使用して](using-the-enable-server-command.md)
[get サーバー コマンドを使用して](using-the-get-server-command.md)
[Initialize サーバー コマンドを使用して](using-the-initialize-server-command.md)
[サブコマンド: サーバーを設定する](subcommand-set-server.md)
[サブコマンド: サーバーの停止](subcommand-stop-server.md)
[非サーバー オプション](the-uninitialize-server-option.md)
