---
title: 'ksetup: mapuser'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f61c67fa21eccb77601b78aed51791259d609c5e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841485"
---
# <a name="ksetupmapuser"></a>ksetup: mapuser



Kerberos プリンシパルの名前をアカウントにマップします。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /mapuser <Principal> <Account>
```

#### <a name="parameters"></a>パラメーター

|  パラメーター   |                                                   説明                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<プリンシパル > |              任意のプリンシパルの完全修飾ドメイン名。たとえば、mike@corp.CONTOSO.COMのようにします。              |
|  \<アカウント >  | このコンピューター上に存在するアカウントまたはセキュリティグループの名前 (Guest、Domain Users、Administrator など)。 |

## <a name="remarks"></a>コメント

ドメインのゲストなど、特定のアカウントを指定できます。 または、ワイルドカード文字 (*) を使用して、すべてのアカウントを含めることができます。

アカウント名を省略した場合は、指定されたプリンシパルのマッピングが削除されます。

コンピューターは、有効な Kerberos チケットが存在する場合にのみ、指定された領域のプリンシパルを認証します。

現在マップされている設定と既定の領域を表示するには、パラメーターまたは引数を指定せずに**ksetup**を使用します。

外部キー配布センター (KDC) と領域の構成に変更が加えられるたびに、設定が変更されたコンピューターの再起動が必要になります。

## <a name="examples"></a><a name=BKMK_Examples></a>例

Kerberos 領域 CONTOSO 内の Mike Danseglio のアカウントをこのコンピューターの guest アカウントにマップし、このコンピューターに対する認証を行わずに、組み込みのゲストアカウントのメンバーのすべての特権を付与します。
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
このコンピューターのゲストアカウントに Mike Danseglio のアカウントのマッピングを削除して、CONTOSO からの資格情報でこのコンピューターを認証できないようにします。
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
CONTOSO Kerberos 領域内の Mike Danseglio のアカウントを、このコンピューターの既存のアカウントにマップします。 (このコンピューターで、標準のユーザーアカウントとゲストアカウントのみがアクティブになっている場合、Mike の特権は次のように設定されます)。
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
CONTOSO Kerberos 領域内のすべてのアカウントを、このコンピューター上の同じ名前の既存のアカウントにマップします。
```
ksetup /mapuser * *
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)