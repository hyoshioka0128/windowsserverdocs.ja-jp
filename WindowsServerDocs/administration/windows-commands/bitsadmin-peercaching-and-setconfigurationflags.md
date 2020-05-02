---
title: bitsadmin peercaching および setconfigurationflags
description: Bitsadmin ピアリングと setconfigurationflags コマンドのリファレンストピック。コンピューターがピアにコンテンツを提供できるかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c3ce69ce7a372311ce0c30e9b3a391ea33f45ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717238"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin peercaching および setconfigurationflags

コンピューターがピアにコンテンツを提供できるかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| value | バイナリ表現のビットを次のように解釈する符号なし整数。<ul><li>ジョブのデータをピアからダウンロードできるようにするには、最下位ビットを設定します。</li><li>ジョブのデータをピアに配信できるようにするには、右側の2番目のビットを設定します。</li></ul>|

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブについて、ピアからダウンロードするジョブのデータを指定するには、次のようにします。

```
bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)

- [bitsadmin ピアキャッシュコマンド](bitsadmin-peercaching.md)
