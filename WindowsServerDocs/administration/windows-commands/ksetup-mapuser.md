---
title: ksetup mapuser
description: Kerberos プリンシパルの名前をアカウントにマップする ksetup mapuser コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f387b8c3ff7cf7515a4f2ed9b8ea62d379332ec7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933690"
---
# <a name="ksetup-mapuser"></a>ksetup mapuser

Kerberos プリンシパルの名前をアカウントにマップします。

## <a name="syntax"></a>構文

```
ksetup /mapuser <principal> <account>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<principal>` | 任意のプリンシパルユーザーの完全修飾ドメイン名を指定します。 たとえば、mike@corp.CONTOSO.COM のようにします。 アカウントパラメーターを指定しない場合、指定されたプリンシパルのマッピングが削除されます。 |
| `<account>` | このコンピューターに存在するアカウントまたはセキュリティグループの名前を指定します ( **Guest**、 **Domain Users**、 **Administrator**など)。 このパラメーターを省略すると、指定したプリンシパルのマッピングが削除されます。 |

#### <a name="remarks"></a>注釈

- **ドメインのゲスト**など、特定のアカウントを指定することも、ワイルドカード文字 (*) を使用してすべてのアカウントを含めることもできます。

- コンピューターは、有効な Kerberos チケットが存在する場合にのみ、指定された領域のプリンシパルを認証します。

- 外部キー配布センター (KDC) と領域の構成に変更が加えられるたびに、設定が変更されたコンピューターの再起動が必要になります。

### <a name="examples"></a>例

現在マップされている設定と既定の領域を表示するには、次のように入力します。

```
ksetup
```

Kerberos 領域 CONTOSO 内の Mike Danseglio のアカウントをこのコンピューターのゲストアカウントにマップするには、このコンピューターに対して認証を行わずに、組み込みのゲストアカウントのメンバーのすべての特権を付与します。

```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```

このコンピューターのゲストアカウントへの Mike Danseglio のアカウントのマッピングを削除して、CONTOSO からの資格情報でこのコンピューターを認証できないようにするには、次のように入力します。

```
ksetup /mapuser mike@corp.CONTOSO.COM
```

CONTOSO Kerberos 領域内の Mike Danseglio のアカウントを、このコンピューター上の既存のアカウントにマップするには、次のように入力します。

```
ksetup /mapuser mike@corp.CONTOSO.COM *
```

> [!NOTE]
> このコンピューターで、標準のユーザーアカウントとゲストアカウントのみがアクティブになっている場合は、Mike の特権がこれらのアカウントに設定されます。

CONTOSO Kerberos 領域内のすべてのアカウントを、このコンピューター上の同じ名前の既存のアカウントにマップするには、次のように入力します。

```
ksetup /mapuser * *
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)
