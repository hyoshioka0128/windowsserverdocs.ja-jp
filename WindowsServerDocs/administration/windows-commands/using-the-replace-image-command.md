---
title: 置換-イメージ
description: 置換イメージのリファレンストピック。既存のイメージをそのイメージの新しいバージョンに置き換えます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9dad35e54f064e02b863059ae6da9378403ee4f9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720320"
---
# <a name="using-the-replace-image-command"></a>置換イメージのコマンドを使用してください。

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
|パラメーター|[説明]|
|-------|--------|
用紙<Image name>|置換されるイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: {Boot &#124; Install}|置換されるイメージの種類を指定します。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|置換されるイメージのアーキテクチャを指定します。 さまざまなアーキテクチャのさまざまなブート イメージで同じイメージの名前を指定することも可能であるため、アーキテクチャを指定する適切なイメージを置き換えることにより、します。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
|置換 ementimage|交換用のイメージの設定を指定します。 次のオプションを使用してこれらの設定を設定します。<p>-mediaFile: <file path> -名と、新しい .wim ファイルの場所 (完全パス) を指定します。<br />-[/SourceImage: <image name>]-.wim ファイルには、複数のイメージが含まれている場合に使用するイメージを指定します。 このオプションは、インストール イメージにのみ適用されます。<br />-[/Name:<Image name>] イメージの表示名を設定します。<br />-[/説明:<Image description>]-イメージの説明を設定します。|
## <a name="examples"></a>例
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
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[のキー追加イメージ](using-the-add-image-command.md)
のコマンドを使用して[コピーイメージ](using-the-copy-image-command.md)
のコマンドを使用して、イメージの[エクスポート](using-the-export-image-command.md)
コマンドを使用して[get](using-the-get-image-command.md)
イメージのコマンドを使用して[置換イメージ](using-the-replace-image-command.md)
のコマンドを使用して[サブコマンド:](subcommand-set-image.md)イメージの設定
