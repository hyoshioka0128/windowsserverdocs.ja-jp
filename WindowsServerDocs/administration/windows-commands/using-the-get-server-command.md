---
title: get-サーバー
description: 指定された Windows 展開サービスサーバーから情報を取得する、get Server の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65903dc89730eb9d1da23be31ecc1909daece9c4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830845"
---
# <a name="get-server"></a>get-サーバー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した Windows 展開サービス サーバーから情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/表示: {Config & #124 文字です。イメージと #124 文字です。すべて}|返される情報の種類を指定します。<p>-   構成は構成情報を**返します。**<br />-   **イメージ**は、イメージグループ、ブートイメージ、およびインストールイメージに関する情報を返します。<br />**すべて**-   は、構成情報とイメージ情報を返します。|
|詳細/|このオプションを使用することができます **/Show:Images** または **/Show:All** を指定する各イメージからすべてのイメージのメタデータを返す必要があります。 **/Detailed**オプションが使用されていない場合、既定の動作では、イメージの名前、説明、およびファイル名が返されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
サーバーに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Server /Show:Config
```
サーバーに関する詳細情報を表示するには、次のように入力します。
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[、無効にするサーバーのコマンドを使用して](using-the-disable-server-command.md)
[、有効にするサーバーのコマンドを使用して](using-the-enable-server-command.md)
[Initialize サーバー コマンドを使用して](using-the-initialize-server-command.md)
[サブコマンド: サーバーを設定する](subcommand-set-server.md)
[サブコマンド: サーバーを起動](subcommand-start-server.md)
[サブコマンド: サーバーの停止](subcommand-stop-server.md)
[非サーバー オプション](the-uninitialize-server-option.md)
