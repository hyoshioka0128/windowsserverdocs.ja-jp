---
title: 初期化解除-サーバー
description: 初期サーバー構成中にサーバーに加えられた変更を元に戻すサーバーの初期化解除に関するリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d7747a44172b7382bd22a7d48ccc717a89ccacb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721394"
---
# <a name="uninitialize-server"></a>初期化解除-サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーの初期構成中に、サーバーに加えられた変更を元に戻します。 これには、**サーバー**オプションまたは Windows 展開サービス mmc スナップインのいずれかによって行われた変更が含まれます。 このコマンドは、サーバーを未構成の状態にリセットしていることに注意してください。 このコマンドでは、remoteInstall 共有フォルダーの内容は変更されません。 代わりに、サーバーを再初期化できるように、サーバーの状態をリセットします。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サーバーを再初期化するには、次のいずれかを入力します。
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[の](using-the-disable-server-command.md)
キーを使用してサーバーを無効にするコマンドを使用して、[有効](using-the-enable-server-command.md)
にするサーバーのコマンドを使用して[get](using-the-get-server-command.md)
server コマンドを使用して、[Initialize](using-the-initialize-server-command.md)
サーバーコマンドを使用してサブコマンド: サーバーを[設定](subcommand-set-server.md)
するサブコマンド: サーバーの[起動](subcommand-start-server.md)
サブコマンド:[サーバーの停止](subcommand-stop-server.md)
