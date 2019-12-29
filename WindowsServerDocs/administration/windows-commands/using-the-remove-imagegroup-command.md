---
title: 削除 ImageGroup コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30e4c2c7c5cf2668d62e96d8d2a54dc33e3d2a55
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71960956"
---
# <a name="using-the-remove-imagegroup-command"></a>削除 ImageGroup コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからイメージグループを削除します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaGroup: <Image group name>|削除するイメージ グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="BKMK_examples"></a>例
イメージ グループを削除するには、次のいずれかを入力します。
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer 
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)  
[追加 ImageGroup コマンドを使用してください。](using-the-add-imagegroup-command.md)  
[Get AllImageGroups コマンドの使用](using-the-get-allimagegroups-command.md)  
[Get ImageGroup コマンドの使用](using-the-get-imagegroup-command.md)  
[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)  
