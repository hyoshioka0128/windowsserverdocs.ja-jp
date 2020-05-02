---
title: 'ksetup: removerealm'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb7bf4663594a6c164d6495a9ba4cd81942afb79
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724602"
---
# <a name="ksetupremoverealm"></a>ksetup: removerealm



指定された領域のすべての情報をレジストリから削除します。

## <a name="syntax"></a>構文

```
ksetup /removerealm <RealmName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。|

## <a name="remarks"></a>Remarks

領域名は、レジストリの2つの場所 ( **HKEY_LOCAL_MACHINE \system\controlset001**と**\CurrentControlSet\Control\Lsa\Kerberos**) に格納されます。

ドメインコントローラーから既定の領域名を削除することはできません。これにより、DNS 情報がリセットされ、削除すると、ドメインコントローラーが使用できなくなる可能性があります。

## <a name="examples"></a>例

ローカルコンピューター上の .COM のスペルを誤った領域名を CORP に設定します。製薬.短所
```
ksetup /setrealm CORP.CONTOSO.CON
```
この誤った領域名をローカルコンピューターから削除します。
```
ksetup /removerealm CORP.CONTOSO.CON
```
**Ksetup**を実行して削除を確認し、出力を確認します。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)