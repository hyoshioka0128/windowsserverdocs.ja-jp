---
title: Get AllImageGroups コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54e302dca5014d084c7277154eb491f9e33a536b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363313"
---
# <a name="using-the-get-allimagegroups-command"></a>Get AllImageGroups コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーおよびそれらのイメージ グループのすべてのイメージ上のすべてのイメージ グループに関する情報を取得します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|詳細/|各イメージからイメージのメタデータを返します。 このパラメーターを使用しない場合、既定の動作は、イメージの名前、説明、および各イメージのファイル名のみを返すには。|
## <a name="BKMK_examples"></a>例
イメージ グループに関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 ImageGroup コマンドを使用して](using-the-add-imagegroup-command.md)
[get ImageGroup コマンドを使用して](using-the-get-imagegroup-command.md)
[削除 ImageGroup コマンドを使用して](using-the-remove-imagegroup-command.md)
[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)
