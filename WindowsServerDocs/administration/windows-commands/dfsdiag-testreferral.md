---
title: dfsdiag TestReferral
description: 分散ファイルシステム (DFS) の参照を確認する、dfsdiag TestReferral のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b4c616181d367a8a95efe6484f74af0ff88cc5f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719567"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag TestReferral

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム (DFS) の参照を確認します。

- 引数を指定せずに DFSpath パラメーターを使用すると、このコマンドは、参照リストにすべての信頼されたドメインが含まれているかどうかを検証します。

- ドメインを指定すると、コマンドはドメインコントローラー (dfsdiag/testdcs) の正常性チェックを実行し、ローカルホストのサイトの関連付けとドメインキャッシュをテストします。

- ドメイン、\SYSvol、または \NETLOGON を指定すると、ドメインを指定したときと同じ正常性チェックを実行するだけでなく、SYSvol または NETLOGON の参照の有効期限 (\ TTL) が既定値の900秒と一致するかどうかが確認されます。

- 名前空間のルートを指定すると、ドメインを指定したときと同じ正常性チェックを実行できるだけでなく、DFS 構成チェック (dfsdiag/TestDFSConfig) と名前空間の整合性チェック (dfsdiag/TestDFSIntegrity) が実行されます。

- DFS フォルダー (リンク) を指定するときに、名前空間のルートを指定した場合と同じ正常性チェックを実行するだけでなく、コマンドはフォルダーターゲットのサイト構成 (dfsdiag/testsites) を検証し、ローカルホストのサイトの関連付けを検証します。

## <a name="syntax"></a>構文

```
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|-------|--------|
| /DFSpath:<path for getting referrals>|この DFS パスは、次のいずれかになります。<p>-   \(blank\): 信頼されたドメインをテストします。<br />-   \\\\ドメイン: ドメインコントローラーの紹介。<br />-   \\\\ドメイン\\SYSvol: sysvol 参照。<br />-   \\\\Netlogon の doma: NETLOGON の\\紹介。<br />-   \\\\<Domain or server>\\<Namespace Root>: 名前空間のルート参照。<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS フォルダー \(リンク\)の紹介。|
|/Full|ドメインおよびルートの参照にのみ適用されます。 レジストリと active directory ドメインサービス\(AD DS\)間のサイトの関連付け情報の整合性を確認します。|

## <a name="examples"></a>例

```
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace
```

```
dfsdiag /TestReferral /DFSpath:
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)


