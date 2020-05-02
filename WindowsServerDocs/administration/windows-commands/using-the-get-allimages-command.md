---
title: get-AllImages
description: サーバー上のすべてのイメージに関する情報を取得する get-AllImages のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1f32a1789b22d04b7b61979d0ea49d91f0cf157
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720016"
---
# <a name="get-allimages"></a>get-AllImages

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべてのイメージに関する情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
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
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[追加イメージ](using-the-add-image-command.md)
のコマンドを使用して[コピーイメージ](using-the-copy-image-command.md)
[Using the Export-Image Command](using-the-export-image-command.md)
のコマンドを使用して削除イメージのコマンドを使用して[削除](using-the-remove-image-command.md)
イメージのコマンドを使用して[置換イメージ](using-the-replace-image-command.md)
のコマンドを使用して[サブコマンド: イメージを設定](subcommand-set-image.md)する
