---
title: ksetup addrealmflags
description: Ksetup addrealmflags コマンドの参照記事。指定された領域に領域フラグを追加します。
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a834d6ce69fede20ed544d858c4f4c46abdf0d68
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888073"
---
# <a name="ksetup-addrealmflags"></a>ksetup addrealmflags

指定された領域に領域フラグを追加します。

## <a name="syntax"></a>構文

```
ksetup /addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<realmname>` | CORP など、大文字の DNS 名を指定します。CONTOSO.COM。 |

#### <a name="remarks"></a>Remarks

- 領域フラグは、Windows Server オペレーティングシステムに基づいていない Kerberos 領域の追加機能を指定します。 Windows Server を実行しているコンピューターは、kerberos サーバーを使用して、Windows Server オペレーティングシステムを実行しているドメインを使用するのではなく、kerberos 領域で認証を管理できます。 このエントリにより、領域の機能が確立され、次のようになります。

| 値 | 領域フラグ | 説明 |
| ----- | ---------- | ----------- |
| 0xF | All | すべての領域フラグが設定されます。 |
| 0x00 | なし | 領域フラグが設定されておらず、追加の機能は有効になっていません。 |
| 0x01 | sendaddress | この IP アドレスは、チケット保証チケット内に含まれます。 |
| 0x02 | tcpsupported | この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) の両方がサポートされています。 |
| 0x04 | delegate | この領域のすべてのユーザーが委任に対して信頼されています。 |
| 0x08 | ncsupported | この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。 |
| 0x80 | rc4 | この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。 |

- 領域フラグは、の下のレジストリに格納され `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` ます。 既定では、このエントリはレジストリに存在しません。 [Ksetup addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

- **Ksetup**またはの出力を表示することで、使用可能な領域フラグと領域フラグを確認でき `ksetup /dumpstate` ます。

### <a name="examples"></a>例

領域 CONTOSO に使用可能な領域フラグを一覧表示するには、次のように入力します。

```
ksetup /listrealmflags
```

CONTOSO 領域に2つのフラグを設定するには、次のように入力します。

```
ksetup /setrealmflags CONTOSO ncsupported delegate
```

現在セットに含まれていないフラグをもう1つ追加するには、次のように入力します。

```
ksetup /addrealmflags CONTOSO SendAddress
```

領域フラグが設定されていることを確認するには、「」と入力し、「 `ksetup` **realm flags =**」というテキストを探します。 テキストが表示されない場合は、フラグが設定されていないことを意味します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup listrealmflags コマンド](ksetup-listrealmflags.md)

- [ksetup setrealmflags コマンド](ksetup-setrealmflags.md)

- [ksetup delrealmflags コマンド](ksetup-delrealmflags.md)

- [ksetup dumpstate コマンド](ksetup-dumpstate.md)
