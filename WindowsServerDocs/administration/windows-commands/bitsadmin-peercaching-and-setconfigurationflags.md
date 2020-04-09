---
title: bitsadmin ピアキャッシュと setconfigurationflags
description: '**Bitsadmin ピアキャッシュ**と**setconfigurationflags**の Windows コマンドに関するトピックでは、コンピューターがピアにコンテンツを提供できるかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebaa09da2d4594d2762e67dc5884dd15cf4d1da8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850135"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin ピアキャッシュと setconfigurationflags

コンピューターがピアにコンテンツを提供できるかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| value | バイナリ表現のビットを次のように解釈する符号なし整数。<ul><li> ジョブのデータをピアからダウンロードできるようにするには、最下位ビットを設定します。</li><li>ジョブのデータをピアに配信できるようにするには、右側の2番目のビットを設定します。</li></ul>|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブについて、ピアからダウンロードされるジョブのデータを指定します。

```
C:\> bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)