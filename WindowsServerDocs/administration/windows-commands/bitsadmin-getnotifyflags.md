---
title: bitsadmin getnotifyflags
description: Bitsadmin getnotifyflags コマンドの参照記事。指定されたジョブの通知フラグを取得します。
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5368069b66b94436c9641527868267676fd6acb9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894085"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

指定されたジョブの通知フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="remarks"></a>Remarks

ジョブには、次の1つまたは複数の通知フラグを含めることができます。

| フラグ | 説明 |
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
