---
title: 新しい MulticastTransmission コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a6893d34e8f1242966d644159823277cf71a0c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401983"
---
# <a name="using-the-new-multicasttransmission-command"></a>新しい MulticastTransmission コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージの新しいマルチキャスト転送を作成します。 このコマンドは、Windows 展開サービス mmc スナップインを使用して転送を作成することと同じです ( **[マルチキャスト転送]** ノードを右クリックし、 **[マルチキャスト転送]** をクリックします)。 展開サーバーの役割サービスと、トランスポート サーバー役割サービスがインストールされる既定のインストール) の両方がある場合は、このコマンドを使用する必要があります。 トランスポート サーバーの役割サービスのみがインストールされていれば、使用 [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)します。
## <a name="syntax"></a>構文
インストールイメージの転送:
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
ブートイメージの転送の場合 (Windows Server 2008 R2 でのみサポートされます):
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア: <Image name>|マルチキャストを使用して転送するイメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/FriendlyName: <Friendly name>|転送のフレンドリ名を指定します。|
|/Description<Description>]|送信の説明を指定します。|
メディアの種類: {ブート&#124;インストール}|マルチキャストを使用して転送する画像の種類を指定します。 注 **ブート** は Windows Server 2008 R2 でのみサポートされます。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループを使用します。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループ名を指定するこのオプションを使用する必要があります。|
|[/ファイル名:<File name>]|ファイル名を指定します。 場合は、ソース イメージは、名前によって一意に識別できない、ファイル名を指定するこのオプションを使用する必要があります。|
|/Transmissiontype:{AutoCast &#124; ScheduledCast}|転送を自動的に開始するかどうかを指定します (オート) か、指定した開始条件 (キャスト) を基にします。<br /><br /><ul><li>**自動キャスト**します。 この転送の型は、該当するクライアントは、インストール イメージを要求するように選択したイメージのマルチキャスト転送が開始することを示します。 既に開始されている転送に参加する他のクライアントが同じイメージを要求するとします。</li><li>**スケジュールされたキャスト**します。 この転送型では、イメージや、特定の曜日と時刻を要求するクライアントの数に基づいて、転送の開始条件を設定します。 次のオプションを選択できます。<br /><br /><ul><li>[/時刻: <time>]-次の形式を使用して、転送を開始する時刻を設定します。YYYY/MM/DD: hh: mm。</li><li>[/クライアント: <Number of clients>]-クライアントから送信が開始する前に待機するの最小数を設定します。</li></ul></li></ul>|
|/アーキテクチャ: {x86 &#124; ia64 &#124; x64}|マルチキャストを使用して送信するブート イメージのアーキテクチャを指定します。 さまざまなアーキテクチャのブート イメージで同じ名前を持つことなので、確実に適切なイメージが使用されるアーキテクチャを指定してください。|
|[/ファイル名:<File name>]|ファイル名を指定します。 ソース イメージは、名前によって一意に識別できない場合、は、ファイル名を指定する必要があります。|
## <a name="BKMK_examples"></a>例
Windows Server 2008 R2 では、ブート イメージの自動キャスト転送を作成するに次のように入力します。
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS Boot Transmission"
/Image:"X64 Boot Imagemediatype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
自動キャスト転送は、インストール イメージを作成するには、次のように入力します。
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS AutoCast Transmission"
/Image:"Vista with Officemediatype:Install /Transmissiontype:AutoCast
```
インストール イメージのスケジュールされたキャスト転送を作成するには、次のように入力します。
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS SchedCast Transmission" /Server:MyWDSServemedia:"Vista with Officemediatype:Install 
/Transmissiontype:ScheduledCast /time:"2006/11/20:17:00" /Clients:100
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllMulticastTransmissions コマンドを使用して](using-the-get-allmulticasttransmissions-command.md)
[/get-multicasttransmission コマンドを使用して](using-the-get-multicasttransmission-command.md)
[/remove-multicasttransmission コマンドを使用して](using-the-remove-multicasttransmission-command.md)
[サブコマンド:/start-multicasttransmission](subcommand-start-multicasttransmission.md)
