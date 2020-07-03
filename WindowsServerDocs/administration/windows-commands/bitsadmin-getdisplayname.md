---
title: bitsadmin getdisplayname
description: Bitsadmin getdisplayname コマンドの参照記事。指定されたジョブの表示名を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0e768f377b9faa23eb59645cbecdc129f1e573
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923042"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

指定されたジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの表示名を取得するには、次のようにします。

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
