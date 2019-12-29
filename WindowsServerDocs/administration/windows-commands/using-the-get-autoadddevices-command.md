---
title: Get AutoaddDevices コマンドの使用
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fa30a8ebd73164dc3d8ab267c3deb0739aa4b700
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363249"
---
# <a name="using-the-get-autoadddevices-command"></a>Get AutoaddDevices コマンドの使用

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービスサーバー上の自動追加データベースにあるすべてのコンピューターを表示します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|コンピューターに戻すの種類を指定します。<br /><br />-   **Pendingdevices**は、状態が [保留中] になっているデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**は、データベース内の、状態が拒否のコンピューターをすべて返します。<br />-   **ApprovedDevices**は、状態が承認済みのデータベース内のすべてのコンピューターを返します。|
## <a name="BKMK_examples"></a>例
すべての承認済みのコンピューターを表示するには、次のように入力します。
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
すべての拒否されたコンピューターを表示するには、次のように入力します。
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[削除-](using-the-delete-autoadddevices-command.md)autoadddevices コマンドを使用して 
 を使用して[承認-autoadddevices](using-the-approve-autoadddevices-command.md)コマンド 
 を使用します。 autoadddevices コマンド[を使用](using-the-reject-autoadddevices-command.md)します。
