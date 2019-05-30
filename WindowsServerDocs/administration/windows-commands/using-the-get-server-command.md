---
title: Get Server コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da8bf0fc6e31bd8d0079933f1d7c529c4fe96f42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870983"
---
# <a name="using-the-get-server-command"></a>Get Server コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した Windows 展開サービス サーバーから情報を取得します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/表示: {Config &#124;文字です。イメージと #124 文字です。すべて}|返される情報の種類を指定します。<br /><br />-   **Config**構成情報を返します。<br />-   **イメージ**イメージ グループ、ブート イメージ、およびインストール イメージに関する情報を返します。<br />-   **すべて**構成情報とイメージ情報を返します。|
|[/詳細]|このオプションを使用することができます **/Show:Images** または **/Show:All** を指定する各イメージからすべてのイメージのメタデータを返す必要があります。 場合、**詳細/** オプションが使用されない場合、既定の動作は、イメージの名前、説明、およびファイル名を返すには。|
## <a name="BKMK_examples"></a>例
サーバーに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Server /Show:Config
```
サーバーに関する詳細情報を表示するには、次のように入力します。
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[、無効にするサーバーのコマンドを使用して](using-the-disable-server-command.md)
[、有効にするサーバーのコマンドを使用して](using-the-enable-server-command.md)
[Initialize サーバー コマンドを使用して](using-the-initialize-server-command.md)
[サブコマンド: サーバーを設定する](subcommand-set-server.md)
[サブコマンド: サーバーを起動](subcommand-start-server.md)
[サブコマンド: サーバーの停止](subcommand-stop-server.md)
[非サーバー オプション](the-uninitialize-server-option.md)
