---
title: Get AllNamespaces コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b77bb80238ee63cc0d71d88592d75850720e33b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440524"
---
# <a name="using-the-get-allnamespaces-command"></a>Get AllNamespaces コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべての名前空間についての情報を表示します。
## <a name="syntax"></a>構文
Windows Server 2008 の場合:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
## <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/Server:<Server name>]  | サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。 |                        |
| [/ContentProvider:<name>] |                                                        名前空間が、指定したコンテンツ プロバイダーに対してのみ表示されます。                                                         |                        |
|      [/ショー: クライアント]      |                            Windows Server 2008 のみサポートされます。 名前空間に接続されているクライアント コンピューターに関する情報を表示します。                             |                        |
|    [/details:Clients]     |                           Windows Server 2008 R2 のみサポートされます。 名前空間に接続されているクライアント コンピューターに関する情報を表示します。                           |                        |
|  [/ExcludedeletePending]  |                                                              一覧から任意の非アクティブ化された転送を除外します。                                                              |                        |

## <a name="BKMK_examples"></a>例
すべての名前空間を表示するには、次のように入力します。
```
wdsutil /Get-AllNamespaces
```
非アクティブ化するものを除くすべての名前空間を表示するには、次のように入力します。
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /details:Clients /ExcludedeletePending
  ```
  #### <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
  [名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
  [サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
