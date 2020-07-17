---
title: イメージグループの削除
description: サーバーからイメージグループを削除する、remove ImageGroup のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d11a24152250786e600332c5eea0a6ffebc4848
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933333"
---
# <a name="using-the-remove-imagegroup-command"></a>削除 ImageGroup コマンドを使用してください。

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからイメージ グループを削除します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaGroup:<Image group name>|削除するイメージ グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
イメージ グループを削除するには、次のいずれかを入力します。
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[追加 ImageGroup コマンド](using-the-add-imagegroup-command.md) 
 を使用してください。[Get AllImageGroups コマンド](using-the-get-allimagegroups-command.md) 
 の使用[Get ImageGroup コマンド](using-the-get-imagegroup-command.md) 
 の使用[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)
