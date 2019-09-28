---
title: 拒否 AutoaddDevices コマンドの使用
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2e8fda3037ef921e2b2a7a0acb616b8a67545ff9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363003"
---
# <a name="using-the-reject-autoadddevices-command"></a>拒否 AutoaddDevices コマンドの使用

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを拒否します。 自動追加ポリシーを有効にすると、不明なコンピューター (事前登録されていないコンピューター) がイメージをインストールする前に、管理者の承認が必要になります。 このポリシーを有効にするには、サーバーのプロパティ ページの  **PXE 応答** タブを使用します。
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
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[@no__t 承認-](using-the-approve-autoadddevices-command.md)autoadddevices コマンドを使用して[削除-](using-the-delete-autoadddevices-command.md)autoadddevices コマンド 
 を使用して[取得 autoadddevices](using-the-get-autoadddevices-command.md)コマンドを使用します。
