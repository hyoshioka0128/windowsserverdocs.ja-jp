---
title: ksetup delrealmflags
description: Ksetup delrealmflags コマンドの参照記事。指定された領域から領域フラグを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22053041-1eb4-47f5-bed9-3d5681bcde7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d3c81d1b034f6c53c33271c1c9e61a0fc5d4893
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929175"
---
# <a name="ksetup-delrealmflags"></a>ksetup delrealmflags

指定された領域から領域フラグを削除します。

## <a name="syntax"></a>構文

```
ksetup /delrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<realmname>` | CORP など、大文字の DNS 名を指定します。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または**領域 =** として表示されます。 |

#### <a name="remarks"></a>注釈

- 領域フラグは、Windows Server オペレーティングシステムに基づいていない Kerberos 領域の追加機能を指定します。 Windows Server を実行しているコンピューターは、kerberos サーバーを使用して、Windows Server オペレーティングシステムを実行しているドメインを使用するのではなく、kerberos 領域で認証を管理できます。 このエントリにより、領域の機能が確立され、次のようになります。

| 値 | 領域フラグ | 説明 |
| ----- | ---------- | ----------- |
| 0xF | All | すべての領域フラグが設定されます。 |
| 0x00 | None | 領域フラグが設定されておらず、追加の機能は有効になっていません。 |
| 0x01 | sendaddress | この IP アドレスは、チケット保証チケット内に含まれます。 |
| 0x02 | tcpsupported | この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) の両方がサポートされています。 |
| 0x04 | delegate | この領域のすべてのユーザーが委任に対して信頼されています。 |
| 0x08 | ncsupported | この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。 |
| 0x80 | rc4 | この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。 |

- 領域フラグは、の下のレジストリに格納され `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` ます。 既定では、このエントリはレジストリに存在しません。 [Ksetup addrealmflags コマンド](ksetup-addrealmflags.md)を使用して、レジストリにデータを設定できます。

- **Ksetup**またはの出力を表示することで、使用可能な領域フラグと領域フラグを確認でき `ksetup /dumpstate` ます。

### <a name="examples"></a>例

領域 CONTOSO に使用可能な領域フラグを一覧表示するには、次のように入力します。

```
ksetup /listrealmflags
```

現在セット内にある2つのフラグを削除するには、次のように入力します。

```
ksetup /delrealmflags CONTOSO ncsupported delegate
```

領域フラグが削除されたことを確認するには、「」と入力して `ksetup` 出力を表示し、テキスト「 **realm flags =**」を探します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup listrealmflags コマンド](ksetup-listrealmflags.md)

- [ksetup setrealmflags コマンド](ksetup-setrealmflags.md)

- [ksetup addrealmflags コマンド](ksetup-addrealmflags.md)

- [ksetup dumpstate コマンド](ksetup-dumpstate.md)
