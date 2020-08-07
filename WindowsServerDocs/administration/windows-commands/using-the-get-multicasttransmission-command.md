---
title: /Get-multicasttransmission
description: 指定されたイメージのマルチキャスト転送に関する情報を表示する/Get-multicasttransmission のリファレンス記事です。
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 883bfb0d462ab87162d6e849947334eae010b0b1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896950"
---
# <a name="get-multicasttransmission"></a>/Get-multicasttransmission

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
用紙<Image name>|このイメージに関連付けられているマルチキャスト転送を表示します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
mediatype: インストール|イメージの種類を指定します。 このオプションに設定する必要があります **インストール**します。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループを使用します。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定するこのオプションを使用する必要があります。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|転送に関連付けられているブート イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を指定することも可能であるために、適切なイメージが使用されるようにするアーキテクチャを指定してください。|
|[/ファイル名:<File name>]|イメージを含むファイルを指定します。 イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
|[/ショー: クライアント]<p>or<p>[詳細: クライアント]|マルチキャスト転送に接続されているクライアント コンピューターに関する情報を表示します。|
## <a name="examples"></a>例
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
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[AllMulticastTransmissions コマンド](using-the-get-allmulticasttransmissions-command.md) 
 の使用[/Get-multicasttransmission コマンド](using-the-new-multicasttransmission-command.md) 
 の使用[/Get-multicasttransmission コマンド](using-the-remove-multicasttransmission-command.md) 
 を使用する[サブコマンド:/get-multicasttransmission](subcommand-start-multicasttransmission.md)
