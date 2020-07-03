---
title: get-AllImageGroups
description: Get AllImageGroups のリファレンス記事。サーバー上のすべてのイメージグループとそれらのイメージグループ内のすべてのイメージに関する情報を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5863ecc22ff5b96024cb3ba2bdbcac9f7ae8455
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935187"
---
# <a name="get-allimagegroups"></a>get-AllImageGroups

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーおよびそれらのイメージ グループのすべてのイメージ上のすべてのイメージ グループに関する情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|詳細/|各イメージからイメージのメタデータを返します。 このパラメーターを使用しない場合、既定の動作は、イメージの名前、説明、および各イメージのファイル名のみを返すには。|
## <a name="examples"></a>例
イメージ グループに関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[追加 ImageGroup コマンド](using-the-add-imagegroup-command.md) 
 を使用してください。[Get ImageGroup コマンド](using-the-get-imagegroup-command.md) 
 の使用[削除 ImageGroup コマンド](using-the-remove-imagegroup-command.md) 
 を使用してください。[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)
