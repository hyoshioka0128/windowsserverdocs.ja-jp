---
title: サブコマンドの設定-イメージ
description: Windows コマンドに関するトピックでは、イメージの属性を変更するサブコマンドを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9564c489c1c3abced839ba27cbfe2841cd5894b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833935"
---
# <a name="subcommand-set-image"></a>サブコマンド: セット イメージ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージの属性を変更します。

## <a name="syntax"></a>構文
ブートイメージの場合:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>] 
[/Description:<Description>] [/Enabled:{Yes | No}]
```
インストールイメージの場合:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     [/Name:<Name>]
     [/Description:<Description>]
     [/UserFilter:<SDDL>]
     [/Enabled:{Yes | No}]
     [/UnattendFile:<Unattend file path>]
         [/OverwriteUnattend:{Yes | No}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|画像の種類を指定します。|
|/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|イメージのアーキテクチャを指定します。 異なるアーキテクチャの異なるブートイメージに対して同じイメージ名を持つことができるため、アーキテクチャを指定すると、正しいイメージが確実に変更されます。|
|[/ファイル名:<File name>]|名前によってイメージを一意に識別できない場合は、このオプションを使用してファイル名を指定する必要があります。|
|/Name|イメージの名前を指定します。|
|/Description<Description>]|イメージの説明を設定します。|
|[有効になっている/: {[はい] &#124; No}]|イメージを有効または無効にします。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが使用されます。 サーバーに複数のイメージグループが存在する場合は、このオプションを使用してイメージグループを指定する必要があります。|
|[/UserFilter:<SDDL>]|イメージに対するユーザーフィルターを設定します。 フィルター文字列は SDDL (Security Descriptor Definition Language) 形式である必要があります。 イメージグループの**セキュリティ**オプションとは異なり、このオプションはイメージの定義を表示できるユーザーのみを制限し、実際のイメージファイルリソースは制限しないことに注意してください。 ファイルリソースへのアクセスを制限し、そのためにイメージグループ内のすべてのイメージにアクセスできるようにするには、イメージグループ自体にセキュリティを設定する必要があります。|
|[/UnattendFile:<Unattend file path>]|イメージに関連付ける無人セットアップファイルへの完全パスを設定します。 例: **D:\Files\Unattend\Img1Unattend.xml**|
|[/OverwriteUnattend: {[はい] &#124; No}]|イメージに関連付けられている無人セットアップファイルが既に存在する場合は、 **/overwrite**を指定して無人セットアップファイルを上書きすることができます。 既定の設定は **[いいえ]** であることに注意してください。|
## <a name="examples"></a><a name=BKMK_examples></a>例
ブートイメージの値を設定するには、次のいずれかを入力します。
```
wdsutil /Set-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /Description:New description
wdsutil /verbose /Set-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:New Name /Description:New Description /Enabled:Yes
```
インストールイメージの値を設定するには、次のいずれかを入力します。
```
wdsutil /Set-Imagmedia:Windows Vista with Officemediatype:Install /Description:New description 
wdsutil /verbose /Set-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:New name /Description:New description /UserFilter:O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU) /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[の追加](using-the-add-image-command.md)イメージのコマンドを使用して
[コピー
イメージ](using-the-copy-image-command.md)のコマンドを使用して、イメージの[エクスポート](using-the-export-image-command.md)コマンドを使用して
[取得](using-the-get-image-command.md)イメージのコマンドを使用して、イメージの[削除](using-the-remove-image-command.md)[コマンド
](using-the-replace-image-command.md)

