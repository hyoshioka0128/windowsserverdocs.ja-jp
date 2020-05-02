---
title: 'ksetup: addkdc'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76d592e4f1c32305d6f939a66a6ad42cd582b032
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724764"
---
# <a name="ksetupaddkdc"></a>ksetup: addkdc



指定された Kerberos 領域のキー配布センター (KDC) アドレスを追加します。

## <a name="syntax"></a>構文

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。 この領域は、他の KDC を追加しようとしています。|
|\<KDCName>|KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.microsoft.com など) として指定されます。 KDC 名を省略した場合、DNS は Kdc を検索します。|

## <a name="remarks"></a>Remarks

これらのマッピングは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**の下のレジストリに格納されます。 Kerberos 領域構成データを複数のコンピューターに展開するには、個々のコンピューターで**ksetup**を明示的に使用するのではなく、セキュリティ構成テンプレートスナップインとポリシー配布を使用します。

新しい領域設定を使用するには、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認するか、またはこのコマンドが意図したとおりに動作したことを確認するには、コマンドプロンプトで**ksetup**を実行し、追加された KDC の出力を確認します。

## <a name="examples"></a>例

Windows 以外の KDC サーバーと、ワークステーションが使用する領域を構成します。
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
前のコマンドと同じコンピューターのコマンドラインで Ksetup ツールを実行して、ローカルコンピューターアカウントのパスワードを% にp@sswrd1設定します。 その後、コンピューターを再起動します。
```
Ksetup /setcomputerpassword p@sswrd1%
```

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)