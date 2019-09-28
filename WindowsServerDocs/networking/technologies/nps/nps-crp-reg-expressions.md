---
title: NPS で正規表現を使用する
description: このトピックでは、Windows Server の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用すると、ネットワークポリシー属性と RADIUS 領域の条件を指定できます。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: jgerend
author: jasongerend
msdate: 08/16/2019
ms.openlocfilehash: 94bb9b54dba046c57c6f82e6a52a71adbcf4ce75
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396376"
---
# <a name="use-regular-expressions-in-nps"></a>NPS で正規表現を使用する

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このトピックでは、Windows Server の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用すると、ネットワークポリシー属性と RADIUS 領域の条件を指定できます。

## <a name="pattern-matching-reference"></a>パターンマッチングのリファレンス

パターンマッチング構文を使用して正規表現を作成する場合は、次の表を参照ソースとして使用できます。 正規表現パターンは、多くの場合、スラッシュ (/) で囲まれていることに注意してください。

|  文字  |  説明  |   例                                                                 |
| ----------- | ------------- | ------------------------------------------------------------------------  |
|     `\ `     | 次に続く文字が特殊文字であるか、文字どおりに解釈される必要があることを示します。  | `/n/ matches the character "n" while the sequence /\n/ matches a line feed or newline character.`  |
|     `^`     |                                                                 入力または行の先頭と一致します。                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    入力または行の末尾と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             直前の文字と0回以上一致します。                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              直前の文字と1回以上一致します。                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              直前の文字と0回または1回一致します。                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           改行文字を除く任意の1文字と一致します。                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         "Pattern" に一致し、一致を記憶します。<br />@No__t-0 および `)` (かっこ) のリテラル文字と一致させるには、`\(` または `\)` を使用します。                         |                                                                 &nbsp;                                                                  |
|   `x | y `  |                                                                               X または y のいずれかに一致します。                                                          |
|   `{n} `    |                                                          N 回の繰り返しに一致し \(n は @ no__t-1negative の整数 @ no__t-2 であることを示します。                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          N 回以上の @no__t に一致します。-0n は、@ no__t-1negative の整数 @ no__t-2 です。                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                N 回以上、m 回以上 \(m と n は、@ no__t-1negative の整数 @ no__t-2 以上に一致します。                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       囲まれた文字 \(a 文字セット @ no__t-1 のいずれかと一致します。                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  @No__t-0a の否定文字セット @ no__t-1 で囲まれていない任意の文字と一致します。                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              単語の境界 @no__t 0 (スペース @ no__t-1 など) と一致します。                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         単語以外境界と一致します。                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       0から9までの数字 @no__t 0 ~ 9 @ no__t の数字と一致します。                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           @No__t-1 @ no__t に相当する nondigit 文字 \( と一致します。                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        フォームフィード文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        改行文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     キャリッジリターン文字と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   スペース、タブ、およびフォームフィードを含む空白文字を @no__t `[ \f\n\r\t\v]` @ no__t-2 に相当します。                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  @No__t-1 @ no__t に等しい、空白以外の任意の文字 \( と一致します。                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           タブ文字と一致します。                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      垂直タブ文字と一致します。                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              @No__t-1 @ no__t に相当するアンダースコア \(equivalent 含む任意の単語文字と一致します。                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           @No__t-2 @ no__t に相当するアンダースコア \( を除く、@ no__t 文字以外の任意の文字と一致します。                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | 記憶された一致文字列 \( @ no__t-1 を参照します。 num は、正の整数 @ no__t-2 です。  このオプションは、属性の操作を構成するときに **[置換]** テキストボックスでのみ使用できます。 |                                       `\1` は、最初に記憶された一致項目に格納されている内容を置き換えます。                                       |
|   `/n/ `    |                      では、ASCII コードを \( @ no__t-1 という正規表現に挿入できます。ここで、n は8進数、16進数、または10進数のエスケープ値 @ no__t-2 です。                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>ネットワークポリシー属性の例

次の例では、パターンマッチング構文を使用してネットワークポリシー属性を指定する方法について説明します。

- 899市外局番内のすべての電話番号を指定する場合、構文は次のようになります。

     `899.*`

- 192.168.1 で始まる IP アドレスの範囲を指定するには、次の構文を使用します。

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>ユーザー名属性の領域名を操作する例

次の例では、パターンマッチング構文を使用して、ユーザー名属性の領域名を操作する方法について説明します。この属性は、接続要求ポリシーのプロパティの **[属性]** タブにあります。

**ユーザー名属性の領域部分を削除するには**

インターネットサービスプロバイダー @no__t 0ISP @ no__t が組織の NPS に接続要求をルーティングする、アウトソーシングされたダイヤルアップシナリオでは、認証要求をルーティングするために、ISP RADIUS プロキシが領域名を必要とする場合があります。 ただし、NPS がユーザー名の領域名の部分を認識しない場合があります。 そのため、組織の NPS に転送する前に、ISP RADIUS プロキシによって領域名を削除する必要があります。

- Find: @microsoft @ no__t-1com

- 次の内容

**@No__t を com\user に置き換えるには<em>、</em>次のように_します。_**

- 検索: `(.*)@(.*)`

- 置換: `$2\$1`



**_Domain\user_を_specific_domain\user_に置き換えるには**

- 検索: `(.*)\\(.*)`

- Replace:*特定*`\$2`



<strong>*ユーザー*を *user@specific_domain</strong>に置き換えるには*

- 検索: `$`

- 置換: @*特定*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>プロキシサーバーによる RADIUS メッセージ転送の例

NPS が RADIUS プロキシとして使用されている場合は、指定された領域名を持つ RADIUS メッセージを一連の RADIUS サーバーに転送するルーティング規則を作成できます。 領域名に基づいて要求をルーティングする場合は、次の構文を使用することをお勧めします。

- **NetBIOS 名**: `WCOAST`
- **Pattern**: `^wcoast\\`

次の例では、wcoast.microsoft.com は、DNS または Active Directory ドメイン wcoast.microsoft.com の一意のユーザープリンシパル名 (UPN) サフィックスです。 NPS プロキシでは、指定されたパターンを使用して、ドメイン NetBIOS 名または UPN サフィックスに基づいてメッセージをルーティングできます。

- **NetBIOS 名**: `WCOAST`
- **UPN サフィックス**: `wcoast.microsoft.com`
- **Pattern**: `^wcoast\\|@wcoast\.microsoft\.com$`


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。
