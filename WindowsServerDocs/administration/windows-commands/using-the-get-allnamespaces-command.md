---
title: get-AllNamespaces
description: サーバー上のすべての名前空間に関する情報を表示する、get-AllNamespaces のリファレンス記事です。
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 470aab904f9404b8dbe99409445b0533fa83fedd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896397"
---
# <a name="get-allnamespaces"></a>get-AllNamespaces

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべての名前空間についての情報を表示します。

## <a name="syntax"></a>構文
Windows Server 2008:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
### <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/Server:<Server name>]  | サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。 |                        |
| [/ContentProvider:<name>] |                                                        名前空間が、指定したコンテンツ プロバイダーに対してのみ表示されます。                                                         |                        |
|      [/ショー: クライアント]      |                            Windows Server 2008 のみサポートされます。 名前空間に接続されているクライアント コンピューターに関する情報を表示します。                             |                        |
|    [詳細: クライアント]     |                           Windows Server 2008 R2 のみサポートされます。 名前空間に接続されているクライアント コンピューターに関する情報を表示します。                           |                        |
|  [/Excludedeletepending]  |                                                              一覧から任意の非アクティブ化された転送を除外します。                                                              |                        |

## <a name="examples"></a>例
すべての名前空間を表示するには、次のように入力します。
```
wdsutil /Get-AllNamespaces
```
非アクティブ化するものを除くすべての名前空間を表示するには、次のように入力します。
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md) 
  [新しい名前空間のコマンド](using-the-new-namespace-command.md) 
   を使用する[名前空間の削除コマンド](using-the-remove-namespace-command.md) 
   を使用する[サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
