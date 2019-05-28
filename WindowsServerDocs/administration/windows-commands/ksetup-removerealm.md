---
title: ksetup:removerealm
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 579b0772e4642389b90aa370dad80a3eebea9d34
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564717"
---
# <a name="ksetupremoverealm"></a>ksetup:removerealm



指定された領域のすべての情報をレジストリから削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM、およびこれが既定の領域として一覧表示と**ksetup**が実行します。|

## <a name="remarks"></a>注釈

領域名は、レジストリ内の 2 つの場所に格納されます。**HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001**と **\CurrentControlSet\Control\Lsa\Kerberos**します。

これは、DNS 情報をリセットし、削除する場合があります、ドメイン コント ローラーを使用できないようにするために、ドメイン コント ローラーから既定の領域名を削除できません。

## <a name="BKMK_Examples"></a>例

誤って領域名".COM"のスペルが間違ってによって、ローカル コンピューター上に設定 corp.CONTOSO です。CON
```
ksetup /setrealm CORP.CONTOSO.CON
```
ローカル コンピューターからそのエラーのある領域名を削除します。
```
ksetup /removerealm CORP.CONTOSO.CON
```
実行して、削除の確認**ksetup**出力を確認します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)