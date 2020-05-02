---
title: bitsadmin getnotifyflags
description: 指定されたジョブの通知フラグを取得する bitsadmin getnotifyflags コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36e4c3584b2e3be9c9985756aeaec08b40e74b0c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717764"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

指定されたジョブの通知フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="remarks"></a>Remarks

ジョブには、次の1つまたは複数の通知フラグを含めることができます。

| フラグ | [説明] |
| ----- | ----- |
| 0x001 | ジョブ内のすべてのファイルが転送されたときにイベントを生成します。 |
| 0x002 | エラーが発生したときにイベントを生成します。 |
| 0x004 | 通知を無効にします。 |
| 0x008 | ジョブが変更されたとき、または転送の進行状況が発生したときにイベントを生成します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの通知フラグを取得するには、次のようにします。

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
