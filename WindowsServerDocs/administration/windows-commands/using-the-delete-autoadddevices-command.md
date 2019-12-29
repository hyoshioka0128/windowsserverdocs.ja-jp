---
title: Delete AutoaddDevices コマンドの使用
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e914506f731685b17117b359359f60ea91992dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363539"
---
# <a name="using-the-delete-autoadddevices-command"></a>Delete AutoaddDevices コマンドの使用

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

自動追加データベースから保留、拒否、または承認されているコンピューターを削除します。 このデータベースは、サーバーでこれらのコンピューターに関する情報を格納します。
## <a name="syntax"></a>構文
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124;ApprovedDevices}|データベースから削除するコンピューターの種類を指定します。 次の 3 種類のいずれかになります。<br /><br />-   **Pendingdevices**は、状態が [保留中] になっているデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**は、データベース内の、状態が拒否のコンピューターをすべて返します。<br />-   **ApprovedDevices**は、状態が承認済みのすべてのコンピューターを返します。|
## <a name="BKMK_examples"></a>例
すべての拒否されたコンピューターを削除するには、次のように入力します。
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
すべての承認されたコンピューターを削除するには、次のように入力します。
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[@no__t 承認-](using-the-approve-autoadddevices-command.md)autoadddevices コマンドを使用して[取得-autoadddevices](using-the-get-autoadddevices-command.md)コマンド 
 を使用します。-5-[autoadddevices](using-the-reject-autoadddevices-command.md)コマンドを使用します。
