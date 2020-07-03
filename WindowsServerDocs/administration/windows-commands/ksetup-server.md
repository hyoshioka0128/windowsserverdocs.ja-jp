---
title: ksetup server
description: Ksetup server コマンドの参照記事。 Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。 ksetup コマンドによって行われた変更によって、対象のコンピューターが更新されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99c708c3842d1d2d36783db09d60750bb2703670
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926096"
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
