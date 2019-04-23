---
title: 却下 AutoaddDevices コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af46aec7c8f02b3600983b66bd1b0ac6f5dd1dcc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852563"
---
# <a name="using-the-reject-autoadddevices-command"></a>却下 AutoaddDevices コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを拒否します。 自動追加ポリシーが有効にすると (事前登録されていないもの) の不明なコンピューターにイメージをインストールする前に管理者の承認が必要です。 このポリシーを使用して有効にすることができます、 **PXE 応答**サーバー プロパティ ページのタブ。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/RequestId: < 要求 ID と #124 文字です。すべて >|保留中のコンピューターに割り当てられた要求 ID を指定します。 保留中のすべてのコンピューターを拒否するには指定 **すべて**です。|
## <a name="BKMK_examples"></a>例
1 台のコンピューターを拒否するには、次のように入力します。
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
すべてのコンピューターを拒否するには、次のように入力します。
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[承認 AutoaddDevices コマンドを使用して](using-the-approve-autoadddevices-command.md)
[AutoaddDevices delete コマンドを使用して](using-the-delete-autoadddevices-command.md)
 [Get AutoaddDevices コマンドを使用してください。](using-the-get-autoadddevices-command.md)
