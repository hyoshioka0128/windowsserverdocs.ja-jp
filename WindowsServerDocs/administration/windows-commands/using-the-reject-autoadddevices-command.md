---
title: AutoaddDevices を拒否する
description: Windows コマンドに関するトピックでは、管理者の承認が保留されているコンピューターを拒否します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39bdddbbc169a0a0810fcc67e95224360858b728
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830655"
---
# <a name="reject-autoadddevices"></a>AutoaddDevices を拒否する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを拒否します。 自動追加ポリシーを有効にすると、不明なコンピューター (事前登録されていないコンピューター) がイメージをインストールする前に、管理者の承認が必要になります。 このポリシーを有効にするには、サーバーのプロパティ ページの  **PXE 応答** タブを使用します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/RequestId: < 要求 ID と #124 文字です。すべて >|保留中のコンピューターに割り当てられた要求 ID を指定します。 保留中のすべてのコンピューターを拒否するには指定 **すべて**です。|
## <a name="examples"></a><a name=BKMK_examples></a>例
1 台のコンピューターを拒否するには、次のように入力します。
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
すべてのコンピューターを拒否するには、次のように入力します。
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[承認 autoadddevices](using-the-approve-autoadddevices-command.md)コマンドを使用して
[削除-autoadddevices](using-the-delete-autoadddevices-command.md)コマンド
使用して[取得 autoadddevices コマンド](using-the-get-autoadddevices-command.md)を使用します。
