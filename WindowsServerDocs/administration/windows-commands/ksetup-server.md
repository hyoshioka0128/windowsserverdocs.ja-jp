---
title: 'ksetup: サーバー'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91549eb78f825264016ec0e03b7035f79132f260
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724594"
---
# <a name="ksetupserver"></a>ksetup: サーバー



Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。これにより、 **ksetup**を使用して行われた変更によって対象のコンピューターが更新されます。

## <a name="syntax"></a>構文

```
ksetup /server <ServerName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ServerName>|IPops897.corp.contoso.com など、構成を有効にするフルコンピューター名。</br>不完全な完全修飾ドメインコンピュータ名が指定されている場合、コマンドは失敗します。|

## <a name="remarks"></a>Remarks

対象のサーバー名を削除する方法はありません。これは、既定のローカルコンピューター名にのみ変更できます。

対象サーバー名は**HKEY_LOCAL_MACHINE \system\controlset001\control\lsa\kerberos**のレジストリに格納されます。 **Ksetup**を使用して報告されることはありません。

## <a name="examples"></a>例

Contoso ドメインに接続されている IPops897 コンピューターで**ksetup**の構成を有効にします。
```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)