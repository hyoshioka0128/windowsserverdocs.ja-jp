---
title: NPS で正規表現を使用する
description: このトピックでは、Windows Server の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用し、ネットワーク ポリシー属性および RADIUS 領域の条件を指定できます。
manager: brianlic
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: jgerend
author: jasongerend
msdate: 08/16/2019
ms.openlocfilehash: b2df170153e2848239a8846e58a84981bc9ad12e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969389"
---
# <a name="use-regular-expressions-in-nps"></a>NPS で正規表現を使用する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このトピックでは、Windows Server の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用し、ネットワーク ポリシー属性および RADIUS 領域の条件を指定できます。

## <a name="pattern-matching-reference"></a>パターン マッチングの参照情報

次の表は、パターン マッチング構文を使用した正規表現を作成する際の参照情報として活用できます。 正規表現パターンは、多くの場合、スラッシュ (/) で囲まれていることに注意してください。

|  文字  |  説明  |   例                                                                 |
| ----------- | ------------- | ------------------------------------------------------------------------  |
|     `\ `     | 次に続く文字が特殊文字であるか、文字どおりに解釈される必要があることを示します。  | `/n/ matches the character "n" while the sequence /\n/ matches a line feed or newline character.`  |
|     `^`     |                                                                 入力または行の最初と一致します。                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    入力または行の末尾と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             直前の文字の 0 回または複数回の繰り返しと一致します。                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              直前の文字の 1 回以上の繰り返しと一致します。                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              直前の文字が 0 回または 1 回出現する文字と一致します。                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           復帰改行文字以外の任意の 1 文字と一致します。                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         "Pattern" に一致し、一致を記憶します。<br />リテラル文字と (かっこ) を一致させるに `(` `)` は、またはを使用し `\(` `\)` ます。                         |                                                                 &nbsp;                                                                  |
|   `x | y `  |                                                                               X または y のいずれかに一致します。                                                          |
|   `{n} `    |                                                          N 回の繰り返し \( に一致します n は負でない \- 整数 \) です。                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          N 回以上の繰り返しに一致 \( します n は負以外の \- 整数 \) です。                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                少なくとも n に一致し、m \( と n の回数は \- 負の整数では \) ありません。                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       文字セットで囲まれた文字のいずれかと一致し \( \) ます。                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  否定文字セットで囲まれていない任意の文字と一致 \( \) します。                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              単語 \( の境界 (スペースなど) と一致 \) します。                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         単語以外の境界と一致します。                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       \(0 ~ 9 の数字に相当する数字の文字と一致し \) ます。                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           と等価の nondigit 文字を検索 \( `[^0-9]` \) します。                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        フォーム フィード文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        改行文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     復帰文字と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   スペース、タブ、およびと同じフォームフィードを含む任意の空白文字と一致 \( `[ \f\n\r\t\v]` \) します。                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  に相当する空白以外の任意の文字と一致 \( `[^ \f\n\r\t\v]` \) します。                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           タブ文字と一致します。                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      垂直タブ文字と一致します。                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              に相当するアンダースコアを含む任意の単語文字と一致 \( `[A-Za-z0-9_]` \) します。                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           \-に相当するアンダースコアを除く、単語以外の任意の文字と一致 \( `[^A-Za-z0-9_]` \) します。                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | 記憶された一致を参照し \( `?num` ます。 num は正の整数 \) です。  このオプションは、属性の操作を構成するときに [**置換**] テキストボックスでのみ使用できます。 |                                       `\1`最初に記憶された一致項目に格納されている内容を置き換えます。                                       |
|   `/n/ `    |                      では、ASCII コードを正規表現に挿入でき \( `?n` ます。ここで、n は8進数、16進数、または10進数のエスケープ値 \) です。                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>ネットワーク ポリシー属性の例

次に、パターン マッチング構文を使用してネットワーク ポリシー属性を指定する方法の例を説明します。

- 市外局番が 899 の電話番号をすべて指定するには、次の構文を使用します。

     `899.*`

- 192.168.1 で始まる IP アドレスの範囲を指定するには、次の構文を使用します。

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>ユーザー名 属性で領域名を扱う例

次の例では、パターンマッチング構文を使用して、ユーザー名属性の領域名を操作する方法について説明します。この属性は、接続要求ポリシーのプロパティの [**属性**] タブにあります。

**[ユーザー名] 属性の領域部分を削除するには**

インターネットサービスプロバイダーの isp が組織の NPS に接続要求をルーティングするアウトソーシングのダイヤルアップシナリオでは、 \( \) isp RADIUS プロキシが認証要求をルーティングするために領域名を必要とする場合があります。 ただし、NPS がユーザー名の領域名の部分を認識しない場合があります。 そのため、組織の NPS に転送する前に、ISP RADIUS プロキシによって領域名を削除する必要があります。

- 検索: @microsoft \. com

- 置換前のコード:

**を com\user に置き換えるには、 <em>user@example.microsoft.com</em> 次のように_します。_**

- 探す`(.*)@(.*)`

- ら`$2\$1`



**_Domain\user_を_specific_domain 場所:_ に置き換えるには**

- 探す`(.*)\\(.*)`

- 置換: *specific_domain*`\$2`



<strong>*ユーザー*をに置き換えるには*user@specific_domain</strong>*

- 探す`$`

- 置換: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>プロキシ サーバーによる RADIUS メッセージの転送の例

NPS を RADIUS プロキシとして使用している場合、一連の RADIUS サーバーに対して指定した領域名を使い、RADIUS メッセージを転送するルーティング規則を作成できます。 次に、領域名に基づいて要求をルーティングするために推奨される構文を挙げます。

- **NetBIOS 名**:`WCOAST`
- **パターン**:`^wcoast\\`

次の例では、wcoast.microsoft.com は、DNS または Active Directory ドメイン wcoast.microsoft.com の一意のユーザープリンシパル名 (UPN) サフィックスです。 NPS プロキシでは、指定されたパターンを使用して、ドメイン NetBIOS 名または UPN サフィックスに基づいてメッセージをルーティングできます。

- **NetBIOS 名**:`WCOAST`
- **UPN サフィックス**:`wcoast.microsoft.com`
- **パターン**:`^wcoast\\|@wcoast\.microsoft\.com$`


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。
