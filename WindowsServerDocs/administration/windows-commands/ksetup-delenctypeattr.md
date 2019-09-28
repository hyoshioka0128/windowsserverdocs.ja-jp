---
title: 'ksetup: delenctypeattr'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3810d83c06b9ea08766451e13390b02b1867c83
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375159"
---
# <a name="ksetupdelenctypeattr"></a>ksetup: delenctypeattr



ドメインの暗号化の種類の属性を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delenctypeattr <DomainName> 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DomainName >|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。|

## <a name="remarks"></a>コメント

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。

正常に完了したか、完了しなかったときに、ステータスメッセージが表示されます。

接続先として使用するドメインを設定するには、 **ksetup/domain \< domainname >** コマンドを実行します。

## <a name="BKMK_Examples"></a>例

このコンピューターに設定されている現在の暗号化の種類を確認します。
```
klist
```
ドメインを mit.contoso.com に設定します。
```
ksetup /domain mit.contoso.com
```
ドメインの暗号化の種類の属性を確認します。
```
ksetup /getenctypeattr mit.contoso.com
```
ドメイン mit.contoso.com の 暗号化の種類の設定属性を削除します。
```
ksetup /delenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)