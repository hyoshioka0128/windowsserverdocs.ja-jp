---
title: bitsadmin setpeercachingflags
description: '**Bitsadmin setpeercachingflags**の Windows コマンドトピックでは、ジョブのファイルをキャッシュしてピアに提供できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b4a7807975fb46440301e30b1fdbd01784d7c85
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122775"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

ジョブのファイルをキャッシュしてピアに提供できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| value | 次を含む符号なし整数。<ul><li>**1.** ジョブは、ピアからコンテンツをダウンロードできます。</li><li>**2.** ジョブのファイルをキャッシュしてピアに配信できます。</li></ul> |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのフラグを設定して、ピアからコンテンツをダウンロードできるようにします。

```
C:\>bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)