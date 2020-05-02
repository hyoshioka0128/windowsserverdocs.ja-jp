---
title: get-サーバー
description: 指定された Windows 展開サービスサーバーから情報を取得する、get Server のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a760371797af8eb95da386a3a5b9dbb0dcf7ba3c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719738"
---
# <a name="get-server"></a>get-サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した Windows 展開サービス サーバーから情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
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
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文](command-line-syntax-key.md)
[の](using-the-disable-server-command.md)
キーを使用して無効にするサーバーのコマンドを使用して、[有効](using-the-enable-server-command.md)
にするサーバーのコマンドを使用して、サーバーの[初期化](using-the-initialize-server-command.md)
コマンドを使用してサブコマンド: サーバーを[設定](subcommand-set-server.md)
[Subcommand: start-Server](subcommand-start-server.md)
[Subcommand: stop-Server](subcommand-stop-server.md)
するサブコマンド: サーバー[の](the-uninitialize-server-option.md)サーバーを指定します。
