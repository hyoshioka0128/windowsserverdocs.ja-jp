---
title: 'ksetup: サーバー'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd05fd294640c63e633b7b866307197ae6770476
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374961"
---
# <a name="ksetupserver"></a>ksetup: サーバー



Windows オペレーティングシステムを実行しているコンピューターの名前を指定できます。これにより、 **ksetup**を使用して行われた変更によって対象のコンピューターが更新されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /server <ServerName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ServerName >|IPops897.corp.contoso.com など、構成を有効にするフルコンピューター名。</br>不完全な完全修飾ドメインコンピュータ名が指定されている場合、コマンドは失敗します。|

## <a name="remarks"></a>コメント

対象のサーバー名を削除する方法はありません。これは、既定のローカルコンピューター名にのみ変更できます。

対象サーバー名は、 **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos**のレジストリに格納されます。 **Ksetup**を使用して報告されることはありません。

## <a name="BKMK_Examples"></a>例

Contoso ドメインに接続されている IPops897 コンピューターで**ksetup**の構成を有効にします。
```
ksetup /server IPops897.corp.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)