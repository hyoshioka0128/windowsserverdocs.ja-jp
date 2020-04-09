---
title: bitsadmin getreplyprogress
description: '**Bitsadmin getreplyprogress**の Windows コマンドに関するトピックでは、サーバーのアップロード応答のサイズと進行状況を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 195ed669817bc0aca7ebc432e7f3c66ab1548162
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850485"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

サーバーのアップロード応答のサイズと進行状況を取得します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /getreplyprogress <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |


## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアップロード応答の進行状況を取得します。

```
C:\>bitsadmin /getreplyprogress myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)