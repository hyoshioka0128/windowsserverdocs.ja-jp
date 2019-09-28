---
title: サブコマンド/Get-multicasttransmission
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0e05a1d625e560d85f0af6ae1d76ef8116ddfd8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383827"
---
# <a name="subcommand-start-multicasttransmission"></a>サブコマンド:/start-multicasttransmission

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージのスケジュールされたキャスト転送を開始します。
## <a name="syntax"></a>構文
**Windows Server 2008**
```
wdsutil /start-MulticastTransmissiomedia:<Image name> [/Server:<Server namemediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
**Windows Server 2008 R2**ブートイメージ:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
インストールイメージの場合:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア: <Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {インストール&#124;ブート}|イメージの種類を指定します。 このオプションに設定する必要があります **インストール** Windows Server 2008 用です。|
|/アーキテクチャ: {x86 &#124; ia64 &#124; x64}|転送の開始に関連付けられているブート イメージのアーキテクチャです。 ブート イメージのイメージの同じ名前のさまざまなアーキテクチャに行うことがあるために、正しい転送が使用されるようにするアーキテクチャを指定してください。|
|\mediaGroup:<Image group name>]|イメージのイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループ名を指定するこのオプションを使用する必要があります。|
|[/ファイル名:<File name>]|イメージを含むファイルの名前を指定します。 イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
## <a name="BKMK_examples"></a>例
マルチキャスト転送を開始するには、次のいずれかを入力します。
```
wdsutil /start-MulticastTransmissiomedia:"Vista with Office"
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
起動するブート イメージの種類の Windows Server 2008 R2 のマルチキャスト転送。
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllMulticastTransmissions コマンドを使用して](using-the-get-allmulticasttransmissions-command.md)
[/get-multicasttransmission コマンドを使用して](using-the-get-multicasttransmission-command.md)
[MulticastTransmission 新しいコマンドを使用して](using-the-new-multicasttransmission-command.md)
[/remove-multicasttransmission コマンドを使用して](using-the-remove-multicasttransmission-command.md)
