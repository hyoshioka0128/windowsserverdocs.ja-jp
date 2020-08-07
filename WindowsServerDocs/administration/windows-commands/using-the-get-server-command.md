---
title: get-サーバー
description: 指定された Windows 展開サービスサーバーから情報を取得する、get Server のリファレンス記事です。
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2756fe6b5a7e7790d779b06fa7def9d16c4f775
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896921"
---
# <a name="get-server"></a>get-サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した Windows 展開サービス サーバーから情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/表示: {Config & #124 文字です。イメージと #124 文字です。すべて}|返される情報の種類を指定します。<p>-   **Config**は構成情報を返します。<br />-   **イメージは**、イメージグループ、ブートイメージ、およびインストールイメージに関する情報を返します。<br />-   **All**は、構成情報とイメージ情報を返します。|
|詳細/|このオプションを使用することができます **/Show:Images** または **/Show:All** を指定する各イメージからすべてのイメージのメタデータを返す必要があります。 **/Detailed**オプションが使用されていない場合、既定の動作では、イメージの名前、説明、およびファイル名が返されます。|
## <a name="examples"></a>例
サーバーに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Server /Show:Config
```
サーバーに関する詳細情報を表示するには、次のように入力します。
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[サーバーの無効化コマンド](using-the-disable-server-command.md) 
 の使用[Enable Server コマンド](using-the-enable-server-command.md) 
 の使用[Initialize-Server コマンド](using-the-initialize-server-command.md) 
 の使用[サブコマンド: サーバー](subcommand-set-server.md) 
 の設定[サブコマンド: start-Server](subcommand-start-server.md) 
[サブコマンド: サーバー](subcommand-stop-server.md) 
 の停止[初期化解除サーバーオプション](the-uninitialize-server-option.md)
