---
title: ksetup setrealm
description: Kerberos 領域の名前を設定する ksetup setrealm コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03b33977f57e187a8bea69be78c1e9c094b9a73e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817282"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Kerberos 領域の名前を設定します。

> [!IMPORTANT]
> ドメインコントローラーでの Kerberos 領域の設定はサポートされていません。 これを行おうとすると、警告とコマンドエラーが発生します。

## <a name="syntax"></a>構文

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<DNSdomainname>` | CORP など、大文字の DNS 名を指定します。CONTOSO.COM。 完全修飾ドメイン名を使用することも、名前の単純な形式を使用することもできます。 DNS 名に大文字を使用しない場合は、続行するかどうかを確認するメッセージが表示されます。 |

### <a name="examples"></a>例

このコンピューターの領域を特定のドメイン名に設定し、ドメインコントローラー以外のアクセスを CONTOSO Kerberos 領域のみに制限するには、次のように入力します。

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
