---
title: bitsadmin setpeercachingflags
description: Bitsadmin setpeercachingflags コマンドのリファレンストピックでは、ジョブのファイルをキャッシュしてピアに提供できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b66b169c38ac050ecaaf6546365547148faa9cf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717265"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

ジョブのファイルをキャッシュしてピアに提供できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| value | 次を含む符号なし整数。<ul><li>**1.** ジョブは、ピアからコンテンツをダウンロードできます。</li><li>**2.** ジョブのファイルをキャッシュしてピアに配信できます。</li></ul> |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブでピアからコンテンツをダウンロードできるようにするには、次のようにします。

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
