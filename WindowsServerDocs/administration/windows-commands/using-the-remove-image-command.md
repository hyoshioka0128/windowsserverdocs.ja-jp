---
title: 削除するイメージのコマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0876649a4de55604707f03ca98cf0ceed2920b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362830"
---
# <a name="using-the-remove-image-command"></a>削除するイメージのコマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからイメージを削除します。
## <a name="syntax"></a>構文
ブートイメージの場合:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
インストールイメージの場合:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<Filename>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア: <Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|画像の種類を指定します。|
|/アーキテクチャ: {x86 &#124; ia64 &#124; x64}|イメージのアーキテクチャを指定します。 さまざまなアーキテクチャのさまざまなブート イメージで同じイメージの名前を指定することも可能である、アーキテクチャの値を指定する適切なイメージを削除することにより、します。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが使用されます。 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定するこのオプションを使用する必要があります。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
## <a name="BKMK_examples"></a>例
ブート イメージを削除するには、次のように入力します。
```
wdsutil /remove-Imagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Imagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
```
インストール イメージを削除するには、次のように入力します。
```
wdsutil /remove-Imagmedia:"Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
