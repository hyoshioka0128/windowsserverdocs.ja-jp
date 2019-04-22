---
title: Delete AutoaddDevices コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8b3375418c5ce0b02e187e292cac5b168f0de5dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813503"
---
# <a name="using-the-delete-autoadddevices-command"></a>Delete AutoaddDevices コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

拒否、または自動追加データベースから承認保留中であるコンピューターを削除します。 このデータベースは、サーバーでこれらのコンピューターに関する情報を格納します。
## <a name="syntax"></a>構文
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124;ApprovedDevices}|データベースから削除するコンピューターの種類を指定します。 次の 3 種類のいずれかになります。<br /><br />-   **PendingDevices**保留中の状態であるデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**の状態を却下するデータベース内のすべてのコンピューターを返します。<br />-   **ApprovedDevices**で返されるの状態であるすべてのコンピュータを承認します。|
## <a name="BKMK_examples"></a>例
すべての拒否されたコンピューターを削除するには、次のように入力します。
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
すべての承認されたコンピューターを削除するには、次のように入力します。
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[承認 AutoaddDevices コマンドを使用して](using-the-approve-autoadddevices-command.md)
[get AutoaddDevices コマンドを使用して](using-the-get-autoadddevices-command.md)
 [却下 AutoaddDevices コマンドを使用して](using-the-reject-autoadddevices-command.md)
