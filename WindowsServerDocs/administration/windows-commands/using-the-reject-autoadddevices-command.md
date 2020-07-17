---
title: AutoaddDevices を拒否する
description: 管理者の承認が保留されているコンピューターを拒否する [自動追加デバイスを拒否する] の参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b678f7a9fc875dfeebf735475db3adfb7ad9ae7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932419"
---
# <a name="reject-autoadddevices"></a>AutoaddDevices を拒否する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを拒否します。 自動追加ポリシーを有効にすると、不明なコンピューター (事前登録されていないコンピューター) がイメージをインストールする前に、管理者の承認が必要になります。 このポリシーを有効にするには、[サーバーのプロパティ] ページの [ **PXE 応答**] タブを使用します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/RequestId: < 要求 ID と #124 文字です。すべて >|保留中のコンピューターに割り当てられた要求 ID を指定します。 保留中のすべてのコンピューターを拒否するには指定 **すべて**です。|
## <a name="examples"></a>例
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
[承認-AutoaddDevices コマンド](using-the-approve-autoadddevices-command.md) 
 の使用[Delete AutoaddDevices コマンド](using-the-delete-autoadddevices-command.md) 
 の使用[Get AutoaddDevices コマンドの使用](using-the-get-autoadddevices-command.md)
