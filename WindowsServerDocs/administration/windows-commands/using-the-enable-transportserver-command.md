---
title: 有効にする-TransportServer
description: トランスポートサーバーのすべてのサービスを有効にする enable TransportServer のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4cd87b78e7a84255593464fede553bc294138c7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936271"
---
# <a name="enable-transportserver"></a>有効にする-TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを有効にします。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Enable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 名前が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
サーバー上のサービスを有効にするには、次のいずれかを実行します。
```
wdsutil /Enable-TransportServer
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[無効化-TransportServer コマンド](using-the-disable-transportserver-command.md) 
 の使用[Get TransportServer コマンド](using-the-get-transportserver-command.md) 
 を使用する[サブコマンド: Set TransportServer](subcommand-set-transportserver.md) 
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md) 
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
