---
title: 'ksetup: delenctypeattr'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c650b973ac34e28394d5b6ec38142a058ad76338
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841765"
---
# <a name="ksetupdelenctypeattr"></a>ksetup: delenctypeattr



ドメインの暗号化の種類の属性を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DomainName >|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。|

## <a name="remarks"></a>コメント

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。

正常に完了したか、完了しなかったときに、ステータスメッセージが表示されます。

接続先として使用するドメインを設定するには、 **ksetup/domain \<DomainName >** コマンドを実行します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)