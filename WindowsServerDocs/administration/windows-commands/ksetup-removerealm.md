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
ms.openlocfilehash: 3f62208d6576890529be80b1c6cb3cc073a2b4e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853363"
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

領域名は、レジストリ内の 2 つの場所に格納されます。**HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001**と**\CurrentControlSet\Control\Lsa\Kerberos**します。

これは、DNS 情報をリセットし、削除する場合があります、ドメイン コント ローラーを使用できないようにするために、ドメイン コント ローラーから既定の領域名を削除できません。

## <a name="BKMK_Examples"></a>例

スペルミスで領域名を誤って設定"。COM でしょうか。 CORP. をローカル コンピューターCONTOSO です。CON
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
-   [ksetup:setrealm](ksetup-setrealm.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)