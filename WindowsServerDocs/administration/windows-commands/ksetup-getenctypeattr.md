---
title: 'ksetup: getenctypeattr'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8363113d4fbb310d98b40d852b36a00f20320e6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724632"
---
# <a name="ksetupgetenctypeattr"></a>ksetup: getenctypeattr



ドメインの暗号化の種類の属性を取得します。

## <a name="syntax"></a>構文

```
ksetup /getenctypeattr <DomainName> 
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<DomainName>|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。|

## <a name="remarks"></a>Remarks

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。

コマンドが成功または失敗した場合は、正常に完了したか失敗したときにステータスメッセージが表示されます。

接続先として使用するドメインを設定するには、 **ksetup/Domain \<DomainName>** コマンドを実行します。

## <a name="examples"></a>例

ドメインの暗号化の種類の属性を確認します。
```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>その他のリファレンス

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)