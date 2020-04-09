---
title: 'ksetup: addkdc'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bb31cbc8ba7920c4ba609f86202e2e62a705078
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841835"
---
# <a name="ksetupaddkdc"></a>ksetup: addkdc



指定された Kerberos 領域のキー配布センター (KDC) アドレスを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。 この領域は、他の KDC を追加しようとしています。|
|\<KDCName >|KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.microsoft.com など) として指定されます。 KDC 名を省略した場合、DNS は Kdc を検索します。|

## <a name="remarks"></a>コメント

これらのマッピングは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**の下のレジストリに格納されます。 Kerberos 領域構成データを複数のコンピューターに展開するには、個々のコンピューターで**ksetup**を明示的に使用するのではなく、セキュリティ構成テンプレートスナップインとポリシー配布を使用します。

新しい領域設定を使用するには、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認するか、またはこのコマンドが意図したとおりに動作したことを確認するには、コマンドプロンプトで**ksetup**を実行し、追加された KDC の出力を確認します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

Windows 以外の KDC サーバーと、ワークステーションが使用する領域を構成します。
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
前のコマンドと同じコンピューターのコマンドラインで Ksetup ツールを実行して、ローカルコンピューターアカウントのパスワードを p@sswrd1% に設定します。 その後、コンピューターを再起動します。
```
Ksetup /setcomputerpassword p@sswrd1%
```

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)