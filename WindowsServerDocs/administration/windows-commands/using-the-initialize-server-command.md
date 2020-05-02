---
title: Initialize-サーバー
description: サーバーの役割をインストールした後に最初に使用するために Windows 展開サービスサーバーを構成する Initialize-Server のリファレンストピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54180923a077c0b423e73588bcbd1c03b0154d08
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719716"
---
# <a name="initialize-server"></a>Initialize-サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーの役割をインストールした後は、初期使用のための Windows 展開サービス サーバーを構成します。 このコマンドを実行した後必要がありますを使用する、 [追加イメージのコマンドを使用して](using-the-add-image-command.md) コマンドをサーバーにイメージを追加します。
## <a name="syntax"></a>構文
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|remInst<Full path>|RemoteInstall フォルダーの完全なパスと名前を指定します。 指定したフォルダーが既に存在しない場合、コマンドの実行時に、このオプションを作成します。 常に発生した場合でも、リモート コンピューターのローカル パスを入力する必要があります。 例: **D:\remoteInstall**。|
|[]、[承認]|動的ホスト制御プロトコル (DHCP) で、サーバーが認証されます。 このオプションは、DHCP 承認されていない検出が有効になっている場合にのみ意味を Windows 展開サービス PXE サーバーで承認する必要 DHCP クライアント コンピューターが処理される前に必要があります。 既定では DHCP 承認されていない検出が無効になっていることに注意してください。|
## <a name="examples"></a>例
サーバーを初期化し、remoteInstall 共有フォルダーを F: ドライブに設定するには、「」と入力します。
```
wdsutil /Initialize-Server /remInst:F:\remoteInstall
```
サーバーを初期化し、remoteInstall 共有フォルダーを C: ドライブに設定するには、「」と入力します。
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:C:\remoteInstall
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[の](using-the-disable-server-command.md)
キーを使用してサーバーを無効にするコマンドを使用して、[有効](using-the-enable-server-command.md)
にするサーバーのコマンドを使用して[get](using-the-get-server-command.md)
サーバーコマンドを使用してサブコマンド[: サーバーを](subcommand-start-server.md)
[設定](subcommand-set-server.md)

[し](the-uninitialize-server-option.md)[ます。](subcommand-stop-server.md)
