---
title: イメージのエクスポート コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efa9b2d09c37a383a91883ee02c995eedb2f235e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823143"
---
# <a name="using-the-export-image-command"></a>イメージのエクスポート コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のイメージをイメージ ストアから別の Windows イメージ (.wim) ファイルにエクスポートします。
## <a name="syntax"></a>構文
ブート イメージ。
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
インストール イメージ。
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|エクスポートするイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|エクスポートする画像の種類を指定します。|
|\mediaGroup:<Image group name>]|エクスポートするイメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが既定で使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定してください。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|エクスポートするイメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を持つことなのではアーキテクチャの値を指定する適切なイメージが必ず返されるようにします。|
|[/ファイル名:<Filename>]|場合は、イメージは、名前によって一意に識別できない、ファイル名を指定する必要があります。|
|/DestinationImage|コピー先の画像の設定を指定します。 次のオプションを使用してこれらの設定を指定することができます。<br /><br />-/Filepath:<File path and name> -新しいイメージのファイルの完全パスを指定します。<br />-[/Name:<Name>]-イメージの表示名を設定します。 名が指定されていない場合は、ソース イメージの表示名が使用されます。<br />-[/説明。 <Description>-イメージの説明を設定します。|
|[/Overwrite: {[はい]&#124;いいえ&#124;追加}]|ファイルが指定されているかどうかを判断、 **/DestinationImage**オプションは、/Filepath でその名前を持つ既存のファイルが既に存在する場合に上書きされます。<br /><br />-   **[はい]** により、既存のファイルを上書きします。<br />-   **いいえ**(既定のオプション) と同じ名前のファイルが既に存在する場合に発生するエラーが発生します。<br />-   **追加**生成された画像が既存の .wim ファイル内の新しいイメージとして追加されます。|
## <a name="BKMK_examples"></a>例
ブート イメージをエクスポートするには、次のいずれかを入力します。
```
wdsutil /Export-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:"C:\temp\boot.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/DestinationImage /Filepath:"\\Server\Share\ExportImage.wim" /Name:"Exported WinPE image" /Description:"WinPE Image from WDS server" /Overwrite:Yes
```
インストール イメージをエクスポートするには、次のいずれかを入力します。
```
wdsutil /Export-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Filepath:"C:\Temp\Install.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:"Exported Windows image" /Description:"Windows Vista image from WDS server" /Overwrite:append
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
