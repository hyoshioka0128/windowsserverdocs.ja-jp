---
title: 取得-AutoaddDevices
description: Get AutoaddDevices のリファレンストピックでは、Windows 展開サービスサーバー上の自動追加データベースにあるすべてのコンピューターが表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c15836fa81c694aa9295d0a98376f4bef3125243
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719988"
---
# <a name="get-autoadddevices"></a>取得-AutoaddDevices

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービスサーバー上の自動追加データベースにあるすべてのコンピューターを表示します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|コンピューターに戻すの種類を指定します。<p>-   **Pendingdevices**は、状態が [保留中] になっているデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**は、データベース内の、状態が拒否のすべてのコンピューターを返します。<br />-   **ApprovedDevices**は、状態が承認済みのデータベース内のすべてのコンピューターを返します。|
## <a name="examples"></a>例
すべての承認済みのコンピューターを表示するには、次のように入力します。
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
すべての拒否されたコンピューターを表示するには、次のように入力します。
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[delete autoadddevices コマンド](using-the-delete-autoadddevices-command.md)
を使用して[承認 autoadddevices](using-the-approve-autoadddevices-command.md)
コマンドを使用して[拒否 autoadddevices コマンド](using-the-reject-autoadddevices-command.md)を使用して
