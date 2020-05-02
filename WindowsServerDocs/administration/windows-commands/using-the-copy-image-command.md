---
title: コピー-イメージ
description: コピーイメージのリファレンストピック。同じイメージグループ内のイメージをコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3ffd590682ec36f78d3cbd53fd67fe3b5981e4c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720997"
---
# <a name="copy-image"></a>コピー-イメージ

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

同じイメージ グループ内にあるイメージをコピーします。 イメージ グループ間でのイメージのコピーを使用して、 [/export-image コマンドを使用して](using-the-export-image-command.md) コマンドし、 [追加イメージのコマンドを使用して](using-the-add-image-command.md) コマンドです。

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
|パラメーター|[説明]|
|-------|--------|
用紙<Image name>|コピーするイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: インストール|コピーするイメージの種類を指定します。 このオプションを設定する必要があります **インストール**します。|
|\mediaGroup:<Image group name>]|コピーするイメージを含むイメージ グループを指定します。 イメージ グループが指定されていないサーバーに 1 つのグループが存在する場合は、そのイメージ グループが既定で使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定する必要があります。|
|[/ファイル名:<Filename>]|コピーするイメージのファイル名を指定します。 ソース イメージは、名前によって一意に識別できない場合、は、ファイル名を指定する必要があります。|
|/DestinationImage|次の表に示すように、コピー先の画像の設定を指定します。<p>-/Name:<Name> にコピーするイメージの表示名を設定します。<br />-これによって:<Filename> -イメージのコピーを格納するイメージ ファイルの名前を設定します。<br />-[/Description: <Description>]-イメージのコピーの説明を設定します。|
## <a name="examples"></a>例
指定されたイメージのコピーを作成し、WindowsVista.wim という名前を付けて、次のように入力します。
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
指定されたイメージのコピーを作成するには、指定した設定を適用し、名前を WindowsVista.wim、型のコピー。
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[のキー追加イメージ](using-the-add-image-command.md)
のコマンドを使用して[エクスポートイメージ](using-the-export-image-command.md)
のコマンドを使用して[get](using-the-get-image-command.md)
イメージのコマンドを使用して削除イメージのコマンドを使用して[削除](using-the-remove-image-command.md)
[イメージ](using-the-replace-image-command.md)
のコマンドを使用して[サブコマンド:](subcommand-set-image.md)イメージを設定する
