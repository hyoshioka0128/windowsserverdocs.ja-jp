---
title: NPS で正規表現を使用します。
description: このトピックでは、パターン マッチングに Windows Server 2016 で NPS の正規表現の使用について説明します。 次の構文を使用すると、ネットワーク ポリシーの属性と RADIUS 領域の条件を指定します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f84173f1f51be9fd44995dc41f759bbea4fb3539
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-regular-expressions-in-nps"></a>NPS で正規表現を使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、パターン マッチングに Windows Server 2016 で NPS の正規表現の使用について説明します。 次の構文を使用すると、ネットワーク ポリシーの属性と RADIUS 領域の条件を指定します。

## <a name="pattern-matching-reference"></a>パターン マッチング リファレンス

構文のパターン マッチングに正規表現を作成するときに、次の表を参照ソースとして使用できます。

|文字|説明|使用例|
|---------|-----------|-------|
|`\`  |一致する文字として次の文字をマークします。 |`/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`  |
|`^`  |入力または行の先頭に一致します。 | &nbsp; |
|`$`  |入力または行の末尾に一致します。 | &nbsp; |
|`*`  |前の文字の 0 個以上の時間と一致します。 |`/zo*/ matches either "z" or "zoo."` |
|`+`  |前の文字を 1 つまたは複数の時刻と一致します。 |`/zo+/ matches "zoo" but not "z."` |
|`?`  |前の文字の 0 または 1 回を一致します。 |`/a?ve?/ matches the "ve" in "never."` |
|`.`  |改行文字を除く任意の 1 文字と一致します。  | &nbsp; |
|`( pattern )`  |"をパターン"と一致してマッチを記録します。   |`To match ( ) (parentheses), use "\(" or "\)".`  |
|' x | Y '  |X または y のいずれかと一致します。  |'/z|餌ですか?「動物園」または「食料」と一致する]。` |
|`{ n } `  |厳密に n 回一致 \ (n は以外負 integer\)。  |`/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`  |
|`{ n ,}`  |少なくとも n 回一致 \ (n は以外負 integer\)。  |`/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.`  |
|`{ n , m }`  |少なくとも n m 回一致 \ (m と n は以外負 integers\)。  |`/o{1,3}/ matches the first three instances of the letter o in "fooooood."`  |
|`[ xyz ]`  |囲まれた文字列のいずれかと一致する \(a character set\) します。  |`/[abc]/ matches the "a" in "plain."`  |
|`[^ xyz ]`  |含まれていない任意の文字と一致する \ (負の文字になって)。  |`/[^abc]/ matches the "p" in "plain."`  |
|`\b`  |Word の境界に一致 \ (たとえば、space\)。  |`/ea*r\b/ matches the "er" in "never early."`  |
|`\B`  |単語の境界と一致します。  |`/ea*r\B/ matches the "ear" in "never early."`  |
|`\d`  |数字と一致する \ (0 ~ 9\ 桁と同等)。  | &nbsp; |
|`\D`  |数字以外の文字と一致する \ (に相当`[^0-9]`\)。  | &nbsp; |
|`\f`  |フォーム フィード文字に一致します。  | &nbsp; |
|`\n`  |ライン フィード文字に一致します。  | &nbsp; |
|`\r`  |文字と一致します。  | &nbsp; |
|`\s`  |スペース、タブ、およびフィード フォームを含む任意の空白文字と一致する \ (に相当`[ \f\n\r\t\v]`\)。  | &nbsp; |
|`\S`  |任意の空白以外の文字と一致する \ (に相当`[^ \f\n\r\t\v]`\)。  | &nbsp; |
|`\t`  |タブ文字と一致します。  | &nbsp; |
|`\v`  |垂直タブ文字と一致します。  | &nbsp; |
|`\w`  |任意の文字、アンダー スコアを含むと一致する \ (に相当`[A-Za-z0-9_]`\)。  | &nbsp; |
|`\W`  |アンダー スコアを除く任意の以外 word 文字と一致する \ (に相当`[^A-Za-z0-9_]`\)。  | &nbsp; |
|`\ num`  |覚えの一致を指します \ (`?num`がテンキーの正 integer\)。  このオプションでのみ使用できます、**置換**属性の操作を構成するときに、テキスト ボックス。| `\1` 記憶している最初の一致に格納されているものに置き換えます。  |
|`/ n / `  |により、ASCII コードの正規表現への挿入 \ (`?n`n は、8 進数、16 進数、または 10 進数のエスケープ value\)。  | &nbsp; |

## <a name="examples-for-network-policy-attributes"></a>ネットワーク ポリシーの属性の例

次の例では、ネットワーク ポリシーの属性を指定するパターン マッチング構文の使用について説明します。

- 構文は 899 市外局番内のすべての電話番号を指定するには。

     `899.*`

- 構文は 192.168.1 で始まる範囲の IP アドレスを指定するには。

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>ユーザー名属性で領域名を操作するための例

次の例では、ユーザー名属性では、上にある領域名を操作するパターン マッチング構文の使用方法を説明する、**属性**接続要求ポリシーのプロパティ] タブ。

**ユーザー名属性の領域の部分を削除するには**

外部委託ダイヤルアップ シナリオではインターネット サービス プロバイダーの \(ISP\) ルート接続要求するには、組織内の NPS サーバー、ISP RADIUS プロキシが認証要求をルーティングする領域名を必要があります。 ただし、NPS サーバーは、ユーザー名の領域名部分を認識しません可能性があります。 そのため、組織の NPS サーバーに転送される前に、ISP RADIUS プロキシで領域名を削除する必要があります。

- 検索:@microsoft\.com

- 置き換えてください。

**置き換える*user@example.microsoft.com*で*example.microsoft.com\user***

- 検索:`(.*)@(.*)`

- 置き換えてください。`$2\$1`



**置き換える*domain \user*で*specific_domain\user***

- 検索:`(.*)\\(.*)`

- [置換]:*置き換える*`\$2`



**置き換える*ユーザー*で*user@specific_domain***

- 検索:`$`

- [置換]: @*置き換える*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>RADIUS プロキシ サーバーによってメッセージの転送の例

NPS を RADIUS プロキシとして使用する場合は、一連の RADIUS サーバーの指定された領域名を持つ RADIUS メッセージを転送ルーティングの規則を作成することができます。 領域名に基づいて要求を送信することをお勧め構文を次に示します。

- **NetBIOS 名 **: `WCOAST`
- **パターン **:      `^wcoast\\`

次の例では、wcoast.microsoft.com は wcoast.microsoft.com DNS または Active Directory ドメインの一意のユーザー プリンシパル名 (UPN) サフィックスです。NPS プロキシは、指定されたパターンを使用して、ドメインの NetBIOS 名またはユーザー プリンシパル名サフィックスを基にメッセージをルーティングできます。

- **NetBIOS 名 **: `WCOAST`
- **UPN サフィックス **:   `wcoast.microsoft.com`
- **パターン **:      `^wcoast\\|@wcoast\.microsoft\.com$`


NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
