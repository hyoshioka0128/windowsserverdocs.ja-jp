---
title: 削除-AutoaddDevices
description: 自動追加データベースから保留中、拒否、または承認されたコンピューターを削除する、AutoaddDevices の参照記事。
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ccde56c5a0d3edd252048f9cf1e2a4b1fd28a35
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892176"
---
# <a name="delete-autoadddevices"></a>削除-AutoaddDevices

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

自動追加データベースから保留、拒否、または承認されているコンピューターを削除します。 このデータベースは、サーバーでこれらのコンピューターに関する情報を格納します。

## <a name="syntax"></a>構文
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124;ApprovedDevices}|データベースから削除するコンピューターの種類を指定します。 次の 3 種類のいずれかになります。<p>-   **Pendingdevices**は、状態が [保留中] になっているデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**は、データベース内の、状態が拒否のすべてのコンピューターを返します。<br />-   **ApprovedDevices**は、状態が承認済みのすべてのコンピューターを返します。|
## <a name="examples"></a>例
すべての拒否されたコンピューターを削除するには、次のように入力します。
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
すべての承認されたコンピューターを削除するには、次のように入力します。
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[承認-AutoaddDevices コマンド](using-the-approve-autoadddevices-command.md) 
 の使用[Get AutoaddDevices コマンド](using-the-get-autoadddevices-command.md) 
 の使用[拒否 AutoaddDevices コマンドの使用](using-the-reject-autoadddevices-command.md)
