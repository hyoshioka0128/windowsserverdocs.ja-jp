---
title: bitsadmin getpeercachingflags
description: Bitsadmin getpeercachingflags コマンドのリファレンストピックでは、ジョブのファイルをキャッシュしてピアに提供できるかどうか、および BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f30eead56958af3cd0fb0d91f6ee2bf9f79fdc4e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717688"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ジョブのファイルをキャッシュしてピアに提供できるかどうか、および BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのフラグを取得するには、次のようにします。

```
bitsadmin /getpeercachingflags myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
