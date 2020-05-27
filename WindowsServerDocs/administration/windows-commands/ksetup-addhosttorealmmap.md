---
title: ksetup addhostの almmap
description: Ksetup addhost almmap コマンドのリファレンストピックでは、指定されたホストと領域の間にサービスプリンシパル名 (SPN) マッピングを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee2639a5bb071bdd3d6ac3f6373e881c18f3bf9a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818112"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhostの almmap

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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup delhostの almmap コマンド](ksetup-delhosttorealmmap.md)
