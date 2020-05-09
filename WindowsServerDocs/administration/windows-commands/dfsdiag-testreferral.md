---
title: dfsdiag testreferral
description: 分散ファイルシステム (DFS) の参照を確認する、dfsdiag testreferral コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 23abcd738170d5f53e12ae83c41d632d2d7ac738
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992935"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag testreferral

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム (DFS) の参照を確認します。

- 引数を指定せずに**DFSpath*** パラメーターを使用すると、コマンドは、参照リストにすべての信頼されたドメインが含まれていることを検証します。

- ドメインを指定した場合、コマンドはドメインコントローラー (`dfsdiag /testdcs`) の正常性チェックを実行し、ローカルホストのサイトの関連付けとドメインキャッシュをテストします。

- ドメインと \SYSvol または \NETLOGON を指定した場合、コマンドは同じドメインコントローラーの正常性チェックを実行し、SYSvol または NETLOGON の参照の**有効期限 (TTL)** が既定値の900秒と一致することを確認します。

- 名前空間のルートを指定すると、コマンドは同じドメインコントローラーの正常性チェックを実行し、DFS 構成チェック`dfsdiag /testdfsconfig`() と名前空間の整合性`dfsdiag /testdfsintegrity`チェック () を実行します。

- DFS フォルダー (リンク) を指定すると、コマンドは同じ名前空間のルート正常性チェックを実行し、フォルダーターゲットのサイト構成 (dfsdiag/testsites) を検証し、ローカルホストのサイトの関連付けを検証します。

## <a name="syntax"></a>構文

```
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /DFSpath:`<path to get referrals>` | 以下のいずれかを指定できます。<ul><li>**空白:** 信頼されたドメインのみをテストします。</li><li>`\\Domain:`ドメインコントローラーの参照のみをテストします。</li><li>`\\Domain\SYSvol:`SYSvol 参照のみをテストします。</li><li>`\\Domain\NETLOGON:`NETLOGON 参照のみをテストします。</li><li>`\\<domain or server>\<namespace root>:`名前空間のルート参照のみをテストします。</li><li>`\\<domain or server>\<namespace root>\<DFS folder>:`DFS フォルダー (リンク) の参照のみをテストします。</li></ul> |
| /full | ドメインおよびルートの参照にのみ適用されます。 レジストリと active directory ドメインサービス (AD DS) 間のサイトの関連付け情報の整合性を確認します。 |

## <a name="examples"></a>使用例

*Com\MyNamespace*で分散ファイルシステム (DFS) の参照を確認するには、次のように入力します。

```
dfsdiag /testreferral /DFSpath:\\contoso.com\MyNamespace
```

すべての信頼されるドメインで分散ファイルシステム (DFS) の参照を確認するには、次のように入力します。

```
dfsdiag /testreferral /DFSpath:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [dfsdiag コマンド](dfsdiag.md)
