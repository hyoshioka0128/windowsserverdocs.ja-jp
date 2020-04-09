---
title: コピー-イメージ
description: コピーイメージの Windows コマンドに関するトピック。同じイメージグループ内のイメージをコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 443fa5bc87bbc7554e13f4b2a7fb7e36aa43dfaa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831705"
---
# <a name="copy-image"></a>コピー-イメージ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

同じイメージ グループ内にあるイメージをコピーします。 イメージ グループ間でのイメージのコピーを使用して、 [/export-image コマンドを使用して](using-the-export-image-command.md) コマンドし、 [追加イメージのコマンドを使用して](using-the-add-image-command.md) コマンドです。
このコマンドを使用する方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|コピーするイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: インストール|コピーするイメージの種類を指定します。 このオプションを設定する必要があります **インストール**します。|
|\mediaGroup:<Image group name>]|コピーするイメージを含むイメージ グループを指定します。 イメージ グループが指定されていないサーバーに 1 つのグループが存在する場合は、そのイメージ グループが既定で使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定する必要があります。|
|[/ファイル名:<Filename>]|コピーするイメージのファイル名を指定します。 ソース イメージは、名前によって一意に識別できない場合、は、ファイル名を指定する必要があります。|
|/DestinationImage|次の表に示すように、コピー先の画像の設定を指定します。<p>-/Name:<Name> にコピーするイメージの表示名を設定します。<br />-これによって:<Filename> -イメージのコピーを格納するイメージ ファイルの名前を設定します。<br />-[/Description: <Description>]-イメージのコピーの説明を設定します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
指定されたイメージのコピーを作成し、WindowsVista.wim という名前を付けて、次のように入力します。
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
指定されたイメージのコピーを作成するには、指定した設定を適用し、名前を WindowsVista.wim、型のコピー。
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
