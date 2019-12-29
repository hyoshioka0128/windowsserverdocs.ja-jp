---
title: 無効にする TransportServer コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7531f8a638ac8fabdad08cc0134dbc63873505de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363462"
---
# <a name="using-the-disable-transportserver-command"></a>無効にする TransportServer コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを無効にします。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|無効にするトランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 トランスポート サーバーの名前が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="BKMK_examples"></a>例
サーバーを無効にするには、次のように入力します。
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[TransportServer 有効にするコマンドを使用して](using-the-enable-transportserver-command.md)
[get TransportServer コマンドを使用して](using-the-get-transportserver-command.md)
[サブコマンド: Set-transportserver](subcommand-set-transportserver.md)
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md)
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
