---
title: get-名前空間
description: カスタム名前空間に関する情報を表示する、名前空間のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76980d2add9ee9b7584812c9d366408f8770b681
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719748"
---
# <a name="get-namespace"></a>get-名前空間

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタムの名前空間についての情報を表示します。

## <a name="syntax"></a>構文
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/Show:Clients]
```
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/details:Clients]
```
### <a name="parameters"></a>パラメーター

|               パラメーター               |                                                                                                                                                                                         [説明]                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      空間<Namespace name>      | 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<p>-展開サーバー: 名前空間名の構文は、/namspace: WDS<ImageGroup>/<ImageName>/<Index>: です。 例: **WDS:ImageGroup1/install.wim/1**<br />-トランスポート サーバー: この値は、サーバー上で作成されたときに、名前空間に付けた名前と一致する必要があります。 |
|        [/Server:<Server name>]        |                                                                                                             サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                              |
| [/Show: クライアント] または [詳細: クライアント] |                                                                                                                                                  指定した名前空間に接続されているクライアント コンピューターに関する情報を表示します。                                                                                                                                                  |

## <a name="examples"></a>例
名前空間に関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
名前空間と接続されているクライアントに関する情報を表示するには、次のいずれかを入力します。
- Windows Server 2008:`wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2:`wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [get allnamespaces](using-the-get-allnamespaces-command.md)
  [Using the new-Namespace Command](using-the-new-namespace-command.md)
  コマンドを使用して、名前空間の削除コマンドを使用して名前空間[を削除](using-the-remove-namespace-command.md)
  するコマンドを使用して[サブコマンド: 開始-名前空間](subcommand-start-namespace.md)
