---
title: bitsadmin addfile
description: Bitsadmin addfile コマンドの参照記事。指定されたジョブにファイルを追加します。
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9bc00f1b63c559d048c9ae590df29f7421e42ec
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894937"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

指定されたジョブにファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfile <job> <remoteURL> <localname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| remoteURL | サーバー上のファイルの URL。 |
| localname | ローカルコンピューター上のファイルの名前。 *Localname*には、ファイルへの絶対パスが含まれている必要があります。 |

## <a name="examples"></a>例

ジョブにファイルを追加するには、次のようにします。

```
bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

追加する各ファイルに対してこの呼び出しを繰り返します。 複数のジョブが*Mydownloadjob*を名前として使用する場合は、ジョブを一意に識別するために、 *mydownloadjob*をジョブの GUID に置き換える必要があります。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
