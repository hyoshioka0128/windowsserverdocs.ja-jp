---
title: bitsadmin ピアキャッシュと getconfigurationflags
description: '**Bitsadmin ピアキャッシュ**と**Getconfigurationflags**の Windows コマンドに関するトピックでは、コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: be8d6a719d63c8e9c6250320560b6ce21274c680
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850175"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin ピアキャッシュと getconfigurationflags

コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの構成フラグを取得します。

```
C:\> bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)