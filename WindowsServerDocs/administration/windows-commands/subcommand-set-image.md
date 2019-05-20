---
title: サブコマンドの画像の設定
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e63c67210764de76edae18a1897a68d763f9d695
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856483"
---
# <a name="subcommand-set-image"></a>サブコマンド: セット イメージ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージの属性を変更します。
## <a name="syntax"></a>構文
ブート イメージ。
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>] 
[/Description:<Description>] [/Enabled:{Yes | No}]
```
インストール イメージ。
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
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
メディア:<Image name>|イメージの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|イメージの種類を指定します。|
|/アーキテクチャ: {x86 &#124; ia64 &#124; x64}|イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでは、同じイメージのさまざまなブート イメージの名前を持つは、適切なイメージが変更されたことにより、アーキテクチャを指定します。|
|[/ファイル名:<File name>]|イメージは、名前によって一意に識別できない、このオプションを使用して、ファイル名を指定する必要があります。|
|[/Name]|イメージの名前を指定します。|
|[/説明。<Description>]|イメージの説明を設定します。|
|[有効になっている/: {[はい] &#124; No}]|有効またはイメージを無効にします。|
|\mediaGroup:<Image group name>]|イメージを含むイメージ グループを指定します。 イメージ グループ名が指定されていないサーバーに 1 つだけのイメージ グループが存在する場合は、そのイメージ グループが使用されます。 サーバーでは、複数のイメージ グループが存在する場合は、イメージ グループを指定するこのオプションを使用する必要があります。|
|[/UserFilter:<SDDL>]|イメージ上には、ユーザー フィルターを設定します。 フィルター文字列は、セキュリティ記述子定義言語 (SDDL) 形式である必要があります。 なおとは異なり、 **/Security**オプション イメージ グループの場合、このオプションだけを制限できる人をイメージの定義と実際のイメージ ファイル リソースではありません。 ファイルのリソースへのアクセスを制限し、イメージ グループ内のすべてのイメージへのアクセスをそのためには、イメージ グループ自体のセキュリティを設定する必要があります。|
|[/UnattendFile:<Unattend file path>]|イメージと関連付ける無人セットアップ ファイルへの完全なパスを設定します。 例:**D:\Files\Unattend\Img1Unattend.xml**|
|[/OverwriteUnattend: {[はい] &#124; No}]|指定できる **/overwrite**イメージに関連付けられている無人セットアップ ファイルが既にある場合は、無人セットアップ ファイルを上書きします。 既定の設定は注**いいえ**します。|
## <a name="BKMK_examples"></a>例
ブート イメージの値を設定するには、次のいずれかを入力します。
```
wdsutil /Set-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /Description:"New description"
wdsutil /verbose /Set-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:"New Name" /Description:"New Description" /Enabled:Yes
```
インストール イメージの値を設定するには、次のいずれかを入力します。
```
wdsutil /Set-Imagmedia:"Windows Vista with Officemediatype:Install /Description:"New description" 
wdsutil /verbose /Set-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:"New name" /Description:"New description" /UserFilter:"O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU)" /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加イメージのコマンドを使用して](using-the-add-image-command.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[を使用して、/Export-image コマンド](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
 [置換イメージのコマンドを使用します。](using-the-replace-image-command.md)
