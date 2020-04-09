---
title: 置換-イメージ
description: Windows コマンドに関するトピックでは、既存のイメージをそのイメージの新しいバージョンで置き換えます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d16ec07171e4560af8074cb9b0be7b6dc252119
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830225"
---
# <a name="using-the-replace-image-command"></a>置換イメージのコマンドを使用してください。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のイメージをそのイメージの新しいバージョンに置き換えます。
## <a name="syntax"></a>構文
ブートイメージの場合:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/Name:<Image name>]
         [/Description:<Image description>]
```
インストールイメージの場合:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/SourceImage:<Source image name>]
         [/Name:<Image name>]
         [/Description:<Image description>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|置換されるイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|置換されるイメージの種類を指定します。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|置換されるイメージのアーキテクチャを指定します。 さまざまなアーキテクチャのさまざまなブート イメージで同じイメージの名前を指定することも可能であるため、アーキテクチャを指定する適切なイメージを置き換えることにより、します。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
|置換 ementimage|交換用のイメージの設定を指定します。 次のオプションを使用してこれらの設定を設定します。<p>-mediaFile: <file path> -名と、新しい .wim ファイルの場所 (完全パス) を指定します。<br />-[/SourceImage: <image name>]-.wim ファイルには、複数のイメージが含まれている場合に使用するイメージを指定します。 このオプションは、インストール イメージにのみ適用されます。<br />-[/Name:<Image name>] イメージの表示名を設定します。<br />-[/説明:<Image description>]-イメージの説明を設定します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
ブート イメージを置き換えるには、次のいずれかを入力します。
```
wdsutil /replace-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /replacementImagmediaFile:C:\MyFolder\Boot.wim
wdsutil /verbose /Progress /replace-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/replacementImagmediaFile:\\MyServer\Share\Boot.wim /Name:My WinPE Image /Description:WinPE Image with drivers
```
インストール イメージを置き換えるには、次のいずれかを入力します。
```
wdsutil /replace-Imagmedia:Windows Vista Homemediatype:Install /replacementImagmediaFile:C:\MyFolder\Install.wim
wdsutil /verbose /Progress /replace-Imagmedia:Windows Vista Pro /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:Install.wim /replacementImagmediaFile:\\MyServer\Share \Install.wim /SourceImage:Windows Vista Ultimate /Name:Windows Vista Desktop /Description:Windows Vista Ultimate with standard business applications.
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
