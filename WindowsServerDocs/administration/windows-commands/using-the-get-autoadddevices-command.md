---
title: Get AutoaddDevices コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 337c8e76923fe243982ba9c10d18f2e5a5e7d9ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885743"
---
# <a name="using-the-get-autoadddevices-command"></a>Get AutoaddDevices コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバー上の自動追加データベース内にあるすべてのコンピューターが表示されます。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|コンピューターに戻すの種類を指定します。<br /><br />-   **PendingDevices**保留中の状態であるデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**の状態を却下するデータベース内のすべてのコンピューターを返します。<br />-   **ApprovedDevices**ことがステータスの承認、データベース内のすべてのコンピューターを返します。|
## <a name="BKMK_examples"></a>例
すべての承認済みのコンピューターを表示するには、次のように入力します。
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
すべての拒否されたコンピューターを表示するには、次のように入力します。
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[AutoaddDevices delete コマンドを使用して](using-the-delete-autoadddevices-command.md)
[承認 AutoaddDevices コマンドを使用して](using-the-approve-autoadddevices-command.md)
 [却下 AutoaddDevices コマンドを使用してください。](using-the-reject-autoadddevices-command.md)
