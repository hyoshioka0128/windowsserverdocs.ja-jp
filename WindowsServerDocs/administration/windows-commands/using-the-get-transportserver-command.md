---
title: get TransportServer
description: 指定されたトランスポートサーバーに関する情報を表示する、TransportServer のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 115942290679decd8b8c660e4113576efb30123d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932170"
---
# <a name="get-transportserver"></a>get TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したトランスポート サーバーの情報を表示します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/表示: {Config}|指定したトランスポート サーバーの構成情報を返します。|
## <a name="examples"></a>例
サーバーに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-TransportServer /Show:Config
```
構成情報を表示するには、次のように入力します。
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[無効化-TransportServer コマンド](using-the-disable-transportserver-command.md) 
 の使用[Enable TransportServer コマンド](using-the-enable-transportserver-command.md) 
 の使用[サブコマンド: Set TransportServer](subcommand-set-transportserver.md) 
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md) 
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
