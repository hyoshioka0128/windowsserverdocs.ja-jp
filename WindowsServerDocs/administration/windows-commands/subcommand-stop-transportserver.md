---
title: サブコマンドの停止 TransportServer
description: 停止 TransportServer のリファレンス記事
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49e7c0c61a110fc7a7aa687ff30d60eb8f51a543
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881967"
---
# <a name="subcommand-stop-transportserver"></a>サブコマンド: 停止 TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバー上のすべてのサービスを停止します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 トランスポート サーバーが指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a><a name="BKMK_examples"></a>例
サービスを停止するには、次のいずれかを入力します。
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[無効化-TransportServer コマンド](using-the-disable-transportserver-command.md) 
 の使用[Enable TransportServer コマンド](using-the-enable-transportserver-command.md) 
 の使用[Get TransportServer コマンド](using-the-get-transportserver-command.md) 
 を使用する[サブコマンド: Set TransportServer](subcommand-set-transportserver.md) 
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md)
