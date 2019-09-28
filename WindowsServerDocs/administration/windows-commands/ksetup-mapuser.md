---
title: 'ksetup: mapuser'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6b80538999c364e9ed10ca0ed43387f603ac9ad3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374980"
---
# <a name="ksetupmapuser"></a>ksetup: mapuser



Kerberos プリンシパルの名前をアカウントにマップします。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /mapuser <Principal> <Account>
```

### <a name="parameters"></a>パラメーター

|  パラメーター   |                                                   説明                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<Principal > |              任意のプリンシパルの完全修飾ドメイン名。たとえば、mike@corp.CONTOSO.COM です。              |
|  \<Account >  | このコンピューター上に存在するアカウントまたはセキュリティグループの名前 (Guest、Domain Users、Administrator など)。 |

## <a name="remarks"></a>コメント

ドメインのゲストなど、特定のアカウントを指定できます。 または、ワイルドカード文字 (*) を使用して、すべてのアカウントを含めることができます。

アカウント名を省略した場合は、指定されたプリンシパルのマッピングが削除されます。

コンピューターは、有効な Kerberos チケットが存在する場合にのみ、指定された領域のプリンシパルを認証します。

現在マップされている設定と既定の領域を表示するには、パラメーターまたは引数を指定せずに**ksetup**を使用します。

外部キー配布センター (KDC) と領域の構成に変更が加えられるたびに、設定が変更されたコンピューターの再起動が必要になります。

## <a name="BKMK_Examples"></a>例

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

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)