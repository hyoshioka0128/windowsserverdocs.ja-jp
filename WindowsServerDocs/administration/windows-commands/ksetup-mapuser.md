---
title: ksetup:mapuser
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5bc68fe9e8f4cbb9869cb74e4eb20a3400eb56ad
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437964"
---
# <a name="ksetupmapuser"></a>ksetup:mapuser



Kerberos プリンシパルの名前は、アカウントにマップします。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /mapuser <Principal> <Account>
```

### <a name="parameters"></a>パラメーター

|  パラメーター   |                                                   説明                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<プリンシパル > |              すべてのプリンシパルの完全修飾ドメイン名たとえば、mike@corp.CONTOSO.COMします。              |
|  \<アカウント >  | どのアカウントまたはセキュリティ グループ名ゲスト、ドメインのユーザーや管理者など、このコンピューター上に存在します。 |

## <a name="remarks"></a>注釈

アカウントを具体的に識別できます、ドメインのゲストなど。 または、ワイルドカード文字 (*) を使用して、すべてのアカウントを含めることができます。

アカウント名を省略した場合は、指定したプリンシパルのマッピングが削除されます。

有効な Kerberos チケットがある場合、コンピューターは特定の領域のプリンシパルを認証のみです。

使用**ksetup**せず、パラメーターや引数を現在のマップの設定と既定の領域を参照してください。

外部キー配布センター (KDC) と領域の構成に変更されるたびに、この設定が変更されたコンピューターの再起動が必要です。

## <a name="BKMK_Examples"></a>例

CONTOSO の Kerberos 領域内の Mike Danseglio のアカウントをこのコンピューターは、このコンピューターを認証することがなく、組み込みのゲスト アカウントのメンバーのすべての権限を許可 (英語) でゲスト アカウントにマップします。
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
Mike Danseglio のアカウントを CONTOSO から自身の資格情報でこのコンピューターに認証することを防ぐ彼には、このコンピューター上で guest アカウントのマッピングを削除します。
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
Mike Danseglio のアカウント CONTOSO Kerberos 領域内では、このコンピューターで、既存のアカウントにマップします。 (場合のみ、標準ユーザー アカウントと guest アカウントは、このコンピューター上でアクティブには、Mike の特権に設定するもの)。
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
CONTOSO Kerberos 領域内のすべてのアカウントをこのコンピューターに同じ名前の既存のアカウントにマップするには。
```
ksetup /mapuser * *
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)