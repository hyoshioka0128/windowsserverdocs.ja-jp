---
title: ksetup listrealmflags
description: Ksetup listrealmflags コマンドの参照記事。 ksetup によって報告される使用可能な領域フラグを一覧表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d094b7d627885d25313b73bb51a1bbeeec2832d6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933684"
---
# <a name="ksetup-listrealmflags"></a>ksetup listrealmflags

**Ksetup**によって報告される可能性のある領域フラグを一覧表示します。

## <a name="syntax"></a>構文

```
ksetup /listrealmflags
```

### <a name="remarks"></a>Remarks

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

## <a name="examples"></a>例

このコンピューターの既知の領域フラグの一覧を表示するには、次のように入力します。

```
ksetup /listrealmflags
```

**Ksetup**で認識されない領域フラグを設定するには、次のように入力します。

```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```

**もしくは**

```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup addrealmflags コマンド](ksetup-addrealmflags.md)

- [ksetup setrealmflags コマンド](ksetup-setrealmflags.md)

- [ksetup delrealmflags コマンド](ksetup-delrealmflags.md)
