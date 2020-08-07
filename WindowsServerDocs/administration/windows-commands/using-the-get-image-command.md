---
title: イメージの取得
description: イメージに関する情報を取得する get イメージの参照記事です。
ms.topic: article
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b97e13441d883a683515222774194c1fb75ecbc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879364"
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
|パラメーター|説明|
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
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[[イメージの追加] コマンド](using-the-add-image-command.md) 
 の使用[コピーイメージのコマンド](using-the-copy-image-command.md) 
 を使用する[Export-Image コマンド](using-the-export-image-command.md) 
 の使用[イメージの削除コマンド](using-the-remove-image-command.md) 
 を使用する[置換イメージのコマンド](using-the-replace-image-command.md) 
 を使用する[サブコマンド: イメージの設定](subcommand-set-image.md)
