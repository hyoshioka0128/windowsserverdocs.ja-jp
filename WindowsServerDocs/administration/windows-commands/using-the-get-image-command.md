---
title: イメージの取得
description: イメージに関する情報を取得する、イメージの参照トピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04cc7b8d90415e32be4103ef6c7f7b709c3550c3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719923"
---
# <a name="get-image"></a>イメージの取得

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
用紙<Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: {Boot &#124; Install}|画像の種類を指定します。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を指定することも可能である、アーキテクチャの値を指定する適切なイメージが返されることにより、します。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループが指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのグループが使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定するこのパラメーターを使用する必要があります。|
## <a name="examples"></a>例
ブート イメージに関する情報を取得するには、次のいずれかを入力します。
```
wdsutil /Get-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86
wdsutil /verbose /Get-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
```
インストール イメージに関する情報を取得するには、次のいずれかを入力します。
```
wdsutil /Get-Imagmedia:Windows Vista with Officemediatype:Install
wdsutil /verbose /Get-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[追加イメージ](using-the-add-image-command.md)
のコマンドを使用して[コピーイメージ](using-the-copy-image-command.md)
[Using the Export-Image Command](using-the-export-image-command.md)
のコマンドを使用して削除イメージのコマンドを使用して[削除](using-the-remove-image-command.md)
イメージのコマンドを使用して[置換イメージ](using-the-replace-image-command.md)
のコマンドを使用して[サブコマンド: イメージを設定](subcommand-set-image.md)する
