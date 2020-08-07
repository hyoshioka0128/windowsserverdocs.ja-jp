---
title: bitsadmin getnoprogresstimeout
description: Bitsadmin getnoprogresstimeout コマンドの参照記事。一時的なエラーが発生した後に、サービスがファイルの転送を試行する時間 (秒単位) を取得します。
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0bd85d93416e5e5718f5be830c99936a3080e24
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894136"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

一時的なエラーが発生した後に、サービスがファイルの転送を試行する時間 (秒単位) を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの進行状況のタイムアウト値を取得するには、次のようにします。

```
bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
