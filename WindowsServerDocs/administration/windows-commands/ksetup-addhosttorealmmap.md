---
title: ksetup addhosttorealmmap
description: Ksetup addhost almmap コマンドの参照記事。このコマンドは、指定されたホストと領域の間にサービスプリンシパル名 (SPN) マッピングを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 830db84e210b94088e74fd08909f7c47ff84df98
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925575"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhosttorealmmap

指定されたホストと領域の間に、サービスプリンシパル名 (SPN) マッピングを追加します。 このコマンドでは、同じ DNS サフィックスを共有しているホストまたは複数のホストを領域にマップすることもできます。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**の下のレジストリに格納されます。

## <a name="syntax"></a>構文

```
ksetup /addhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| `<hostname>` | ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。 |
| `<realmname>` | 領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 |

### <a name="examples"></a>例

ホストコンピューター *IPops897*を*CONTOSO*領域にマップするには、次のように入力します。

```
ksetup /addhosttorealmmap IPops897 CONTOSO
```

レジストリを調べて、マッピングが意図したとおりに発生したことを確認してください。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup delhostの almmap コマンド](ksetup-delhosttorealmmap.md)
