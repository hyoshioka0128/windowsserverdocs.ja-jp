---
title: 有効にするサーバーのコマンドを使用します。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b90621ec14c6cf451d7a05eace79f2e0679b2f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363455"
---
# <a name="using-the-enable-server-command"></a>有効にするサーバーのコマンドを使用します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービスのすべてのサービスを有効にします。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="BKMK_examples"></a>例
サーバー上のサービスを有効にするには、次のいずれかを実行します。
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[、無効にするサーバーのコマンドを使用して](using-the-disable-server-command.md)
[get サーバー コマンドを使用して](using-the-get-server-command.md)
[Initialize サーバー コマンドを使用して](using-the-initialize-server-command.md)
[サブコマンド: サーバーを設定する](subcommand-set-server.md)
[サブコマンド: サーバーを起動](subcommand-start-server.md)
[サブコマンド: サーバーの停止](subcommand-stop-server.md)
[非サーバー オプション](the-uninitialize-server-option.md)
