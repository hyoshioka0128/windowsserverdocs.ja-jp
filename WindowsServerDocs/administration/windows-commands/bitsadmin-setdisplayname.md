---
title: bitsadmin setdisplayname
description: Bitsadmin setdisplayname コマンドの参照記事。指定されたジョブの表示名を設定します。
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac83fee33703555f1a8ba4b65ae8dc4d0f947916
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893167"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

指定されたジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| display_name | 特定のジョブの表示名として使用されるテキスト。 |

## <a name="examples"></a>例

ジョブの表示名を*Mydownloadjob*に設定するには、次のようにします。

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
