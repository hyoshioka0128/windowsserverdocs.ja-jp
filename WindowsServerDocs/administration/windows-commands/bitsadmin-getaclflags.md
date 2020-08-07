---
title: bitsadmin getaclflags
description: アクセス制御リスト (ACL) の伝達フラグを取得する bitsadmin getaclflags コマンドの参照記事。
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 437ad345ec778290499b7b128ee08ffd41be320c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894573"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

項目が子オブジェクトによって継承されているかどうかを示すアクセス制御リスト (ACL) の伝達フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

### <a name="remarks"></a>Remarks

次のフラグ値のうち1つ以上を返します。

- **o** -所有者の情報をファイルにコピーします。

- **g** -グループ情報をファイルと共にコピーします。

- **d** -随意アクセス制御リスト (DACL) の情報をファイルと共にコピーします。

- **s** -システムアクセス制御リスト (SACL) の情報をファイルにコピーします。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを取得するには、次の操作を行います。

```
bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
