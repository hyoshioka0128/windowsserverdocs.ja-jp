---
title: ksetup server
description: Ksetup server コマンドの参照記事。 Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。 ksetup コマンドによって行われた変更によって、対象のコンピューターが更新されます。
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2bfa894468ee05b983d8c0122a1738982ef4d909
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887784"
---
# <a name="ksetup-server"></a>ksetup server

Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。そのため、 **ksetup**コマンドによって行われた変更によって、対象のコンピューターが更新されます。

対象サーバー名は、の下のレジストリに格納され `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos` ます。 このエントリは、 **ksetup**コマンドを実行したときには報告されません。

> [!IMPORTANT]
> 対象のサーバー名を削除する方法はありません。 代わりに、既定のローカルコンピューター名に戻すことができます。

## <a name="syntax"></a>構文

```
ksetup /server <servername>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<servername>` | *IPops897.corp.contoso.com*など、構成を有効にするフルコンピューター名を指定します。<p>不完全な完全修飾ドメインコンピュータ名が指定されている場合、コマンドは失敗します。 |

### <a name="examples"></a>例

Contoso ドメインに接続されている*IPops897*コンピューターで**ksetup**の構成を有効にするには、次のように入力します。

```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)
