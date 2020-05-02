---
title: bitsadmin setnoprogresstimeout
description: Bitsadmin setnoprogresstimeout コマンドのリファレンストピックでは、一時的なエラーが発生した後にサービスがファイルの転送を試行する時間の長さを秒単位で設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 398882cf795e98dc0bbc0fb81006d3406fded707
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720111"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

最初の一時的なエラーが発生した後に、BITS がファイルの転送を試行する時間を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setnoprogresstimeout <job> <timeoutvalue>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| timeoutvalue | 最初のエラーの後、ファイルの転送を BITS が待機する時間 (秒単位)。 |

### <a name="remarks"></a>Remarks

- ジョブが最初の一時的なエラーを検出したときに、"進行状況なし" のタイムアウト間隔が開始されます。

- データのバイトが正常に転送されると、タイムアウト間隔が停止またはリセットされます。

- "進行状況なし" のタイムアウト間隔が*timeoutvalue*を超えると、ジョブは致命的なエラー状態になります。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの "進行状況なし" タイムアウト値を20秒に設定するには、次のようにします。

```
bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
