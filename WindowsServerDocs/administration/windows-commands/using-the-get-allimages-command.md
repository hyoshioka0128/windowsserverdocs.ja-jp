---
title: get-AllImages
description: サーバー上のすべてのイメージに関する情報を取得する get-AllImages のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9834552ebe6395f13333e81fbc2996a8ff49f39c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935177"
---
# <a name="get-allimages"></a>get-AllImages

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべてのイメージに関する情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/表示: {ブートと #124 文字です。インストールと #124 文字です。LegacyRis & #124 文字です。すべて}|-   **ブート**では、ブートイメージのみが返されます。<br />-   **インストール**では、インストールイメージと、そのイメージを含むイメージグループに関する情報が返されます。<br />-   **LegacyRis**は、リモートインストールサービス (RIS) のイメージのみを返します。<br />-   **すべて**のブートイメージ情報、インストールイメージ情報 (イメージグループに関する情報を含む)、および RIS イメージ情報が返されます。|
|詳細/|各イメージからすべてのイメージのメタデータを返すことを示します。 このオプションを使用しない場合、既定の動作は、イメージの名前、説明、およびファイル名のみを返すには。|
## <a name="examples"></a>例
イメージに関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[[イメージの追加] コマンド](using-the-add-image-command.md) 
 の使用[コピーイメージのコマンド](using-the-copy-image-command.md) 
 を使用する[Export-Image コマンド](using-the-export-image-command.md) 
 の使用[イメージの削除コマンド](using-the-remove-image-command.md) 
 を使用する[置換イメージのコマンド](using-the-replace-image-command.md) 
 を使用する[サブコマンド: イメージの設定](subcommand-set-image.md)
