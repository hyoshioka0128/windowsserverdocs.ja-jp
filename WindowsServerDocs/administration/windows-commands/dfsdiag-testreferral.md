---
title: dfsdiag TestReferral
description: DFS (分散ファイルシステム) の参照を確認する、dfsdiag TestReferral の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5c0a75d557d816ac9e19a1e22b3273195b93f53
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846250"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag TestReferral

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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

|パラメーター|説明|
|-------|--------|
| /DFSpath:<path for getting referrals>|この DFS パスは、次のいずれかになります。<p>-   \(blank\): 信頼されたドメインをテストします。<br />-   \\\\ドメイン: ドメインコントローラーの紹介。<br />-   \\\\ドメイン\\SYSvol: SYSvol 参照。<br />-   \\\\NETLOGON: NETLOGON の紹介に \\Doma です。<br />-   \\\\<Domain or server>\\<Namespace Root>: 名前空間のルート参照。<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS フォルダー \(リンク\) 参照します。|
|/Full|ドメインおよびルートの参照にのみ適用されます。 レジストリと active directory ドメインサービス \(AD DS\)間のサイトの関連付け情報の整合性を確認します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

```
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace
```

```
dfsdiag /TestReferral /DFSpath:
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)


