---
title: /Get-multicasttransmission
description: /Get-multicasttransmission の Windows コマンドに関するトピック。指定したイメージのマルチキャスト転送に関する情報が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec66107452be86423a4d542ee3999e86f1446656
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830945"
---
# <a name="get-multicasttransmission"></a>/Get-multicasttransmission

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したイメージのマルチキャスト転送に関する情報を表示します。

## <a name="syntax"></a>構文
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] 
[/Filename:<File name>] [/Show:Clients]
```
**Windows Server 2008 R2**ブートイメージの転送:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
インストールイメージの転送:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|このイメージに関連付けられているマルチキャスト転送を表示します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
mediatype: インストール|イメージの種類を指定します。 このオプションに設定する必要があります **インストール**します。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループを使用します。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定するこのオプションを使用する必要があります。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|転送に関連付けられているブート イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を指定することも可能であるために、適切なイメージが使用されるようにするアーキテクチャを指定してください。|
|[/ファイル名:<File name>]|イメージを含むファイルを指定します。 イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
|[/ショー: クライアント]<p>または<p>[詳細: クライアント]|マルチキャスト転送に接続されているクライアント コンピューターに関する情報を表示します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
**Windows Server 2008**"Vista with Office" という名前のイメージの転送に関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Officemediatype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2**"Vista with Office" という名前のイメージの転送に関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Office
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllMulticastTransmissions コマンドを使用して](using-the-get-allmulticasttransmissions-command.md)
[MulticastTransmission 新しいコマンドを使用して](using-the-new-multicasttransmission-command.md)
[/remove-multicasttransmission コマンドを使用して](using-the-remove-multicasttransmission-command.md)
[サブコマンド:/start-multicasttransmission](subcommand-start-multicasttransmission.md)
