---
title: 'ksetup: removerealm'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 11858d8a24d4f125c83b3e4092ac48f336a9ef0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374947"
---
# <a name="ksetupremoverealm"></a>ksetup: removerealm



指定された領域のすべての情報をレジストリから削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。|

## <a name="remarks"></a>コメント

領域名は、レジストリの2つの場所に格納されます。**HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001**と **\CurrentControlSet\Control\Lsa\Kerberos**。

ドメインコントローラーから既定の領域名を削除することはできません。これにより、DNS 情報がリセットされ、削除すると、ドメインコントローラーが使用できなくなる可能性があります。

## <a name="BKMK_Examples"></a>例

ローカルコンピューターの ".com" に対して ".com" というスペルを間違えて、誤って領域名を設定しています。製薬.短所
```
ksetup /setrealm CORP.CONTOSO.CON
```
この誤った領域名をローカルコンピューターから削除します。
```
ksetup /removerealm CORP.CONTOSO.CON
```
**Ksetup**を実行して削除を確認し、出力を確認します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)