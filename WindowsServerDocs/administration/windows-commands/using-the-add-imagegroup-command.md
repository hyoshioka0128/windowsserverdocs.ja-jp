---
title: ImageGroup の追加
description: Windows 展開サービスサーバーにイメージグループを追加する、ImageGroup の参照記事。
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 611425c7c3ff997009e16792fea1924a403f364e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896596"
---
# <a name="add-imagegroup"></a>ImageGroup の追加

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバーには、イメージ グループを追加します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaGroup:<Image group name>|追加するイメージ グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
## <a name="examples"></a>例
イメージ グループを追加するには、次のいずれかを入力します。
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[Get AllImageGroups コマンド](using-the-get-allimagegroups-command.md) 
 の使用[Get ImageGroup コマンド](using-the-get-imagegroup-command.md) 
 の使用[削除 ImageGroup コマンド](using-the-remove-imagegroup-command.md) 
 を使用してください。[サブコマンド: セット ImageGroup](subcommand-set-imagegroup.md)
