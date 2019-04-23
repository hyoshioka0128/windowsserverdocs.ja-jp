---
title: ksetup:setrealm
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa6b2a21904ec4dae1e60def5bd36647291b1af6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877403"
---
# <a name="ksetupsetrealm"></a>ksetup:setrealm



Kerberos 領域の名前を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setrealm <DNSDomainName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DNSDomainName>|DNS ドメイン名は、完全修飾ドメイン名または単純なドメイン名の形式にできます。|

## <a name="remarks"></a>注釈

DNS ドメイン名のパラメーターは大文字で入力する必要があります。 それ以外の場合、 **ksetup**コマンドで引き続き確認が求められます。

ドメイン コント ローラーで Kerberos 領域を設定することはサポートされていません。 しようと、警告とコマンド エラー。

## <a name="BKMK_Examples"></a>例

CONTOSO の Kerberos 領域にのみ、非ドメイン コント ローラーによってアクセスを制限する特定のドメイン名には、このコンピューターの領域を設定します。
```
ksetup /setrealm CONTOSO
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [ksetup:removerealm](ksetup-removerealm.md)