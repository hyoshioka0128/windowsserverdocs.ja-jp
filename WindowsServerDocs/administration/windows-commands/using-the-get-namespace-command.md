---
title: get-名前空間
description: カスタム名前空間に関する情報を表示する、名前空間の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 58e84ec5c82ea3c2663b38bd2e53f65f2cf47519
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830885"
---
# <a name="get-namespace"></a>get-名前空間

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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

|               パラメーター               |                                                                                                                                                                                         説明                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Namespace:<Namespace name>      | 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<p>-展開サーバー: 名前空間名の構文は/namspace: WDS:<ImageGroup>/<ImageName>/<Index>です。 例: **WDS:ImageGroup1/install.wim/1**<br />-トランスポート サーバー: この値は、サーバー上で作成されたときに、名前空間に付けた名前と一致する必要があります。 |
|        [/Server:<Server name>]        |                                                                                                             サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                              |
| [/Show: クライアント] または [詳細: クライアント] |                                                                                                                                                  指定した名前空間に接続されているクライアント コンピューターに関する情報を表示します。                                                                                                                                                  |

## <a name="examples"></a><a name=BKMK_examples></a>例
名前空間に関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
名前空間と接続されているクライアントに関する情報を表示するには、次のいずれかを入力します。
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のポイント](command-line-syntax-key.md)
  [get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
  [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
  [名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
  [サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
