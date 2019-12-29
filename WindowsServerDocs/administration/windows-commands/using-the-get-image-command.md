---
title: Get イメージのコマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73b25fd70c1512f99b5097b2317c3f0403f3526c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363106"
---
# <a name="using-the-get-image-command"></a>Get イメージのコマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージに関する情報を取得します。
## <a name="syntax"></a>構文
ブートイメージの場合:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
インストールイメージの場合:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア: <Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|画像の種類を指定します。|
|/アーキテクチャ: {x86 &#124; ia64 &#124; x64}|イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を指定することも可能である、アーキテクチャの値を指定する適切なイメージが返されることにより、します。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループが指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのグループが使用されます。 サーバーに複数のイメージグループが存在する場合は、このパラメーターを使用してイメージグループを指定する必要があります。|
## <a name="BKMK_examples"></a>例
ブート イメージに関する情報を取得するには、次のいずれかを入力します。
```
wdsutil /Get-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86
wdsutil /verbose /Get-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
```
インストール イメージに関する情報を取得するには、次のいずれかを入力します。
```
wdsutil /Get-Imagmedia:"Windows Vista with Officemediatype:Install
wdsutil /verbose /Get-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
