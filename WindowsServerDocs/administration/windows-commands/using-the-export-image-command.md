---
title: エクスポート-イメージ
description: エクスポートイメージのリファレンストピック。既存のイメージをイメージストアから別の Windows イメージ (.wim) ファイルにエクスポートします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 477859687732fa2cccdc782edb81fdd348f313c5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720913"
---
# <a name="export-image"></a>エクスポート-イメージ

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のイメージをイメージ ストアから別の Windows イメージ (.wim) ファイルにエクスポートします。

## <a name="syntax"></a>構文
ブートイメージの場合:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
インストールイメージの場合:
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
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
用紙<Image name>|エクスポートするイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: {Boot &#124; Install}|エクスポートする画像の種類を指定します。|
|\mediaGroup:<Image group name>]|エクスポートするイメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが既定で使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定してください。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|エクスポートするイメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を持つことなのではアーキテクチャの値を指定する適切なイメージが必ず返されるようにします。|
|[/ファイル名:<Filename>]|イメージを名前で一意に識別できない場合は、ファイル名を指定する必要があります。|
|/DestinationImage|コピー先の画像の設定を指定します。 次のオプションを使用してこれらの設定を指定することができます。<p>-/Filepath:<File path and name> -新しいイメージの完全ファイルパスを指定します。<br />-[/Name:<Name>]-イメージの表示名を設定します。 名が指定されていない場合は、ソース イメージの表示名が使用されます。<br />-[/Description: <Description>]-イメージの説明を設定します。|
|[/Overwrite: {はい &#124; &#124; 追加}]|/Filepath にその名前の既存のファイルが既に存在する場合に、 **/destinationimage**オプションで指定されたファイルを上書きするかどうかを指定します。<p>-   **[はい]** に設定すると、既存のファイルが上書きされます。<br />-   [**いいえ**] (既定のオプション) を指定すると、同じ名前のファイルが既に存在する場合にエラーが発生します。<br />-   **append**を指定すると、生成されたイメージが既存の .wim ファイル内に新しいイメージとして追加されます。|
## <a name="examples"></a>例
ブート イメージをエクスポートするには、次のいずれかを入力します。
```
wdsutil /Export-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
wdsutil /verbose /Progress /Export-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```
インストール イメージをエクスポートするには、次のいずれかを入力します。
```
wdsutil /Export-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
wdsutil /verbose /Progress /Export-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[追加イメージ](using-the-add-image-command.md)
のコマンドを使用して[コピーイメージ](using-the-copy-image-command.md)
のコマンドを使用して[get](using-the-get-image-command.md)
イメージのコマンドを使用して削除イメージのコマンドを使用して[削除](using-the-remove-image-command.md)
イメージのコマンドを使用して[サブコマンド:](subcommand-set-image.md)イメージを設定[する](using-the-replace-image-command.md)

