---
title: サブコマンドの開始-サーバー
description: サブコマンドのリファレンストピックで、Windows 展開サービスサーバーのすべてのサービスを開始します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2a6de007e62bf3be5544f97b53a4fcc13118985
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721654"
---
# <a name="subcommand-start-server"></a>サブコマンド: 開始サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバーのすべてのサービスを開始します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|起動するサーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サーバーを起動するには、次のいずれかを入力します。
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[の](using-the-disable-server-command.md)
キーを使用してサーバーを無効にするコマンドを使用して、[有効](using-the-enable-server-command.md)
にするサーバーのコマンドを使用して[get](using-the-get-server-command.md)
server コマンドを使用して、[Initialize](using-the-initialize-server-command.md)
サーバーコマンドを使用してサブコマンド: サーバーを[設定](subcommand-set-server.md)
するサブコマンド: サーバーの[停止](subcommand-stop-server.md)
サーバー[オプション](the-uninitialize-server-option.md)
