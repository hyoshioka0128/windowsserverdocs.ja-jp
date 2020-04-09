---
title: bitsadmin geterror
description: '**Bitsadmin geterror**の Windows コマンドに関するトピックでは、指定されたジョブの詳細なエラー情報を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c65b072bb190e3e516b917c310942146bb3f3d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850705"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

指定されたジョブの詳細なエラー情報を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのエラー情報を取得します。

```
C:\>bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)