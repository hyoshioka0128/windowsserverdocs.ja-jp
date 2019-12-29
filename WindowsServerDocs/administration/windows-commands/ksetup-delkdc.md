---
title: 'ksetup: delkdc'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b918f8c2fa0ec09c2aae77517a0ee2c9e77ce2dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375138"
---
# <a name="ksetupdelkdc"></a>ksetup: delkdc



Kerberos 領域のキー配布センター (KDC) 名のインスタンスを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。 **ksetup**を実行すると、既定の領域として表示されます。 これは、他の KDC を削除しようとしているこの領域です。|
|\<KDCName >|KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.contoso.com など) として指定します。|

## <a name="remarks"></a>コメント

これらのマッピングは、 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**のレジストリに格納されます。 複数のコンピューターから領域構成データを削除するには、個々のコンピューターで**ksetup**を明示的に使用するのではなく、セキュリティ構成テンプレートスナップインとポリシー配布を使用します。

Windows 2000 Server Service Pack 1 (SP1) 以前を実行しているコンピューターでは、変更された領域設定の構成を使用する前に、コンピューターを再起動する必要があります。

コンピューターの既定の領域名を確認するか、このコマンドが意図したとおりに動作していることを確認するには、コマンドプロンプトで**ksetup**を実行し、削除された KDC が一覧に存在していないことを確認します。

## <a name="BKMK_Examples"></a>例

このコンピューターのセキュリティ要件が変更されたため、Windows 領域と Windows 以外の領域との間のリンクを削除する必要があります。 まず、削除するアソシエーションを決定し、既存の関連付けの出力を生成します。
```
ksetup
```
次のコマンドを使用して、関連付けを削除します。
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)