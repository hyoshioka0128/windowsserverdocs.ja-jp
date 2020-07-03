---
title: bitsadmin getcreationtime
description: Bitsadmin get time コマンドの参照記事。指定されたジョブの作成時刻を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0efc3d2a0f0f2cf3e72a4ff634733b16ef80055d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923084"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

指定されたジョブの作成時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの作成時刻を取得するには、次のようにします。

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
