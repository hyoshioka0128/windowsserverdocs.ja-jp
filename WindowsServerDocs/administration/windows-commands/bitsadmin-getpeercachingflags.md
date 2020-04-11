---
title: bitsadmin getpeercachingflags
description: '**Bitsadmin getpeercachingflags**の Windows コマンドトピックでは、ジョブのファイルをキャッシュしてピアに提供できるかどうか、および BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59ff3e3a5802c6023d85129c82f19cd7ee625d2f
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123120"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ジョブのファイルをキャッシュしてピアに提供できるかどうか、および BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのフラグを取得します。

```
C:\>bitsadmin /getpeercachingflags myJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)