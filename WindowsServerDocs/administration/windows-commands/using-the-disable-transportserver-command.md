---
title: 無効にする-TransportServer
description: トランスポートサーバーのすべてのサービスを無効にする、無効にする TransportServer のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81ae150b4f8e4de577e377a2d10a7a69675adac7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720965"
---
# <a name="disable-transportserver"></a>無効にする-TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを無効にします。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|無効にするトランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 トランスポート サーバーの名前が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サーバーを無効にするには、次のように入力します。
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
を使用し[て有効にする transportserver コマンド](using-the-enable-transportserver-command.md)
を使用して[get transportserver コマンド](using-the-get-transportserver-command.md)
を使用してサブコマンド:[set transportserver](subcommand-set-transportserver.md)
サブコマンド:[開始](subcommand-start-transportserver.md)
transportserver サブコマンド:[停止 transportserver](subcommand-stop-transportserver.md)
