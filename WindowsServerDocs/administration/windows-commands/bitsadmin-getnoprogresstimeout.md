---
title: bitsadmin getnoprogresstimeout
description: Bitsadmin getnoprogresstimeout コマンドのリファレンストピックでは、一時的なエラーが発生した後にサービスがファイルの転送を試行する時間の長さを秒単位で取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ee0377bde8a438f23ca571bc9859deef92f18fb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717819"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

一時的なエラーが発生した後に、サービスがファイルの転送を試行する時間 (秒単位) を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの進行状況のタイムアウト値を取得するには、次のようにします。

```
bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
