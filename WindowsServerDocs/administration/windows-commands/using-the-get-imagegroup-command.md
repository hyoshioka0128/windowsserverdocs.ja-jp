---
title: Get ImageGroup コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9dcb76155dc1044730673ed46a53cad57441a246
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862603"
---
# <a name="using-the-get-imagegroup-command"></a>Get ImageGroup コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージ グループおよびその中のイメージに関する情報を取得します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaGroup:<Image group name>|イメージ グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|[/詳細]|各イメージのイメージのメタデータを返します。 このパラメーターが使用でない場合は、既定の動作は、イメージの名前、説明、およびファイル名のみを返すには。|
## <a name="BKMK_examples"></a>例
イメージ グループに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
メタデータを含む情報を表示するには、次のように入力します。
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 ImageGroup コマンドを使用して](using-the-add-imagegroup-command.md)
[get AllImageGroups コマンドを使用して](using-the-get-allimagegroups-command.md)
[削除 ImageGroup コマンドを使用して](using-the-remove-imagegroup-command.md)
[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)
