---
title: bitsadmin setnoprogresstimeout
description: '**Bitsadmin setnoprogresstimeout**の Windows コマンドに関するトピックでは、一時的なエラーが発生した後にサービスがファイルの転送を試行する時間の長さを秒単位で設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8adff95b0dbae68634db2e248d4493549c5ac85d
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122882"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

最初の一時的なエラーが発生した後に、BITS がファイルの転送を試行する時間を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setnoprogresstimeout <job> <timeoutvalue>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| timeoutvalue | 最初のエラーの後、ファイルの転送を BITS が待機する時間 (秒単位)。 |

## <a name="remarks"></a>コメント

- ジョブが最初の一時的なエラーを検出したときに、"進行状況なし" のタイムアウト間隔が開始されます。

- データのバイトが正常に転送されると、タイムアウト間隔が停止またはリセットされます。

- "進行状況なし" のタイムアウト間隔が*timeoutvalue*を超えると、ジョブは致命的なエラー状態になります。

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの "進行状況なし" タイムアウト値を20秒に設定します。

```
C:\>bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)