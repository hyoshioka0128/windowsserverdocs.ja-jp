---
title: 'ksetup: addkdc'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66efe4e56007aff39b83c92dfea2afaadcfc0210
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375208"
---
# <a name="ksetupaddkdc"></a>ksetup: addkdc



指定された Kerberos 領域のキー配布センター (KDC) アドレスを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。 この領域は、他の KDC を追加しようとしています。|
|\<KDCName >|KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.microsoft.com など) として指定されます。 KDC 名を省略した場合、DNS は Kdc を検索します。|

## <a name="remarks"></a>コメント

これらのマッピングは、 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**の下のレジストリに格納されます。 Kerberos 領域構成データを複数のコンピューターに展開するには、個々のコンピューターで**ksetup**を明示的に使用するのではなく、セキュリティ構成テンプレートスナップインとポリシー配布を使用します。

新しい領域設定を使用するには、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認するか、またはこのコマンドが意図したとおりに動作したことを確認するには、コマンドプロンプトで**ksetup**を実行し、追加された KDC の出力を確認します。

## <a name="BKMK_Examples"></a>例

Windows 以外の KDC サーバーと、ワークステーションが使用する領域を構成します。
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
前のコマンドと同じコンピューターのコマンドラインで Ksetup ツールを実行して、ローカルコンピューターアカウントのパスワードを "p@sswrd1%" に設定します。 その後、コンピューターを再起動します。
```
Ksetup /setcomputerpassword p@sswrd1%
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)