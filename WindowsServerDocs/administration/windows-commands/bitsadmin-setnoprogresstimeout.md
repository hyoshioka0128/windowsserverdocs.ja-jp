---
title: bitsadmin setnoprogresstimeout
description: Bitsadmin setnoprogresstimeout の Windows コマンドに関するトピックでは、一時的なエラーが発生した後にサービスがファイルの転送を試行する時間の長さを秒単位で設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 544a6c73f29684bc4091ec05fa28016fbc718bb2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849355"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

最初の一時的なエラーが発生した後に、BITS がファイルの転送を試行する時間を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|TimeOutvalue|秒単位で表された数値。|

## <a name="remarks"></a>コメント

-   ジョブで一時的なエラーが発生した場合、進行状況のタイムアウト間隔は開始されません。
-   データのバイトが正常に転送されると、タイムアウト間隔が停止またはリセットされます。
-   進行状況のタイムアウト間隔が*TimeOutvalue*を超えると、ジョブは致命的なエラー状態になります。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの 進行状況なしのタイムアウト値を20秒に設定します。
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)