---
title: サブコマンドの停止-サーバー
description: サブコマンドに関するリファレンストピックでは、Windows 展開サービスサーバー上のすべてのサービスを停止します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68cc73ac016e2ffded774567034801e1c11944d1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721632"
---
# <a name="subcommand-stop-server"></a>サブコマンド: 停止サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバー上のすべてのサービスを停止します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サービスを停止するには、次のいずれかを入力します。
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[の](using-the-disable-server-command.md)
キーを使用してサーバーを無効にするコマンドを使用して、[有効](using-the-enable-server-command.md)
にするサーバーのコマンドを使用して[get](using-the-get-server-command.md)
server コマンドを使用して、[Initialize](using-the-initialize-server-command.md)
サーバーコマンドを使用して[サブ](subcommand-set-server.md)
コマンド: サーバーを設定[します](the-uninitialize-server-option.md)[。](subcommand-start-server.md)

