---
title: イメージグループの削除
description: サーバーからイメージグループを削除する remove ImageGroup のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f814d83a32a8c739e7462bc77251cf3f3f4fe20e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720353"
---
# <a name="using-the-remove-imagegroup-command"></a>削除 ImageGroup コマンドを使用してください。

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからイメージ グループを削除します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
mediaGroup:<Image group name>|削除するイメージ グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
イメージ グループを削除するには、次のいずれかを入力します。
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer 
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
[追加 ImageGroup コマンドを使用してください。](using-the-add-imagegroup-command.md)  
[Get AllImageGroups コマンドを使用してください。](using-the-get-allimagegroups-command.md)  
[Get ImageGroup コマンドを使用してください。](using-the-get-imagegroup-command.md)  
[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)  
