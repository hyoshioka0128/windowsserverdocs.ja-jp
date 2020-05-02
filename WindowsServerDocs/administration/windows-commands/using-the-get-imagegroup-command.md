---
title: 取得-ImageGroup
description: イメージグループとその中のイメージに関する情報を取得する、get ImageGroup のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30a87085cb935f95a209ffdd78ecf2b9fb45dc15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719898"
---
# <a name="get-imagegroup"></a>取得-ImageGroup

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージ グループおよびその中のイメージに関する情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
mediaGroup:<Image group name>|イメージグループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|詳細/|各イメージのイメージのメタデータを返します。 このパラメーターが使用でない場合は、既定の動作は、イメージの名前、説明、およびファイル名のみを返すには。|
## <a name="examples"></a>例
イメージ グループに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
メタデータを含む情報を表示するには、次のように入力します。
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[のキー追加 imagegroup コマンド](using-the-add-imagegroup-command.md)
を使用して[get allimagegroups コマンド](using-the-get-allimagegroups-command.md)
を使用して[削除 imagegroup コマンド](using-the-remove-imagegroup-command.md)
を使用して[サブコマンド: セット imagegroup](subcommand-set-imagegroup.md)
