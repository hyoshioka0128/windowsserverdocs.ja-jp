---
title: 名前空間の get コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 607fb758db64cfc938a08b070b520fe2950aa482
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363083"
---
# <a name="using-the-get-namespace-command"></a>名前空間の get コマンドを使用してください。

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
## <a name="parameters"></a>パラメーター

|               パラメーター               |                                                                                                                                                                                         説明                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Namespace:<Namespace name>      | 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<br /><br />-展開サーバー: 名前空間名の構文は/namspace: WDS:<ImageGroup>/<ImageName>/<Index>です。 例: **WDS:ImageGroup1/install.wim/1**<br />-トランスポート サーバー: この値は、サーバー上で作成されたときに、名前空間に付けた名前と一致する必要があります。 |
|        [/Server:<Server name>]        |                                                                                                             サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                              |
| [/Show: クライアント] または [詳細: クライアント] |                                                                                                                                                  指定した名前空間に接続されているクライアント コンピューターに関する情報を表示します。                                                                                                                                                  |

## <a name="BKMK_examples"></a>例
名前空間に関する情報を表示するには、次のように入力します。
```
wdsutil /Get-Namespace /Namespace:"Custom Auto 1"
```
名前空間と接続されているクライアントに関する情報を表示するには、次のいずれかを入力します。
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /details:Clients`
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
  [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
  [名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
  [サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
