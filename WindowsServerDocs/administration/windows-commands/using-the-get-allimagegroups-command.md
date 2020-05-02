---
title: get-AllImageGroups
description: Get-AllImageGroups のリファレンストピック。サーバー上のすべてのイメージグループとそれらのイメージグループ内のすべてのイメージに関する情報を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 204618955e91f1c9c9659d37ac3dfe2a01897c51
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720027"
---
# <a name="get-allimagegroups"></a>get-AllImageGroups

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーおよびそれらのイメージ グループのすべてのイメージ上のすべてのイメージ グループに関する情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|詳細/|各イメージからイメージのメタデータを返します。 このパラメーターを使用しない場合、既定の動作は、イメージの名前、説明、および各イメージのファイル名のみを返すには。|
## <a name="examples"></a>例
イメージ グループに関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[のキー追加 imagegroup コマンド](using-the-add-imagegroup-command.md)
を使用して[get](using-the-get-imagegroup-command.md)
imagegroup コマンドを使用して[削除 imagegroup](using-the-remove-imagegroup-command.md)
コマンドを使用して[サブコマンド: セット imagegroup](subcommand-set-imagegroup.md)
