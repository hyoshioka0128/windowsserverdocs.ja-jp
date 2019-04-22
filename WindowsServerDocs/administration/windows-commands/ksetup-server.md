---
title: ksetup:server
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f370d4dede278e1facdda829503ea3793502b9e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814573"
---
# <a name="ksetupserver"></a>ksetup:server



使用して、変更が行われるため、Windows オペレーティング システムを実行するコンピューターの名前を指定することができます**ksetup**ターゲット コンピューターに更新されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /server <ServerName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<サーバー名 >|フル コンピューター名を構成は IPops897.corp.contoso.com など、適用されます。</br>不完全な完全修飾されている場合は、ドメインのコンピューター名が指定されて、コマンドは失敗します。|

## <a name="remarks"></a>注釈

は、対象のサーバー名を削除する方法はありません既定値は、ローカル コンピューターの名前にのみ変更できます。

対象のサーバー名がレジストリに格納されている**HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos**します。 使用しては報告されません**ksetup**します。

## <a name="BKMK_Examples"></a>例

ように、 **ksetup**構成は、Contoso ドメインに接続されている IPops897 コンピューターで有効になります。
```
ksetup /server IPops897.corp.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)