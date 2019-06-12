---
title: NPS で正規表現を使用する
description: このトピックでは、Windows Server 2016 で NPS に一致するパターンの正規表現の使用について説明します。 この構文を使用して、ネットワーク ポリシー属性および RADIUS 領域の条件を指定することができます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f51bfb1c767c0eee3aed64df9879dd0a97f2f7b1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446163"
---
# <a name="use-regular-expressions-in-nps"></a>NPS で正規表現を使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Windows Server 2016 で NPS に一致するパターンの正規表現の使用について説明します。 この構文を使用して、ネットワーク ポリシー属性および RADIUS 領域の条件を指定することができます。

## <a name="pattern-matching-reference"></a>パターン マッチングの参照情報

パターン マッチング構文を使用して正規表現を作成するときに、次の表を参照元として使用できます。


|  文字  |                                                                                 説明                                                                                  |                                                                 例                                                                 |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
|     `\`     |                                                              次の文字を一致する文字としてマークします。                                                               |                      `/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`                       |
|     `^`     |                                                                 入力または行の先頭に一致します。                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    入力または行の末尾に一致します。                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             直前の文字を 0 回以上一致します。                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              直前の文字を 1 回以上一致します。                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              前の文字は 0 または 1 回を一致します。                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           改行文字を除く任意の 1 文字と一致します。                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         「パターン」と一致して、一致を記憶します。<br />リテラル文字に一致する`(`と`)`(かっこ) を使用して、`\(`または`\)`します。                         |                                                                 &nbsp;                                                                  |
|     \`x     |                                                                                     y \`                                                                                     |                                                         X または y のいずれかと一致します。                                                          |
|   `{n} `    |                                                          正確に n 回の繰り返しと一致する\(n は、非\-負の整数\)します。                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          N 回以上と一致する\(n は、非\-負の整数\)します。                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                N 以上 m 回の繰り返しと一致する\(m と n は非\-負の整数\)します。                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       囲まれた文字列のいずれかと一致する\(文字セット\)します。                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  囲まれていない任意の文字と一致する\(負の文字セット\)します。                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              ワード境界と一致する\(スペースなど、\)します。                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         単語の境界と一致します。                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       数字の文字と一致する\(0 ~ 9 桁の数字に相当\)します。                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           数字以外の文字と一致する\(等しく`[^0-9]`\)します。                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        フォーム フィード文字に一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        ライン フィード文字に一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     キャリッジ リターン文字と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   スペース、タブ、フォーム フィードなど、任意の空白文字と一致する\(等しく`[ \f\n\r\t\v]`\)します。                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  空白以外の任意の文字と一致する\(等しく`[^ \f\n\r\t\v]`\)します。                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           タブ文字と一致します。                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      垂直タブ文字と一致します。                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              アンダー スコアを含む、任意の単語文字と一致する\(等しく`[A-Za-z0-9_]`\)します。                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           以外の一致\-単語文字、アンダー スコアを除く\(等しく`[^A-Za-z0-9_]`\)します。                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | 記憶された文字を指す\( `?num`、num は正の整数\)します。  このオプションでのみ使用できます、**置換**属性の操作を構成するときに、テキスト ボックス。 |                                       `\1` 記憶されている最初の一致に格納されているものに置き換えます。                                       |
|   `/n/ `    |                      正規表現に ASCII コードを挿入できるように\( `?n`n は 8 進数、16 進数、または 10 進数のエスケープ値を\)します。                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>ネットワーク ポリシー属性の例

次の例では、ネットワーク ポリシー属性を指定するパターン マッチング構文の使用について説明します。

- 市外局番が 899 の電話番号をすべてを指定するには、構文は次のとおりです。

     `899.*`

- 192. 168.1 で始まる範囲の IP アドレスを指定するには、構文は次のとおりです。

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>ユーザー名 属性で領域名を操作するための例

次の例では、説明の上にある [ユーザー名] 属性の領域名を操作するパターン マッチング構文を使用、**属性**タブで、接続要求ポリシーのプロパティ。

**ユーザー名 属性の領域の部分を削除するには**

外部委託ダイヤルアップ シナリオでは、インターネット サービス プロバイダーにする\(ISP\)組織の NPS に接続要求をルーティング、ISP RADIUS プロキシが認証要求をルーティングする領域名を必要があります。 ただし、NPS は、ユーザー名の領域名部分を認識しない可能性が。 そのため、組織の NPS に転送される前に、ISP RADIUS プロキシが領域名を削除してください。

- 検索: @microsoft \.com

- 次の内容

**置換する<em>user@example.microsoft.com</em>で*example.microsoft.com\user***

- 検索:`(.*)@(.*)`

- 置き換えます。`$2\$1`



**置換する*domain \user*で*specific_domain\user***

- 検索:`(.*)\\(.*)`

- 置換:*置換*`\$2`



<strong>置換する*ユーザー*で *user@specific_domain</strong>*

- 検索:`$`

- 置換: @*置換*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>プロキシ サーバーが RADIUS メッセージの転送の例

NPS が RADIUS プロキシとして使用する場合は、一連の RADIUS サーバーの指定された領域名を持つ RADIUS メッセージを転送するルーティング規則を作成することができます。 領域名に基づいて要求を送信することをお勧めの構文を次に示します。

- **NetBIOS 名**: `WCOAST`
- **パターン**:      `^wcoast\\`

次の例では、wcoast.microsoft.com は DNS や Active Directory ドメイン wcoast.microsoft.com の一意のユーザー プリンシパル名 (UPN) サフィックスは。 指定されたパターンを使用して、NPS プロキシは、NetBIOS ドメイン名または UPN サフィックスに基づいてメッセージをルーティングできます。

- **NetBIOS 名**: `WCOAST`
- **UPN サフィックス**:   `wcoast.microsoft.com`
- **パターン**:      `^wcoast\\|@wcoast\.microsoft\.com$`


NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
