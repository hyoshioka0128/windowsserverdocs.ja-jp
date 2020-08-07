---
title: bitsadmin getproxybypasslist
description: Bitsadmin getproxybypasslist コマンドの参照記事。指定されたジョブのプロキシバイパスリストを取得します。
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16cca14a47f086be65764da5441d915d2d28d2db
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894005"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

指定されたジョブのプロキシバイパスリストを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

### <a name="remarks"></a>Remarks

バイパスリストには、プロキシ経由でルーティングされないホスト名または IP アドレス (またはその両方) が含まれます。 この一覧には、 `<local>` 同じ LAN 上のすべてのサーバーを参照するを含めることができます。 リストはセミコロン (;)またはスペースで区切られます。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのプロキシバイパス一覧を取得するには、次のようにします。

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
