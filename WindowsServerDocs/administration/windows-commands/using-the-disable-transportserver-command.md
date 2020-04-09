---
title: 無効にする-TransportServer
description: トランスポートサーバーのすべてのサービスを無効にする、disable TransportServer の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39f930a464364cda680098ef4e7e1081d0995503
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831625"
---
# <a name="disable-transportserver"></a>無効にする-TransportServer

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーのすべてのサービスを無効にします。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|無効にするトランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 トランスポート サーバーの名前が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
サーバーを無効にするには、次のように入力します。
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[TransportServer 有効にするコマンドを使用して](using-the-enable-transportserver-command.md)
[get TransportServer コマンドを使用して](using-the-get-transportserver-command.md)
[サブコマンド: Set-transportserver](subcommand-set-transportserver.md)
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md)
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
