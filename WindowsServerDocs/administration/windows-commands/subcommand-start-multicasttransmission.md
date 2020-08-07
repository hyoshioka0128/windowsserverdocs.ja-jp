---
title: サブコマンド/Get-multicasttransmission
description: サブコマンド/Get-multicasttransmission の参照記事。イメージのスケジュールされたキャスト転送を開始します。
ms.topic: article
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34d55e233926a3e5c8a07a6a31d985f1955f814e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882089"
---
# <a name="subcommand-start-multicasttransmission"></a>サブコマンド:/start-multicasttransmission

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
用紙<Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
mediatype: {Install&#124;Boot}|イメージの種類を指定します。 このオプションに設定する必要があります **インストール** Windows Server 2008 用です。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|転送の開始に関連付けられているブート イメージのアーキテクチャです。 ブート イメージのイメージの同じ名前のさまざまなアーキテクチャに行うことがあるために、正しい転送が使用されるようにするアーキテクチャを指定してください。|
|\mediaGroup:<Image group name>]|イメージのイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが使用されます。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループ名を指定するこのオプションを使用する必要があります。|
|[/ファイル名:<File name>]|イメージを含むファイルの名前を指定します。 イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
## <a name="examples"></a>例
マルチキャスト転送を開始するには、次のいずれかを入力します。
```
wdsutil /start-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
起動するブート イメージの種類の Windows Server 2008 R2 のマルチキャスト転送。
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[AllMulticastTransmissions コマンド](using-the-get-allmulticasttransmissions-command.md) 
 の使用[/Get-multicasttransmission コマンド](using-the-get-multicasttransmission-command.md) 
 の使用[/Get-multicasttransmission コマンド](using-the-new-multicasttransmission-command.md) 
 の使用[/Get-multicasttransmission コマンドを使用する](using-the-remove-multicasttransmission-command.md)
