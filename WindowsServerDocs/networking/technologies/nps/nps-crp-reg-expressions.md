---
title: NPS で正規表現を使用する
description: このトピックでは、Windows Server 2016 の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用すると、ネットワークポリシー属性と RADIUS 領域の条件を指定できます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3182ce1d0e856b06b143719c488864e9a58fbc0a
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476571"
---
# <a name="use-regular-expressions-in-nps"></a>NPS で正規表現を使用する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 の NPS でのパターンマッチングに正規表現を使用する方法について説明します。 この構文を使用すると、ネットワークポリシー属性と RADIUS 領域の条件を指定できます。

## <a name="pattern-matching-reference"></a>パターンマッチングのリファレンス

パターンマッチング構文を使用して正規表現を作成する場合は、次の表を参照ソースとして使用できます。


|  文字  |                                                                                 説明                                                                                  |                                                                 例                                                                 |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
|     `\`|                                                             次の文字を一致する文字としてマークします。                                                               |                      `/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`                       |
|     `^`     |                                                                 入力または行の先頭と一致します。                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    入力または行の末尾と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             直前の文字と0回以上一致します。                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              直前の文字と1回以上一致します。                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              直前の文字と0回または1回一致します。                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           改行文字を除く任意の1文字と一致します。                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         "Pattern" に一致し、一致を記憶します。<br />リテラル文字`(`と`)` (かっこ) を一致させるに`\(`は`\)`、またはを使用します。                         |                                                                 &nbsp;                                                                  |
|   `x | y `  |                                                                               X または y のいずれかに一致します。                                                          |
|   `{n} `    |                                                          N 回の繰り返し\(に一致します\-n は\)負でない整数です。                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          N 回以上の繰り返し\(に一致します\-n は\)負以外の整数です。                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                少なくとも n に一致し、m \(と n\-の回数は負の\)整数ではありません。                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       文字セット\(\)で囲まれた文字のいずれかと一致します。                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  否定文字セット\(\)で囲まれていない任意の文字と一致します。                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              単語の境界\((スペース\)など) と一致します。                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         単語以外境界と一致します。                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       0 ~ 9\)の\(数字に相当する数字の文字と一致します。                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           と\( `[^0-9]`等価のnondigit文字を\)検索します。                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        フォームフィード文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        改行文字と一致します。                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     キャリッジリターン文字と一致します。                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   スペース、タブ、およびと\( `[ \f\n\r\t\v]` \)同じフォームフィードを含む任意の空白文字と一致します。                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  に相当する\( `[^ \f\n\r\t\v]`空白以外の任意の文字と一致します。\)                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           タブ文字と一致します。                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      垂直タブ文字と一致します。                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              に相当する\( `[A-Za-z0-9_]`アンダースコアを含む任意の単語文字と一致します。\)                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           に相当する\- \(アンダースコアを除く\)、単語以外の任意の文字と一致します。 `[^A-Za-z0-9_]`                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | 記憶された\(一致`?num`を参照します。 num\)は正の整数です。  このオプションは、属性の操作を構成するときに **[置換]** テキストボックスでのみ使用できます。 |                                       `\1`最初に記憶された一致項目に格納されている内容を置き換えます。                                       |
|   `/n/ `    |                      では、ASCII コードを正規表現\( `?n`に挿入できます。ここで、n は8進数、16\)進数、または10進数のエスケープ値です。                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>ネットワークポリシー属性の例

次の例では、パターンマッチング構文を使用してネットワークポリシー属性を指定する方法について説明します。

- 899市外局番内のすべての電話番号を指定する場合、構文は次のようになります。

     `899.*`

- 192.168.1 で始まる IP アドレスの範囲を指定するには、次の構文を使用します。

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>ユーザー名属性の領域名を操作する例

次の例では、パターンマッチング構文を使用して、ユーザー名属性の領域名を操作する方法について説明します。この属性は、接続要求ポリシーのプロパティの **[属性]** タブにあります。

**ユーザー名属性の領域部分を削除するには**

インターネットサービスプロバイダー \(の isp\)が組織の NPS に接続要求をルーティングするアウトソーシングのダイヤルアップシナリオでは、isp RADIUS プロキシが認証要求をルーティングするために領域名を必要とする場合があります。 ただし、NPS がユーザー名の領域名の部分を認識しない場合があります。 そのため、組織の NPS に転送する前に、ISP RADIUS プロキシによって領域名を削除する必要があります。

- 検索: @microsoft \.com

- 次の内容

**を com\user <em>user@example.microsoft.com</em>に置き換えるには、次のように*します。***

- 探す`(.*)@(.*)`

- ら`$2\$1`



***Domain\user*を*specific_domain\user*に置き換えるには**

- 探す`(.*)\\(.*)`

- 置換:*特定*`\$2`



<strong>*ユーザー*をに置き換えるには *user@specific_domain</strong>*

- 探す`$`

- 置換: @*特定*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>プロキシサーバーによる RADIUS メッセージ転送の例

NPS が RADIUS プロキシとして使用されている場合は、指定された領域名を持つ RADIUS メッセージを一連の RADIUS サーバーに転送するルーティング規則を作成できます。 領域名に基づいて要求をルーティングする場合は、次の構文を使用することをお勧めします。

- **NetBIOS 名**:`WCOAST`
- **パターン**:`^wcoast\\`

次の例では、wcoast.microsoft.com は、DNS または Active Directory ドメイン wcoast.microsoft.com の一意のユーザープリンシパル名 (UPN) サフィックスです。 NPS プロキシでは、指定されたパターンを使用して、ドメイン NetBIOS 名または UPN サフィックスに基づいてメッセージをルーティングできます。

- **NetBIOS 名**:`WCOAST`
- **UPN サフィックス**:`wcoast.microsoft.com`
- **パターン**:`^wcoast\\|@wcoast\.microsoft\.com$`


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。
