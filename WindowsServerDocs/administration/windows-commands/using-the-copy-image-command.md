---
title: コピー イメージのコマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f269884e9c1f96151c9e1220242fad917b76831
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363557"
---
# <a name="using-the-copy-image-command"></a>コピー イメージのコマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア: <Image name>|コピーするイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: インストール|コピーするイメージの種類を指定します。 このオプションを設定する必要があります **インストール**します。|
|\mediaGroup:<Image group name>]|コピーするイメージを含むイメージ グループを指定します。 イメージ グループが指定されていないサーバーに 1 つのグループが存在する場合は、そのイメージ グループが既定で使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定する必要があります。|
|[/ファイル名:<Filename>]|コピーするイメージのファイル名を指定します。 ソース イメージは、名前によって一意に識別できない場合、は、ファイル名を指定する必要があります。|
|/DestinationImage|次の表に示すように、コピー先の画像の設定を指定します。<br /><br />-/Name:<Name> にコピーするイメージの表示名を設定します。<br />-これによって:<Filename> -イメージのコピーを格納するイメージ ファイルの名前を設定します。<br />-[/Description: <Description>]-イメージのコピーの説明を設定します。|
## <a name="BKMK_examples"></a>例
指定されたイメージのコピーを作成し、WindowsVista.wim という名前を付けて、次のように入力します。
```
wdsutil /copy-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim"
```
指定されたイメージのコピーを作成するには、指定した設定を適用し、名前を WindowsVista.wim、型のコピー。
```
wdsutil /verbose /Progress /copy-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim" /Description:"This is a copy of the original Windows image with Office installed"
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
