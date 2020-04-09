---
title: 取得-AutoaddDevices
description: Get AutoaddDevices の Windows コマンドに関するトピックでは、Windows 展開サービスサーバー上の自動追加データベースにあるすべてのコンピューターが表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b373fca81769ff1296d0e9a0788fe536c4fc3132
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831185"
---
# <a name="get-autoadddevices"></a>取得-AutoaddDevices

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービスサーバー上の自動追加データベースにあるすべてのコンピューターを表示します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|コンピューターに戻すの種類を指定します。<p>-   **Pendingdevices**は、状態が [保留中] になっているデータベース内のすべてのコンピューターを返します。<br />-   **RejectedDevices**は、データベース内の、状態が拒否のコンピューターをすべて返します。<br />-   **ApprovedDevices**は、承認済みの状態のデータベース内のすべてのコンピューターを返します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
すべての承認済みのコンピューターを表示するには、次のように入力します。
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
すべての拒否されたコンピューターを表示するには、次のように入力します。
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[削除 Autoadddevices コマンドを](using-the-delete-autoadddevices-command.md)使用して
[承認-autoadddevices](using-the-approve-autoadddevices-command.md)コマンドを使用して
[autoadddevices](using-the-reject-autoadddevices-command.md)コマンドを使用します。
