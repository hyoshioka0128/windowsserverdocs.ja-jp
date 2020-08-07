---
title: gpfixup
description: Gpfixup コマンドの参照記事。ドメイン名変更操作後のグループポリシーオブジェクトおよびグループポリシーリンク内のドメイン名の依存関係を修正します。
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9379efe545544028980cf570de30bc6d3d816c81
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888563"
---
# <a name="gpfixup"></a>gpfixup

ドメイン名変更操作後のグループポリシーオブジェクトおよびグループポリシーリンク内のドメイン名の依存関係を修正します。 このコマンドを使用するには、サーバーマネージャーを使用してグループポリシー管理を機能としてインストールする必要があります。

## <a name="syntax"></a>構文

```
gpfixup [/v]
[/olddns:<olddnsname> /newdns:<newdnsname>]
[/oldnb:<oldflatname> /newnb:<newflatname>]
[/dc:<dcname>] [/sionly]
[/user:<username> [/pwd:{<password>|*}]] [/?]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| /v | 詳細なステータスメッセージを表示します。 このパラメーターを使用しない場合は、エラーメッセージ、または**成功**または**失敗**を示す概要ステータスメッセージのみが表示されます。 |
| /olddns:`<olddnsname>` | ドメイン `<olddnsname>` の名前変更操作によってドメインの dns 名が変更されるときに、名前が変更されたドメインの古い DNS 名を指定します。 このパラメーターは、 **/newdns**パラメーターを使用して新しいドメイン dns 名を指定する場合にのみ使用できます。 |
| /newdns:`<newdnsname>` | ドメイン `<newdnsname>` の名前変更操作によってドメインの dns 名が変更されるときに、名前が変更されたドメインの新しい dns 名を指定します。 このパラメーターは、古いドメイン DNS 名を指定するために、 **/olddns**パラメーターも使用する場合にのみ使用できます。 |
| /oldnb:`<oldflatname>` | ドメインの名前変更 `<oldflatname>` 操作によってドメインの netbios 名が変更されるときに、名前が変更されたドメインの古い NetBIOS 名を指定します。 このパラメーターは、 **/newnb**パラメーターを使用して新しいドメイン NetBIOS 名を指定する場合にのみ使用できます。 |
| /newnb:`<newflatname>` | ドメインの名前変更 `<newflatname>` 操作によってドメインの netbios 名が変更されるときに、名前が変更されたドメインの新しい netbios 名を指定します。 このパラメーターは、 **/oldnb**パラメーターを使用して古いドメイン NetBIOS 名を指定する場合にのみ使用できます。 |
| /dc`<dcname>` | という名前のドメインコントローラー `<dcname>` (DNS 名または NetBIOS 名) に接続します。 `<dcname>`次のいずれかの方法で示されているように、ドメインディレクトリパーティションの書き込み可能なレプリカをホストする必要があります。<ul><li>DNS 名には、 `<newdnsname>` **/dns dns**名を使用します。</li><li>`<newflatname>` **/Newnb**を使用した NetBIOS 名</br>このパラメーターが使用されていない場合は、またはによって示される名前を変更したドメイン内の任意のドメインコントローラーに接続でき `<newdnsname>` `<newflatname>` ます。</li></ul> |
| /sionly | は、管理されているソフトウェアのインストール (グループポリシーのソフトウェアインストール拡張機能) に関連するグループポリシー修正プログラムのみを実行します。 Gpo のグループポリシーリンクと SYSVOL パスを修正する操作をスキップします。 |
| /user`<username>` |このコマンドは、ユーザーのセキュリティコンテキストで実行 `<username>` されます。ここで、 `<username>` は domain\user という形式になっています。 このパラメーターを使用しない場合、このコマンドはログインしているユーザーとして実行されます。 |
| /pwd`{<password> | *}` | ユーザーのパスワードを指定します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

### <a name="examples"></a>例

この例では、DNS 名を**MyOldDnsName**から**MyNewDnsName**に、NetBIOS 名を**MyOldNetBIOSName**から**MyNewNetBIOSName**に変更したドメインの名前変更操作を既に実行していることを前提としています。

この例では、 **gpfixup**コマンドを使用して、gpo とリンクに埋め込まれている古いドメイン名を更新することによって、 **Mydcdnsname 名**という名前のドメインコントローラーに接続し、gpo とグループポリシーリンクを修復します。 状態およびエラー出力は、 **gpfixup .log**という名前のファイルに保存されます。

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

この例は前の例と同じですが、ドメインの名前変更操作中にドメインの NetBIOS 名が変更されていないことを前提としています。

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Active Directory ドメインの名前変更の管理](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794869(v=ws.10))
