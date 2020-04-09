---
title: 'ksetup: サーバー'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7889e1a03d3c0eec1958bf1d6356c67e9371a80f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841445"
---
# <a name="ksetupserver"></a>ksetup: サーバー



Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。これにより、 **ksetup**を使用して行われた変更によって対象のコンピューターが更新されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /server <ServerName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ServerName >|IPops897.corp.contoso.com など、構成を有効にするフルコンピューター名。</br>不完全な完全修飾ドメインコンピュータ名が指定されている場合、コマンドは失敗します。|

## <a name="remarks"></a>コメント

対象のサーバー名を削除する方法はありません。これは、既定のローカルコンピューター名にのみ変更できます。

対象サーバー名は**HKEY_LOCAL_MACHINE \system\controlset001\control\lsa\kerberos**のレジストリに格納されます。 **Ksetup**を使用して報告されることはありません。

## <a name="examples"></a><a name=BKMK_Examples></a>例

Contoso ドメインに接続されている IPops897 コンピューターで**ksetup**の構成を有効にします。
```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)